---
title: Visualizzare o modificare le proprietà di un database | Microsoft Docs
ms.custom: ''
ms.date: 01/05/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- displaying databases
- database viewing [SQL Server]
- databases [SQL Server], viewing
- viewing databases
ms.assetid: 9e8ac097-84b7-46c7-85e3-c1e79f94d747
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: dc1e6d1021e1e7cf30a683d8c81c625a56b9766c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68127062"
---
# <a name="view-or-change-the-properties-of-a-database"></a>Visualizzare o modificare le proprietà di un database
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

  In questo argomento si illustra come visualizzare o modificare le proprietà di un database in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Dopo aver modificato la proprietà di un database, la modifica diventa effettiva immediatamente.  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Indicazioni](#Recommendations)  
  
     [Security](#Security)  
  
-   **Per visualizzare o modificare le proprietà di un database utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Recommendations"></a> Indicazioni  
  
-   Se l'opzione AUTO_CLOSE è impostata su ON, alcune colonne nella vista del catalogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) e della funzione DATABASEPROPERTYEX restituiranno NULL perché il database non è disponibile per il recupero dei dati. Per risolvere questo problema, aprire il database.  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Richiede l'autorizzazione ALTER per il database per modificare le proprietà di un database. Richiede almeno l'appartenenza al ruolo del database Public per visualizzare le proprietà di un database.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-view-or-change-the-properties-of-a-database"></a>Per visualizzare o modificare le proprietà di un database  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], quindi espandere questa istanza.  
  
2.  Espandere **Database**, fare clic con il pulsante destro del mouse sul database da visualizzare, quindi scegliere **Proprietà**.  
  
3.  Nella finestra di dialogo **Proprietà database** selezionare una pagina per visualizzare le informazioni corrispondenti. Selezionare la pagina **File** , ad esempio, per visualizzare le informazioni sui file di dati e di log.  
  
##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
 Transact-SQL fornisce una serie di metodi diversi per visualizzare le proprietà di un database e la modifica delle proprietà di un database. Per visualizzare le proprietà di un database, è possibile usare la funzione [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md) e la vista del catalogo [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) . Per modificare le proprietà di un database, è possibile usare la versione dell'istruzione ALTER DATABASE per l'ambiente:  [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md) o [ALTER DATABASE (database SQL di Azure)](../../t-sql/statements/alter-database-azure-sql-database.md). Per visualizzare le proprietà con ambito database, usare la vista del catalogo [sys.database_scoped_configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) , mentre per modificarle, usare l'istruzione [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) .  
  
#### <a name="to-view-a-property-of-a-database-by-using-the-databasepropertyex-function"></a>Per visualizzare una proprietà di un database usando la funzione DATABASEPROPERTYEX  
  
1.  Connettersi a [!INCLUDE[ssDE](../../includes/ssde-md.md)] e quindi connettersi al database di cui vogliono visualizzare le proprietà.  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. Questo esempio usa la funzione di sistema [DATABASEPROPERTYEX](../../t-sql/functions/databasepropertyex-transact-sql.md) per restituire lo stato dell'opzione di database AUTO_SHRINK nel database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Un valore restituito pari a 1 indica che l'opzione è impostata su ON, mentre un valore restituito pari a 0 indica che l'opzione è impostata su OFF.  
  
    ```sql  
    SELECT DATABASEPROPERTYEX('AdventureWorks2012', 'IsAutoShrink');  
    ```  
  
#### <a name="to-view-the-properties-of-a-database-by-querying-sysdatabases"></a>Per visualizzare le proprietà di un database eseguendo una query su sys.databases  
  
1.  Connettersi a [!INCLUDE[ssDE](../../includes/ssde-md.md)] e quindi connettersi al database di cui vogliono visualizzare le proprietà.  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio si esegue una query sulla vista del catalogo [sys.databases](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md) per visualizzare diverse proprietà del database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . In questo esempio viene restituito il numero ID del database (`database_id`), se il database è di sola lettura o di lettura e scrittura (`is_read_only`), le regole di confronto per il database (`collation_name`), nonché il livello di compatibilità del database (`compatibility_level`).  
  
    ```sql  
    SELECT database_id, is_read_only, collation_name, compatibility_level  
    FROM sys.databases WHERE name = 'AdventureWorks2012';  
    ```  
  
#### <a name="to-view-the-properties-of-a-database-scoped-configuration-by-querying-sysdatabasesscopedconfiguration"></a>Per visualizzare le proprietà di una configurazione con ambito database eseguendo una query su sys.databases_scoped_configuration  
  
1.  Connettersi a [!INCLUDE[ssDE](../../includes/ssde-md.md)] e quindi connettersi al database di cui vogliono visualizzare le proprietà.  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio si esegue una query sulla vista del catalogo [sys.database_scoped_configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md) per visualizzare diverse proprietà del database corrente.  
  
    ```sql  
    SELECT configuration_id, name, value, value_for_secondary  
    FROM sys.database_scoped_configurations;  
    ```  
  
     Per altri esempi, vedere [sys.database_scoped_configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md)  
  
#### <a name="to-change-the-properties-of-a-sql-server-2016-database-using-alter-database"></a>Per modificare le proprietà di un database di SQL Server 2016 usando ALTER DATABASE  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query. Nell'esempio si determina lo stato di isolamento dello snapshot nel database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] , si modifica lo stato della proprietà, quindi si verifica la modifica.  
  
     Per determinare lo stato di isolamento dello snapshot, selezionare la prima istruzione `SELECT` e fare clic su **Esegui**.  
  
     Per modificare lo stato di isolamento dello snapshot, selezionare la prima istruzione `ALTER DATABASE` e fare clic su **Esegui**.  
  
     Per verificare la modifica, selezionare la seconda istruzione `SELECT` e fare clic su **Esegui**.  
  
     [!code-sql[DatabaseDDL#AlterDatabase9](../../relational-databases/databases/codesnippet/tsql/view-or-change-the-prope_1.sql)]  
  
#### <a name="to-change-the-database-scoped-properties-using-alter-database-scoped-configuration"></a>Per modificare le proprietà con ambito database usando ALTER DATABASE SCOPED CONFIGURATION  
  
1.  Connettersi a un database nell'istanza di SQL Server.  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query. L'esempio seguente imposta MAXDOP per un database secondario sul valore per il database primario.  
  
    ```sql  
    ALTER DATABASE SCOPED CONFIGURATION FOR SECONDARY SET MAXDOP = PRIMARY   
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [sys.databases &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-databases-transact-sql.md)   
 [DATABASEPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/databasepropertyex-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [ALTER DATABASE (database SQL di Azure)](../../t-sql/statements/alter-database-azure-sql-database.md)   
 [ALTER DATABASE SCOPED CONFIGURATION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md)   
 [sys.database_scoped_configurations &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-scoped-configurations-transact-sql.md)  

  
  
