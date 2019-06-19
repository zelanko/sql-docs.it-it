---
title: Compilazione nativa di tabelle e stored procedure | Microsoft Docs
ms.custom: ''
ms.date: 07/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 5880fbd9-a23e-464a-8b44-09750eeb2dad
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e70ab55fedcc5053cf82a78c040c850a23824eb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63075196"
---
# <a name="native-compilation-of-tables-and-stored-procedures"></a>Compilazione nativa di tabelle e stored procedure
  Con OLTP in memoria viene introdotto il concetto di compilazione nativa. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può compilare in modo nativo stored procedure che accedono alle tabelle ottimizzate per la memoria. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è anche in grado di compilare in modo nativo tabelle ottimizzate per la memoria. Con la compilazione nativa si accede ai dati più velocemente e si eseguono le query in modo più efficiente rispetto al tradizionale [!INCLUDE[tsql](../../includes/tsql-md.md)]interpretato. La compilazione nativa di tabelle e stored procedure produce DLL.  
  
 È anche supportata la compilazione nativa dei tipi di tabella con ottimizzazione per la memoria. Per altre informazioni, vedere [Memory-Optimized Table Variables](../../database-engine/memory-optimized-table-variables.md).  
  
 La compilazione nativa si riferisce al processo di conversione dei costrutti di programmazione in codice nativo, costituito da istruzioni del processore senza la necessità di ulteriore compilazione o interpretazione.  
  
 OLTP in memoria compila le tabelle ottimizzate per la memoria quando vengono create e le stored procedure compilate in modo nativo quando vengono caricate nelle DLL native. Inoltre, le DLL vengono ricompilate dopo il riavvio di un database o di un server. Le informazioni necessarie per ricreare le DLL vengono archiviate nei metadati del database. Le DLL non fanno parte del database, sebbene siano associate al database. Ad esempio, le DLL non sono incluse nei backup del database.  
  
> [!NOTE]  
>  Le tabelle con ottimizzazione per la memoria vengono ricompilate durante un riavvio del server. Per velocizzare il recupero del database, le stored procedure compilate in modo nativo non vengono ricompilate durante un riavvio del server, ma vengono compilate al momento della prima esecuzione. A causa di questa compilazione posticipata, le stored procedure compilate in modo nativo vengono visualizzate solo quando si chiama [sys.dm_os_loaded_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-os-loaded-modules-transact-sql) dopo la prima esecuzione.  
  
## <a name="maintenance-of-in-memory-oltp-dlls"></a>Manutenzione delle DLL di OLTP in memoria  
 La query seguente indica che tutte le DLL di tabelle e stored procedure vengono attualmente caricate in memoria nel server:  
  
```sql  
SELECT name, description FROM sys.dm_os_loaded_modules  
where description = 'XTP Native DLL'  
```  
  
 Gli amministratori di database non devono gestire i file generati da una compilazione nativa. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rimuove automaticamente i file generati non più necessari. Ad esempio, i file generati verranno eliminati quando una tabella e una stored procedure vengono eliminate o nel caso in cui un database venga eliminato.  
  
> [!NOTE]  
>  Se la compilazione ha esito negativo o viene interrotta, alcuni file generati non vengono rimossi. Questi file vengono lasciati intenzionalmente per motivi di supporto e vengono rimossi quando il database viene eliminato.  
  
> [!NOTE]  
>  Durante l'avvio del database, SQL Server compila file DLL per tutte le tabelle necessarie per il ripristino del database. Se una tabella è stata eliminata immediatamente prima di un riavvio del database, è possibile che i file checkpoint o i log delle transazioni includano ancora residui della tabella. È quindi possibile ricompilare il file DLL della tabella durante l'avvio del database. Dopo il riavvio, il file DLL verrà scaricato e i file verranno rimossi durante il normale processo di pulitura.  
  
## <a name="native-compilation-of-tables"></a>Compilazione nativa di tabelle  
 Tramite la creazione di una tabella ottimizzata per la memoria mediante un'istruzione `CREATE TABLE` vengono restituite le informazioni della tabella scritte nei metadati del database e le strutture di indice e di tabella create in memoria. La tabella verrà compilata in una DLL.  
  
 Considerare il seguente script di esempio che crea un database e una tabella ottimizzata per la memoria:  
  
```sql  
use master  
go  
create database db1  
go  
alter database db1 add filegroup db1_mod contains memory_optimized_data  
go  
-- adapt filename as needed  
alter database db1 add file (name='db1_mod', filename='c:\data\db1_mod') to filegroup db1_mod  
go  
use db1  
go  
create table dbo.t1  
   (c1 int not null primary key nonclustered,  
    c2 INT)  
with (memory_optimized=on)  
go  
-- retrieve the path of the DLL for table t1  
select name, description FROM sys.dm_os_loaded_modules  
where name like '%xtp_t_' + cast(db_id() as varchar(10)) + '_' + cast(object_id('dbo.t1') as varchar(10)) + '.dll'  
go  
```  
  
 La creazione della tabella comporta anche la creazione della corrispondente DLL e il caricamento della DLL in memoria. La query DMV immediatamente dopo l'istruzione CREATE TABLE recupera il percorso della DLL della tabella.  
  
 La DLL della tabella interpreta le strutture di indice e il formato di riga della tabella. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usano la DLL per attraversare indici, recuperare righe e archiviare il contenuto delle righe.  
  
