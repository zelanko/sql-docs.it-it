---
title: Visualizzare le informazioni sullo spazio allocato ai dati e ai log per un database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], space
- status information [SQL Server], space
- displaying space information
- disk space [SQL Server], displaying
- databases [SQL Server], space used
- viewing space information
- space allocation [SQL Server], displaying
- data space [SQL Server]
ms.assetid: c7b99463-4bab-4e9b-9217-fcb0898dc757
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4850be4c112f9c0b987d543873cb55af08372455
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62917344"
---
# <a name="display-data-and-log-space-information-for-a-database"></a>Visualizzare le informazioni sullo spazio allocato ai dati e ai log per un database
  In questo argomento si illustra come visualizzare le informazioni sullo spazio allocato ai dati e ai log per un database in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per visualizzare le informazioni sullo spazio allocato ai dati e ai log per un database utilizzando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 L'autorizzazione per eseguire **sp_spaceused** è concessa al ruolo **public** . Solo i membri del ruolo predefinito del database **db_owner** possono specificare il parametro **@updateusage** .  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-display-data-and-log-space-information-for-a-database"></a>Per visualizzare le informazioni sullo spazio allocato ai dati e ai log per un database  
  
1.  In Esplora oggetti connettersi a un'istanza del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , quindi espanderla.  
  
2.  Espandere **Database**.  
  
3.  Fare clic con il pulsante destro del mouse su un database, scegliere **Report**, **Report standard**, quindi fare clic su **Utilizzo disco**.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-display-data-and-log-space-information-for-a-database-by-using-sp_spaceused"></a>Per visualizzare le informazioni sullo spazio allocato ai dati e ai log per un database utilizzando sp_spaceused  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio viene usata la stored procedure di sistema [sp_spaceused](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql) per fornire le informazioni sullo spazio su disco per la tabella `Vendor` e i relativi indici.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_spaceused N'Purchasing.Vendor';  
GO  
```  
  
#### <a name="to-display-data-and-log-space-information-for-a-database-by-querying-sysdatabase_files"></a>Per visualizzare le informazioni sullo spazio allocato ai dati e ai log per un database eseguendo una query su sys.database_files  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio si esegue una query sulla vista del catalogo [sys.database_files](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql) per restituire informazioni specifiche sui file di dati e di log nel database [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] .  
  
```sql  
USE AdventureWorks2012;  
GO  
SELECT file_id, name, type_desc, physical_name, size, max_size  
FROM sys.database_files ;  
GO  
  
```  
  
## <a name="see-also"></a>Vedi anche  
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)   
 [sys. database_files &#40;&#41;Transact-SQL](/sql/relational-databases/system-catalog-views/sys-database-files-transact-sql)   
 [sp_spaceused &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql)   
 [Aggiungere file di dati o di log a un database](add-data-or-log-files-to-a-database.md)   
 [Eliminare file di dati o file di log da un database](delete-data-or-log-files-from-a-database.md)  
  
  
