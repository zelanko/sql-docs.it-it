---
description: Impostare o modificare le regole di confronto del database
title: Impostare o modificare le regole di confronto del database | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- collations [SQL Server], database
- database collations [SQL Server]
ms.assetid: 1379605c-1242-4ac8-ab1b-e2a2b5b1f895
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7fbaf22758dcf62d2159e63ee3af3c0507f3f607
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97460574"
---
# <a name="set-or-change-the-database-collation"></a>Impostare o modificare le regole di confronto del database
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Questo argomento descrive come impostare e modificare le regole di confronto del database usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Se non viene specificata alcuna regola di confronto, vengono utilizzate le regole di confronto del server.  
  
> [!IMPORTANT]
> L'istruzione `ALTER DATABASE COLLATE` nel database SQL di Azure non è supportata.

 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Indicazioni](#Recommendations)  
  
     [Sicurezza](#Security)  
  
-   **Per impostare o modificare le regole di confronto del database utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   Le regole di confronto solo Unicode di Windows possono essere usate solo con la clausola COLLATE per essere applicate ai tipi di dati **nchar**, **nvarchar** e **ntext** per i dati a livello di colonna e di espressione. Non è possibile utilizzarle con la clausola COLLATE per modificare le regole di confronto di un database o un'istanza del server.  
  
-   Se le regole di confronto specificate o adottate dall'oggetto cui viene fatto riferimento utilizzano una tabella codici non supportata dai sistemi operativi Windows, nel [!INCLUDE[ssDE](../../includes/ssde-md.md)] viene visualizzato un errore.  

###  <a name="recommendations"></a><a name="Recommendations"></a> Indicazioni  
  
È possibile trovare i nomi delle regole di confronto supportate in [Windows_collation_name &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md) e [Nome delle regole di confronto di SQL Server &#40;Transact-SQL&#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md); oppure è possibile usare la funzione di sistema [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md) .  
  
Quando si modificano le regole di confronto del database, è possibile modificare gli elementi seguenti:  
  
-   Qualsiasi **char**, **varchar**, **text**, **nchar**, **nvarchar** o colonna **ntext** nelle tabelle di sistema viene impostata sulle nuove regole di confronto.  
  
-   Tutti i parametri esistenti di tipo **char**, **varchar**, **text**, **nchar**, **nvarchar** o **ntext** , i valori scalari restituiti per le stored procedure e le funzioni definite dall'utente vengono modificati in base alle nuove regole di confronto.  
  
-   I tipi di dati di sistema **char**, **varchar**, **text**, **nchar**, **nvarchar** o **ntext** e tutti i tipi di dati definiti dall'utente basati su tali tipi di dati di sistema vengono modificati in base alle nuove regole di confronto predefinite.  
  
È possibile modificare le regole di confronto di qualsiasi nuovo oggetto creato in un database utente usando la clausola `COLLATE` dell'istruzione [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md). Questa istruzione **non consente di modificare** le regole di confronto delle colonne delle tabelle definite dall'utente esistenti. Per modificare le regole di confronto delle colonne, è necessario usare la clausola `COLLATE` dell'istruzione [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).  

> [!IMPORTANT]
> La modifica delle regole di confronto di un database o di singole colonne **non modifica** i dati sottostanti già archiviati nelle tabelle esistenti. A meno che l'applicazione non gestisca in modo esplicito la conversione e il confronto dei dati tra regole di confronto diverse, è consigliabile eseguire la transizione dei dati esistenti nel database alle nuove regole di confronto. Si evita così il rischio che le applicazioni modifichino erroneamente i dati, causando possibili risultati errati o una perdita di dati invisibile all'utente.   

Quando si modificano le regole di confronto del database, solo le nuove tabelle erediteranno le nuove regole di confronto del database per impostazione predefinita. Sono disponibili diverse alternative per convertire i dati esistenti nelle nuove regole di confronto:
-  Convertire i dati sul posto. Per convertire le regole di confronto per una colonna in una tabella esistente, vedere [Impostare o modificare le regole di confronto della colonna](../../relational-databases/collations/set-or-change-the-column-collation.md). Questa operazione è facile da implementare, ma può diventare un problema notevole per tabelle di grandi dimensioni e applicazioni occupate. Vedere l'esempio seguente per una conversione sul posto della colonna `MyString` per nuove regole di confronto:

   ```sql
   ALTER TABLE dbo.MyTable
   ALTER COLUMN MyString VARCHAR(50) COLLATE Latin1_General_100_CI_AI_SC_UTF8;
   ```

-  Copiare i dati nelle nuove tabelle che usano le nuove regole di confronto e sostituire le tabelle originali nello stesso database. Creare una nuova tabella nel database corrente che erediterà le regole di confronto del database, copiare i dati tra la tabella precedente e la nuova tabella, eliminare la tabella originale e rinominare la nuova tabella con il nome della tabella originale. Si tratta di un'operazione più rapida rispetto a una conversione sul posto, ma può diventare complicata quando si gestiscono schemi complessi con dipendenze quali vincoli di chiave esterna, vincoli di chiave primaria e trigger. Richiede anche una sincronizzazione dei dati finale tra la tabella originale e quella nuova prima del taglio finale, se i dati continuano a essere modificati dalle applicazioni. Vedere l'esempio seguente per una conversione con "copia e sostituzione" della colonna `MyString` per le nuove regole di confronto:

   ```sql
   CREATE TABLE dbo.MyTable2 (MyString VARCHAR(50) COLLATE Latin1_General_100_CI_AI_SC_UTF8); 
   
   INSERT INTO dbo.MyTable2 
   SELECT * FROM dbo.MyTable; 
   
   DROP TABLE dbo.MyTable; 
   
   EXEC sp_rename 'dbo.MyTable2', 'dbo.MyTable’;
   ```

-  Copiare i dati in un nuovo database che usa le nuove regole di confronto e sostituire il database originale. Creare un nuovo database usando le nuove regole di confronto e trasferire i dati dal database originale tramite strumenti come [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] o l'Importazione/Esportazione guidata [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Questo è un approccio più semplice per gli schemi complessi. Richiede anche un sincronizzazione dei dati finale tra il database originale e quello nuovo prima del taglio finale, se i dati continuano a essere modificati dalle applicazioni.
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 Per creare un nuovo database è richiesta l'autorizzazione `CREATE DATABASE` nel database **master** oppure l'autorizzazione `CREATE ANY DATABASE` o `ALTER ANY DATABASE`.  
  
 Per modificare le regole di confronto di un database esistente è richiesta l'autorizzazione `ALTER` per il database.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-set-or-change-the-database-collation"></a>Per impostare o modificare le regole di confronto del database  
  
1.  In **Esplora oggetti** connettersi a un'istanza di [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], espandere tale istanza, quindi espandere **Database**.  
  
2.  Se si crea un nuovo database, fare clic con il pulsante destro del mouse su **Database** , quindi fare clic su **Nuovo database**. Se non si vuole usare le regole di confronto predefinite, fare clic sulla pagina **Opzioni** e selezionare le regole di confronto dall'elenco a discesa **Regole di confronto** .  
  
     In alternativa, se il database esiste già, fare clic con il pulsante destro del mouse sul database desiderato e fare clic su **Proprietà**. Fare clic sulla pagina **Opzioni** e selezionare le regole di confronto dall'elenco a discesa **Regole di confronto** .  
  
3.  Al termine dell'operazione scegliere **OK**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-set-the-database-collation"></a>Per impostare le regole di confronto del database  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio viene mostrato come utilizzare la clausola [COLLATE](~/t-sql/statements/collations.md) per specificare un nome delle regole di confronto. Nell'esempio viene creato l'elemento `MyOptionsTest` del database che utilizza le regole di confronto `Latin1_General_100_CS_AS_SC` . Dopo aver creato il database, eseguire l'istruzione `SELECT` per verificare l'impostazione.  
  
```sql  
USE master;  
GO  
IF DB_ID (N'MyOptionsTest') IS NOT NULL  
DROP DATABASE MyOptionsTest;  
GO  
CREATE DATABASE MyOptionsTest  
COLLATE Latin1_General_100_CS_AS_SC;  
GO  
  
--Verify the collation setting.  
SELECT name, collation_name  
FROM sys.databases  
WHERE name = N'MyOptionsTest';  
GO  
```  
  
#### <a name="to-change-the-database-collation"></a>Per modificare le regole di confronto del database  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio viene mostrato come utilizzare la clausola [COLLATE](~/t-sql/statements/collations.md) in un'istruzione [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) per modificare il nome delle regole di confronto. Eseguire l'istruzione `SELECT` per verificare la modifica.  
  
```sql  
USE master;  
GO  
ALTER DATABASE MyOptionsTest  
COLLATE French_CI_AS ;  
GO  
  
--Verify the collation setting.  
SELECT name, collation_name  
FROM sys.databases  
WHERE name = N'MyOptionsTest';  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Regole di confronto e supporto Unicode](../../relational-databases/collations/collation-and-unicode-support.md)   
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md)   
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [Nome delle regole di confronto di SQL Server &#40;Transact-SQL&#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md)   
 [Windows_collation_name &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md)   
 [COLLATE &#40;Transact-SQL&#41;](~/t-sql/statements/collations.md)   
 [Precedenza delle regole di confronto &#40;Transact-SQL&#41;](../../t-sql/statements/collation-precedence-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
