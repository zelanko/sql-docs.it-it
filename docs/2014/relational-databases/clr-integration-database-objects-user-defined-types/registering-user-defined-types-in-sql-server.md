---
title: Registrazione di tipi definiti dall'utente in SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- TSQL
helpviewer_keywords:
- UDTs [CLR integration], maintaining
- user-defined types [CLR integration], maintaining
- dependencies [CLR integration]
- deploying user-defined types [CLR integration]
- CurrencyConversion function
- user-defined types [CLR integration], deploying
- Transact-SQL deploying UDTs
- assemblies [CLR integration], user-defined types
- cross-database UDT support
- CREATE ASSEMBLY statement
- DROP TYPE statement
- Currency UDT
- CREATE TYPE statement
- registering user-defined types
- UDTs [CLR integration], deploying
- removing user-defined types
- user-defined types [CLR integration], registering
- ALTER ASSEMBLY statement
- UDTs [CLR integration], registering
- ADD FILE clause
ms.assetid: f7da3e92-e407-4f0b-b3a3-f214e442b37d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 19ea6e9f077b5097b8c5daa6d967a17336553ba7
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62919943"
---
# <a name="registering-user-defined-types-in-sql-server"></a>Registrazione dei tipi definiti dall'utente in SQL Server
  Per utilizzare un tipo definito dall'utente (UDT) in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è necessario registrarlo. La registrazione di un tipo definito dall'utente (UDT) comporta la registrazione dell'assembly e la creazione del tipo nel database in cui si desidera utilizzarlo. I tipi definiti dall'utente (UDT) vengono definiti nell'ambito di un singolo database e non possono essere utilizzati in più database a meno che lo stesso assembly e lo stesso tipo definito dall'utente (UDT) non vengano registrati con ogni database. Dopo la registrazione dell'assembly del tipo definito dall'utente (UDT) e la creazione del tipo, è possibile utilizzare il tipo definito dall'utente (UDT) in [!INCLUDE[tsql](../../includes/tsql-md.md)] e nel codice client. Per altre informazioni, vedere [Tipi CLR definiti dall'utente](clr-user-defined-types.md).  
  
## <a name="using-visual-studio-to-deploy-udts"></a>Utilizzo di Visual Studio per distribuire i tipi definiti dall'utente (UDT)  
 Il modo più semplice per distribuire il tipo definito dall'utente (UDT) è utilizzare [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Studio. Per scenari di distribuzione più complessi e una maggiore flessibilità utilizzare tuttavia [!INCLUDE[tsql](../../includes/tsql-md.md)] come illustrato più avanti in questo argomento.  
  
 Seguire questi passaggi per creare e distribuire un tipo definito dall'utente (UDT) mediante Visual Studio:  
  
1.  Creare un nuovo progetto di **database** nei nodi del linguaggio **Visual Basic** o **Visual C#** .  
  
2.  Aggiungere un riferimento al database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che conterrà il tipo definito dall'utente (UDT).  
  
3.  Aggiungere una classe di **tipo definito dall'utente** .  
  
4.  Scrivere il codice per implementare il tipo definito dall'utente (UDT).  
  
5.  Scegliere **Distribuisci**dal menu **Compila** . per registrare l'assembly e creare il tipo nel database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="using-transact-sql-to-deploy-udts"></a>Utilizzo di Transact-SQL per distribuire i tipi definiti dall'utente (UDT)  
 La sintassi [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE ASSEMBLY viene utilizzata per registrare l'assembly nel database in cui si desidera utilizzare il tipo definito dall'utente (UDT). Viene archiviata internamente nelle tabelle di sistema del database e non esternamente nel file system. Se il tipo definito dall'utente (UDT) dipende dagli assembly esterni, questi dovranno essere caricati nel database. L'istruzione CREATE TYPE viene utilizzata per creare il tipo definito dall'utente (UDT) nel database in cui deve essere utilizzato. Per altre informazioni, vedere [CREATE ASSEMBLY &#40;Transact-sql&#41;](/sql/t-sql/statements/create-assembly-transact-sql) e [create Type &#40;transact-SQL&#41;](/sql/t-sql/statements/create-type-transact-sql).  
  
### <a name="using-create-assembly"></a>Utilizzo di CREATE ASSEMBLY  
 La sintassi CREATE ASSEMBLY registra l'assembly nel database in cui si desidera utilizzare il tipo definito dall'utente (UDT). Dopo avere registrato l'assembly, non saranno presenti dipendenze.  
  
 Non è possibile creare più versioni dello stesso assembly in uno specifico database. È tuttavia possibile creare più versioni dello stesso assembly basate sulle impostazioni cultura in un database specificato. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] distingue più versioni dell'impostazione cultura di un assembly dai nomi diversi come registrate nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per ulteriori informazioni, vedere la sezione relativa alla creazione e all'utilizzo di assembly con nome sicuro in .NET Framework SDK.  
  
 Quando CREATE ASSEMBLY viene eseguito con il set di autorizzazioni SAFE o EXTERNAL_ACCESS, l'assembly viene controllato per garantire che sia verificabile e indipendente dai tipi. Se non si specifica un set di autorizzazioni, viene utilizzato SAFE. Il codice con il set di autorizzazioni UNSAFE non viene controllato. Per altre informazioni sui set di autorizzazioni per gli assembly, vedere [Progettazione di assembly](../../relational-databases/clr-integration/assemblies-designing.md).  
  