## <a name="native-compilation-of-stored-procedures"></a>Compilazione nativa di stored procedure  
 Le stored procedure che sono contrassegnate con NATIVE_COMPILATION vengono compilate in modo nativo. Pertanto, le istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] nella procedura vengono tutte compilate nel codice nativo per l'esecuzione efficiente della logica di business critica per le prestazioni.  
  
 Per altre informazioni sulle stored procedure compilate in modo nativo, vedere [Natively Compiled Stored Procedures](natively-compiled-stored-procedures.md).  
  
 Considerare la seguente stored procedure di esempio che inserisce righe nella tabella t1 dell'esempio precedente:  
  
```sql  
create procedure dbo.native_sp  
with native_compilation, schemabinding, execute as owner  
as  
begin atomic  
with (transaction isolation level=snapshot, language=N'us_english')  
  
  declare @i int = 1000000  
  while @i > 0  
  begin  
    insert dbo.t1 values (@i, @i+1)  
    set @i -= 1  
  end  
  
end  
go  
exec dbo.native_sp  
go  
-- reset  
delete from dbo.t1  
go  
```  
  
 La DLL di native_sp può interagire direttamente con la DLL di t1 e con il motore di archiviazione di OLTP in memoria per inserire le righe il più rapidamente possibile.  
  
 Il compilatore di OLTP in memoria usano Query Optimizer per creare un piano di esecuzione efficiente per ogni query della stored procedure. Si noti che le stored procedure compilate in modo nativo non vengono automaticamente ricompilate se i dati della tabella cambiano. Per altre informazioni sulla gestione delle statistiche e delle stored procedure con OLTP in memoria, vedere [Statistiche per tabelle con ottimizzazione per la memoria](memory-optimized-tables.md).  
  
## <a name="security-considerations-for-native-compilation"></a>Considerazioni sulla sicurezza della compilazione nativa  
 Per la compilazione nativa di tabelle e stored procedure viene usato il compilatore di OLTP in memoria. Il compilatore genera file che vengono scritti su disco e caricati in memoria. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono usati i seguenti meccanismi per limitare l'accesso a tali file.  
  
### <a name="native-compiler"></a>Compilatore nativo  
 Il file eseguibile del compilatore, nonché i file binari e i file di intestazione necessari per la compilazione nativa, vengono installati come parte dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nella cartella MSSQL\Binn\Xtp. Pertanto, se l'istanza predefinita viene installata in C:\Program Files, i file del compilatore vengono installati in C:\Program Files\\[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12. MSSQLSERVER\MSSQL\Binn\Xtp.  
  
 Per limitare l'accesso al compilatore, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono usati gli elenchi di controllo di accesso (ACL) per limitare l'accesso ai file binari. Tutti i file binari di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono protetti dalla modifica o dalla manomissione tramite gli ACL. Gli ACL del compilatore nativo limitano anche l'utilizzo del compilatore; solo gli amministratori di sistema e l'account del servizio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dispongono delle autorizzazioni di lettura ed esecuzione per i file del compilatore nativo.  
  
### <a name="files-generated-by-a-native-compilation"></a>File generati da una compilazione nativa  
 I file generati quando una tabella o una stored procedure viene compilata includono file DLL e file intermedi compresi i file con le estensioni seguenti: c, obj, xml e pdb. I file generati vengono salvati in una sottocartella della cartella dati predefinita. La sottocartella viene denominata Xtp. Quando si installa l'istanza predefinita con la cartella dati predefinita, i file generati vengono posizionati in C:\Program Files\\[!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL12. MSSQLSERVER\MSSQL\DATA\Xtp.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la manomissione dei file DLL generati viene impedita in tre modi:  
  
-   Quando una tabella o una stored procedure viene compilata in una DLL, tale DLL viene immediatamente caricata in memoria e collegata al processo sqlserver.exe. Non è possibile modificare una DLL mentre è collegata a un processo.  
  
-   Quando un database viene riavviato, tutte le tabelle e le stored procedure vengono ricompilate (rimosse e ricreate) in base ai metadati del database. In questo modo verranno rimosse tutte le modifiche apportate a un file generato da un agente dannoso.  
  
-   I file generati sono considerati parte dei dati utente e dispongono delle stesse restrizioni di sicurezza, tramite ACL, dei file di database: solo gli amministratori di sistema e l'account del servizio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono accedere a tali file.  
  
 Per gestire tali file, non sono necessarie interazioni dell'utente. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verranno creati e rimossi automaticamente in base alle necessità.  
  
## <a name="see-also"></a>Vedere anche  
 [Tabelle con ottimizzazione per la memoria](memory-optimized-tables.md)   
 [Natively Compiled Stored Procedures](natively-compiled-stored-procedures.md)  
  
  
