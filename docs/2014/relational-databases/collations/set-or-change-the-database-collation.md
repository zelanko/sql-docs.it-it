---
title: Impostare o modificare le regole di confronto del database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- collations [SQL Server], database
- database collations [SQL Server]
ms.assetid: 1379605c-1242-4ac8-ab1b-e2a2b5b1f895
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 38c29f8d70b3cc72baf81e2ae23082fe270ba573
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62874035"
---
# <a name="set-or-change-the-database-collation"></a>Impostare o modificare le regole di confronto del database
  In questo argomento viene descritto come impostare e modificare le regole di confronto del database in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Se non viene specificata alcuna regola di confronto, vengono utilizzate le regole di confronto del server.  
  
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
  
-   Le regole di confronto solo Unicode di Windows possono essere utilizzate solo con la clausola COLLATE per essere applicate ai tipi di dati `nchar`, `nvarchar` e `ntext` per i dati a livello di colonna e di espressione. Non è possibile utilizzarle con la clausola COLLATE per modificare le regole di confronto di un database o un'istanza del server.  
  
-   Se le regole di confronto specificate o adottate dall'oggetto cui viene fatto riferimento utilizzano una tabella codici non supportata dai sistemi operativi Windows, nel [!INCLUDE[ssDE](../../includes/ssde-md.md)] viene visualizzato un errore.  
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Indicazioni  
  
-   È possibile trovare i nomi delle regole di confronto supportate in [Windows_collation_name &#40;Transact-SQL&#41;](/sql/t-sql/statements/windows-collation-name-transact-sql) e [Nome delle regole di confronto di SQL Server &#40;Transact-SQL&#41;](/sql/t-sql/statements/sql-server-collation-name-transact-sql); oppure è possibile usare la funzione di sistema [sys.fn_helpcollations &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-helpcollations-transact-sql) .  
  
-   Quando si modificano le regole di confronto del database, è possibile modificare gli elementi seguenti:  
  
    -   Qualsiasi `char`, `varchar`, `text`, `nchar`, `nvarchar` o colonna `ntext` nelle tabelle di sistema viene impostata sulle nuove regole di confronto.  
  
    -   Tutti i parametri di tipo `char`, `varchar`, `text`, `nchar`, `nvarchar` o `ntext` e i valori scalari restituiti per le stored procedure e le funzioni definite dall'utente vengono modificati in base alle nuove regole di confronto.  
  
    -   I tipi di dati di sistema `char`, `varchar`, `text`, `nchar`, `nvarchar` o `ntext` e tutti i tipi di dati definiti dall'utente basati sui questi tipi di dati di sistema vengono modificati in base alle nuove regole di confronto predefinite.  
  
-   È possibile modificare le regole di confronto di qualsiasi nuovo oggetto creato in un database utente utilizzando la clausola COLLATE dell'istruzione [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql) . Questa istruzione non consente di modificare le regole di confronto delle colonne delle tabelle definite dall'utente esistenti. Per modificare le regole di confronto delle colonne, è necessario utilizzare la clausola COLLATE dell'istruzione [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql).  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 CREATE DATABASE  
 È richiesta l'autorizzazione CREATE DATABASE nel database **Master** oppure l'autorizzazione create any database o ALTER ANY database.  
  
 ALTER DATABASE  
 È richiesta l'autorizzazione ALTER per il database.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-set-or-change-the-database-collation"></a>Per impostare o modificare le regole di confronto del database  
  
1.  In **Esplora oggetti**connettersi a un'istanza di [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], espandere tale istanza, quindi espandere **Database**.  
  
2.  Se si crea un nuovo database, fare clic con il pulsante destro del mouse su **Database** , quindi fare clic su **Nuovo database**. Se non si vuole usare le regole di confronto predefinite, fare clic sulla pagina **Opzioni** e selezionare le regole di confronto dall'elenco a discesa **Regole di confronto** .  
  
     In alternativa, se il database esiste già, fare clic con il pulsante destro del mouse sul database desiderato e fare clic su **Proprietà**. Fare clic sulla pagina **Opzioni** e selezionare le regole di confronto dall'elenco a discesa **Regole di confronto** .  
  
3.  Al termine dell'operazione scegliere **OK**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-set-the-database-collation"></a>Per impostare le regole di confronto del database  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio viene mostrato come utilizzare la clausola [COLLATE](/sql/t-sql/statements/collations) per specificare un nome delle regole di confronto. Nell'esempio viene creato l'elemento `MyOptionsTest` del database che utilizza le regole di confronto `Latin1_General_100_CS_AS_SC` . Dopo aver creato il database, eseguire l'istruzione `SELECT` per verificare l'impostazione.  
  
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
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio viene mostrato come utilizzare la clausola [COLLATE](/sql/t-sql/statements/collations) in un'istruzione [ALTER DATABASE](/sql/t-sql/statements/alter-database-transact-sql) per modificare il nome delle regole di confronto. Eseguire l'istruzione `SELECT` per verificare la modifica.  
  
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
 [Regole di confronto e supporto Unicode](collation-and-unicode-support.md)   
 [sys.fn_helpcollations &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-helpcollations-transact-sql)   
 [sys.databases &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql)   
 [Nome delle regole di confronto di SQL Server &#40;Transact-SQL&#41;](/sql/t-sql/statements/sql-server-collation-name-transact-sql)   
 [Windows_collation_name &#40;Transact-SQL&#41;](/sql/t-sql/statements/windows-collation-name-transact-sql)   
 [COLLATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/collations)   
 [Precedenza delle regole di confronto &#40;Transact-SQL&#41;](/sql/t-sql/statements/collation-precedence-transact-sql)   
 [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)   
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](/sql/t-sql/statements/create-database-sql-server-transact-sql)   
 [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
  