#### <a name="example"></a>Esempio  
 Nell'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente viene registrato l'assembly Point [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in nel database **AdventureWorks** con il set di autorizzazioni SAFE. Se la clausola WITH PERMISSION_SET viene omessa, l'assembly viene registrato con il set di autorizzazioni SAFE.  
  
```  
USE AdventureWorks;  
CREATE ASSEMBLY Point  
FROM '\\ShareName\Projects\Point\bin\Point.dll'   
WITH PERMISSION_SET = SAFE;  
```  
  
 Nell'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente viene registrato l'assembly utilizzando *<assembly_bits argomento>* nella clausola from. Il valore `varbinary` rappresenta il file come flusso di byte.  
  
```  
USE AdventureWorks;  
CREATE ASSEMBLY Point  
FROM 0xfeac4 ... 21ac78  
```  
  
### <a name="using-create-type"></a>Utilizzo di CREATE TYPE  
 Dopo avere caricato l'assembly nel database, è possibile creare il tipo utilizzando l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] CREATE TYPE. In questo modo il tipo viene aggiunto all'elenco di tipi disponibili per il database. Il tipo viene definito nell'ambito del database e può essere utilizzato solo nel database in cui è stato creato. Se il tipo definito dall'utente (UDT) esiste già nel database, l'istruzione CREATE TYPE ha esito negativo e restituisce un errore.  
  
> [!NOTE]  
>  La sintassi CREATE TYPE viene utilizzata anche per la creazione dei tipi di dati alias [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nativi e deve sostituire `sp_addtype` per creare i tipi di dati alias. Alcuni argomenti facoltativi nella sintassi CREATE TYPE si riferiscono alla creazione dei tipi definiti dall'utente (UDT) e non sono applicabili alla creazione dei tipi di dati alias, ad esempio il tipo di base.  
  
 Per ulteriori informazioni, vedere [CREATE TYPE &#40;&#41;Transact-SQL ](/sql/t-sql/statements/create-type-transact-sql).  
  
#### <a name="example"></a>Esempio  
 Nell'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente viene creato il tipo `Point`. Il nome esterno viene specificato utilizzando la sintassi di denominazione in due parti di *AssemblyName*. *NomeUDT*.  
  
```  
CREATE TYPE dbo.Point   
EXTERNAL NAME Point.[Point];  
```  
  
## <a name="removing-a-udt-from-the-database"></a>Rimozione di un tipo definito dall'utente (UDT) dal database  
 L'istruzione DROP TYPE rimuove un tipo definito dall'utente (UDT) dal database corrente. Dopo avere eliminato un tipo definito dall'utente (UDT), è possibile utilizzare l'istruzione DROP ASSEMBLY per eliminare l'assembly dal database.  
  
 L'istruzione DROP TYPE non viene eseguita nelle situazioni seguenti:  
  
-   Tabelle del database che contengono colonne definite mediante il tipo definito dall'utente (UDT).  
  
-   Funzioni, stored procedure o trigger che utilizzano variabili o parametri del tipo definito dall'utente (UDT), creati nel database con la clausola WITH SCHEMABINDING.  
  
### <a name="example"></a>Esempio  
 La seguente istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] deve essere eseguita nell'ordine indicato. È necessario eliminare prima la tabella a cui fa riferimento il tipo definito dall'utente (UDT) `Point`, quindi il tipo e infine l'assembly.  
  
```  
DROP TABLE dbo.Points;  
DROP TYPE dbo.Point;  
DROP ASSEMBLY Point;  
```  
  
### <a name="finding-udt-dependencies"></a>Ricerca di dipendenze di tipi definiti dall'utente (UDT)  
 Se sono presenti oggetti dipendenti, ad esempio tabelle con definizioni di colonne con tipo definito dall'utente (UDT), l'istruzione DROP TYPE avrà esito negativo. L'istruzione avrà esito negativo anche se nel database sono stati creati trigger, funzioni o stored procedure mediante la clausola WITH SCHEMABINDING, e tali routine utilizzano variabili o parametri del tipo definito dall'utente (UDT). È necessario innanzitutto eliminare tutti gli oggetti dipendenti, quindi eseguire l'istruzione DROP TYPE.  
  
 Nella query [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente vengono individuate tutte le colonne e i parametri che utilizzano un tipo definito dall'utente nel database **AdventureWorks** .  
  
```  
USE Adventureworks;  
SELECT o.name AS major_name, o.type_desc AS major_type_desc  
     , c.name AS minor_name, c.type_desc AS minor_type_desc  
     , at.assembly_class  
  FROM (  
        SELECT object_id, name, user_type_id, 'SQL_COLUMN' AS type_desc  
          FROM sys.columns  
     UNION ALL  
        SELECT object_id, name, user_type_id, 'SQL_PROCEDURE_PARAMETER'  
          FROM sys.parameters  
     ) AS c  
  JOIN sys.objects AS o  
    ON o.object_id = c.object_id  
  JOIN sys.assembly_types AS at  
    ON at.user_type_id = c.user_type_id;  
```  
  
## <a name="maintaining-udts"></a>Gestione di tipi definiti dall'utente (UDT)  
 Non è possibile modificare un tipo definito dall'utente (UDT) una volta creato in un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], sebbene sia possibile modificare l'assembly sul quale si basa il tipo. Nella maggior parte dei casi, è necessario rimuovere il tipo definito dall'utente (UDT) dal database con l'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] DROP TYPE, apportare le modifiche all'assembly sottostante e ricaricarlo mediante l'istruzione ALTER ASSEMBLY. È necessario quindi ricreare il tipo definito dall'utente (UDT) e tutti gli oggetti dipendenti.  
  
### <a name="example"></a>Esempio  
 L'istruzione ALTER ASSEMBLY viene utilizzata dopo avere apportato le modifiche al codice sorgente nell'assembly del tipo definito dall'utente (UDT) e averlo ricompilato. Il file con estensione dll viene copiato nel server e riassociato al nuovo assembly. Per la sintassi completa, vedere [ALTER ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-assembly-transact-sql).  
  
 L'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] ALTER ASSEMBLY seguente ricarica l'assembly Point.dll dal percorso specificato su disco.  
  
```  
ALTER ASSEMBLY Point  
FROM '\\Projects\Point\bin\Point.dll'  
```  
  
### <a name="using-alter-assembly-to-add-source-code"></a>Utilizzo di ALTER ASSEMBLY per aggiungere codice sorgente  
 La clausola ADD FILE nella sintassi ALTER ASSEMBLY non è presente in CREATE ASSEMBLY. È possibile utilizzarla per aggiungere codice sorgente o altri file associati a un assembly. I file vengono copiati dai percorsi originali e vengono archiviati nelle tabelle di sistema del database. In questo modo il codice sorgente o gli altri file saranno sempre disponibili nel caso in cui sia necessario ricreare o documentare la versione corrente del tipo definito dall'utente (UDT).  
  
 L'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] alter assembly seguente aggiunge il codice sorgente della classe Point.cs per `Point` il tipo definito dall'utente. Il testo contenuto nel file Point.cs viene copiato e archiviato nel database con il nome "PointSource".  
  
```  
ALTER ASSEMBLY Point  
ADD FILE FROM '\\Projects\Point\Point.cs' AS PointSource;  
```  
  
 Le informazioni sull'assembly vengono archiviate nella tabella **sys. assembly_files** nel database in cui è stato installato l'assembly. La tabella **sys. assembly_files** contiene le colonne seguenti.  
  
 **assembly_id**  
 Identificatore definito per l'assembly. Questo numero viene assegnato a tutti gli oggetti relativi allo stesso assembly.  
  
 **nome**  
 Nome dell'oggetto .  
  
 **file_id**  
 Numero che identifica ogni oggetto, con il primo oggetto associato a un dato **assembly_id** a cui viene assegnato il valore 1. Se sono presenti più oggetti associati alla stessa **assembly_id**, ogni valore **file_id** successivo viene incrementato di 1.  
  
 **contenuto**  
 Rappresentazione esadecimale dell'assembly o del file.  
  
 È possibile utilizzare la funzione CAST o CONVERT per convertire il contenuto della colonna **contenuto** in testo leggibile. Nella query seguente il contenuto del file Point.cs viene convertito in testo leggibile, utilizzando il nome nella clausola WHERE per limitare il set di risultati a una singola riga.  
  
```  
SELECT CAST(content AS varchar(8000))   
  FROM sys.assembly_files   
  WHERE name='PointSource';  
```  
  
 Se i risultati vengono copiati e incollati in un editor di testo, si noterà come le interruzioni di riga e gli spazi presenti nell'originale sono stati conservati.  
  
## <a name="managing-udts-and-assemblies"></a>Gestione di assembly e di tipi definiti dall'utente (UDT)  
 Quando si pianifica l'implementazione di tipi definiti dall'utente (UDT), considerare quali metodi sono necessari nell'assembly del tipo definito dall'utente (UDT) stesso e quali metodi devono essere creati in assembly separati e implementati come stored procedure o funzioni definite dall'utente. La separazione dei metodi in assembly distinti consente di aggiornare il codice senza influire sui dati che possono essere archiviati in una colonna con tipo definito dall'utente (UDT) di una tabella. È possibile modificare gli assembly del tipo definito dall'utente (UDT) senza eliminare le colonne con tipo definito dall'utente (UDT) e gli altri oggetti dipendenti solo quando la nuova definizione può leggere i valori precedenti e la firma del tipo non viene modificata.  
  
 Separando il codice procedurale che può cambiare dal codice necessario per implementare il tipo definito dall'utente (UDT) si semplifica notevolmente la manutenzione. Includendo solo il codice necessario per l'utilizzo del tipo definito dall'utente (UDT) e mantenendo le definizioni del tipo definito dall'utente (UDT) il più semplice possibile, si riduce il rischio di dovere eliminare il tipo definito dall'utente (UDT) dal database per revisioni del codice o correzioni di bug.  
  
### <a name="the-currency-udt-and-currency-conversion-function"></a>Funzione di conversione valuta e tipo definito dall'utente (UDT) Currency  
 Il tipo definito dall'utente **Currency** nel database di esempio **AdventureWorks** fornisce un esempio utile della modalità consigliata per strutturare un tipo definito dall'utente e le funzioni associate. Il tipo definito dall'utente **Currency** viene usato per gestire i costi in base al sistema monetario di determinate impostazioni cultura e consente l'archiviazione di diversi tipi di valuta, ad esempio dollari, euro e così via. La classe del tipo definito dall'utente (UDT) espone il nome della lingua come stringa e l'importo come tipo di dati `decimal`. Tutti i metodi di serializzazione necessari sono contenuti all'interno dell'assembly che definisce la classe. La funzione che implementa la conversione di valuta da una lingua a un'altra viene implementata come funzione esterna denominata **ConvertCurrency**e questa funzione si trova in un assembly separato. La funzione **ConvertCurrency** esegue le operazioni recuperando il tasso di conversione da una tabella del database **AdventureWorks** . Se l'origine dei tassi di conversione deve essere modificata o se devono essere apportate altre modifiche al codice esistente, l'assembly può essere facilmente modificato senza influire sul tipo definito dall'utente di **valuta** .  
  
 Il listato di codice per le funzioni di tipo definito dall'utente **Currency** e **ConvertCurrency** può essere trovato installando gli esempi di Common Language Runtime (CLR).  
  
### <a name="using-udts-across-databases"></a>Utilizzo di tipi definiti dall'utente (UDT) tra database  
 I tipi definiti dall'utente (UDT) vengono definiti nell'ambito di un singolo database. Un tipo definito dall'utente (UDT) in un database non può pertanto essere utilizzato in una definizione di colonna di un altro database. Per utilizzare i tipi definiti dall'utente (UDT) in più database, è necessario eseguire le istruzioni CREATE ASSEMBLY e CREATE TYPE in ogni database in assembly identici. Gli assembly sono considerati identici se hanno nome, nome sicuro, lingua, versione, set di autorizzazioni e contenuto binario identici.  
  
 Dopo avere registrato e reso accessibile il tipo definito dall'utente (UDT) in entrambi database, è possibile convertire un valore UDT in un database per utilizzarlo nell'altro. I tipi definiti dall'utente (UDT) identici possono essere utilizzati tra i database negli scenari seguenti:  
  
-   Chiamata a una stored procedure definita in database diversi.  
  
-   Esecuzione di una query su tabelle definite in database diversi.  
  
-   Selezione di dati del tipo definito dall'utente (UDT) da una colonna con tipo definito dall'utente (UDT) della tabella di database e inserimento di tali dati in un secondo database con una colonna con tipo definito dall'utente (UDT) identica.  
  
 In queste situazioni, la conversione richiesta dal server viene eseguita automaticamente. Non è possibile eseguire le conversioni in modo esplicito mediante le funzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] CAST o CONVERT.  
  
 Si noti che non è necessario eseguire alcuna azione per l'utilizzo dei tipi [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] definiti dall'utente durante la creazione di tabelle di lavoro nel database di sistema **tempdb** . Sono incluse la gestione di cursori, variabili di tabella e funzioni con valori di tabella definite dall'utente che includono tipi definiti dall'utente e che utilizzano in modo trasparente **tempdb**. Tuttavia, se si crea in modo esplicito una tabella temporanea in **tempdb** che definisce una colonna con tipo definito dall'utente, il tipo definito dall'utente deve essere registrato in **tempdb** allo stesso modo di un database utente.  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi CLR definiti dall'utente](clr-user-defined-types.md)  
  
  
