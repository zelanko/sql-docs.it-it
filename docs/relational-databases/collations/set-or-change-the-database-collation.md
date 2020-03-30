---
title: Impostare o modificare le regole di confronto del database | Microsoft Docs
ms.custom: ''
ms.date: 10/11/2019
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2221d88e5f564b08f993f68f9be4131588aebe2a
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "78866110"
---
# <a name="set-or-change-the-database-collation"></a>Impostare o modificare le regole di confronto del database
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  In questo argomento viene descritto come impostare e modificare le regole di confronto del database in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Se non viene specificata alcuna regola di confronto, vengono utilizzate le regole di confronto del server.  
  
> [!IMPORTANT]
> La modifica delle regole di confronto del database non è esplicitamente proibita nel database SQL di Azure. Richiede tuttavia il blocco esclusivo sul database e altri processi utente e processi in background, ad esempio il background che esegue i backup, potrebbero mantenere i blocchi del database e impedire la modifica delle regole di confronto. L'istruzione `ALTER DATABASE COLLATE` nel database SQL di Azure avrà esito negativo se viene eseguita mentre i processi in background accedono al database. Se si verifica un errore di timeout del blocco, sarà necessario ripetere l'istruzione. 
 
> [!NOTE]
> Le regole di confronto non possono essere modificate usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] dopo la creazione del database in [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Possono essere modificate solo tramite [!INCLUDE[tsql](../../includes/tsql-md.md)].

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
  
-   Le regole di confronto solo Unicode di Windows possono essere usate solo con la clausola COLLATE per essere applicate ai tipi di dati **nchar**, **nvarchar**e **ntext** per i dati a livello di colonna e di espressione. Non è possibile utilizzarle con la clausola COLLATE per modificare le regole di confronto di un database o un'istanza del server.  
  
-   Se le regole di confronto specificate o adottate dall'oggetto cui viene fatto riferimento utilizzano una tabella codici non supportata dai sistemi operativi Windows, nel [!INCLUDE[ssDE](../../includes/ssde-md.md)] viene visualizzato un errore.  

-   Le regole di confronto non possono essere modificate usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] dopo la creazione del database in [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. Possono essere modificate solo tramite [!INCLUDE[tsql](../../includes/tsql-md.md)].
  
###  <a name="recommendations"></a><a name="Recommendations"></a> Raccomandazioni  
  
È possibile trovare i nomi delle regole di confronto supportate in [Windows_collation_name &#40;Transact-SQL&#41;](../../t-sql/statements/windows-collation-name-transact-sql.md) e [Nome delle regole di confronto di SQL Server &#40;Transact-SQL&#41;](../../t-sql/statements/sql-server-collation-name-transact-sql.md); oppure è possibile usare la funzione di sistema [sys.fn_helpcollations &#40;Transact-SQL&#41;](../../relational-databases/system-functions/sys-fn-helpcollations-transact-sql.md) .  
  
Quando si modificano le regole di confronto del database, è possibile modificare gli elementi seguenti:  
  
-   Qualsiasi **char**, **varchar**, **text**, **nchar**, **nvarchar**o colonna **ntext** nelle tabelle di sistema viene impostata sulle nuove regole di confronto.  
  
-   Tutti i parametri esistenti di tipo **char**, **varchar**, **text**, **nchar**, **nvarchar**o **ntext** , i valori scalari restituiti per le stored procedure e le funzioni definite dall'utente vengono modificati in base alle nuove regole di confronto.  
  
-   I tipi di dati di sistema **char**, **varchar**, **text**, **nchar**, **nvarchar**o **ntext** e tutti i tipi di dati definiti dall'utente basati su tali tipi di dati di sistema vengono modificati in base alle nuove regole di confronto predefinite.  
  
È possibile modificare le regole di confronto di qualsiasi nuovo oggetto creato in un database utente usando la clausola `COLLATE` dell'istruzione [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md). Questa istruzione **non consente di modificare** le regole di confronto delle colonne delle tabelle definite dall'utente esistenti. Per modificare le regole di confronto delle colonne, è necessario usare la clausola `COLLATE` dell'istruzione [ALTER TABLE](../../t-sql/statements/alter-table-transact-sql.md).  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 Per creare un nuovo database è richiesta l'autorizzazione `CREATE DATABASE` nel database **master** oppure l'autorizzazione `CREATE ANY DATABASE` o `ALTER ANY DATABASE`.  
  
 Per modificare le regole di confronto di un database esistente è richiesta l'autorizzazione `ALTER` per il database.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Con SQL Server Management Studio  
  
#### <a name="to-set-or-change-the-database-collation"></a>Per impostare o modificare le regole di confronto del database  
  
1.  In **Esplora oggetti**connettersi a un'istanza di [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], espandere tale istanza, quindi espandere **Database**.  
  
2.  Se si crea un nuovo database, fare clic con il pulsante destro del mouse su **Database** , quindi fare clic su **Nuovo database**. Se non si vuole usare le regole di confronto predefinite, fare clic sulla pagina **Opzioni** e selezionare le regole di confronto dall'elenco a discesa **Regole di confronto** .  
  
     In alternativa, se il database esiste già, fare clic con il pulsante destro del mouse sul database desiderato e fare clic su **Proprietà**. Fare clic sulla pagina **Opzioni** e selezionare le regole di confronto dall'elenco a discesa **Regole di confronto** .  
  
3.  Al termine dell'operazione scegliere **OK**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Con Transact-SQL  
  
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
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)  
  
  
