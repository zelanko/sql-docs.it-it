---
title: Rinominare una stored procedure | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [SQL Server], renaming
- renaming stored procedures
ms.assetid: 5d2e4c68-7e0b-4405-8919-f5b203e46770
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b85a6a5e79c004eb3ed2c7c40c6e3b62d526e95a
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/27/2019
ms.locfileid: "58536283"
---
# <a name="rename-a-stored-procedure"></a>Rinominare una stored procedure
  In questo argomento viene descritto come rinominare una stored procedure in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] tramite [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Limitazioni e restrizioni](#Restrictions)  
  
     [Sicurezza](#Security)  
  
-   **Per rinominare una stored procedure tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Restrictions"></a> Limitazioni e restrizioni  
  
-   I nomi delle procedure devono essere conformi alle regole per gli [identificatori](../databases/database-identifiers.md).  
  
-   La ridenominazione di una stored procedure non comporta la modifica del nome dell'oggetto corrispondente nella colonna di definizione della vista del catalogo **sys.sql_modules** . È pertanto consigliabile evitare di rinominare questo tipo di oggetto. In alternativa, eliminare e ricreare la stored procedure con il nuovo nome.  
  
-   La modifica del nome o della definizione di una stored procedure può causare un errore degli oggetti dipendenti se questi non vengono aggiornati in base alle modifiche apportate alla stored procedure. Per altre informazioni, vedere [Visualizzare le dipendenze di una stored procedure](view-the-dependencies-of-a-stored-procedure.md).  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 CREATE PROCEDURE  
 Sono richieste l'autorizzazione CREATE PROCEDURE per il database e ALTER per lo schema in cui viene creata la procedura oppure è richiesta l'appartenenza al ruolo predefinito **db_ddladmin** del database.  
  
 ALTER PROCEDURE  
 È richiesta l'autorizzazione ALTER per la procedura o l'appartenenza al ruolo predefinito **db_ddladmin** del database.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-rename-a-stored-procedure"></a>Per rinominare una stored procedure  
  
1.  In Esplora oggetti connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] , quindi espanderla.  
  
2.  Espandere **Database**, espandere il database a cui appartiene la stored procedure, quindi espandere **Programmabilità**.  
  
3.  [Determinare le dipendenze della stored procedure](view-the-dependencies-of-a-stored-procedure.md).  
  
4.  Espandere **Stored Procedures**, fare clic con il pulsante destro del mouse sulla procedura da rinominare e quindi scegliere **Rinomina**.  
  
5.  Modificare il nome della stored procedure.  
  
6.  Modificare il nome della stored procedure in qualsiasi oggetto dipendente o script che vi fa riferimento.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-rename-a-stored-procedure"></a>Per rinominare una stored procedure  
  
1.  Connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Dalla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**. In questo esempio viene illustrato come rinominare una stored procedure eliminandola e ricreandola con un nuovo nome. Nel primo esempio si crea la stored procedure `'HumanResources.uspGetAllEmployeesTest`, nel secondo esempio la stored procedure viene rinominata in `HumanResources.uspEveryEmployeeTest`.  
  
```sql  
--Create the stored procedure.  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'HumanResources.uspGetAllEmployeesTest', 'P' ) IS NOT NULL   
    DROP PROCEDURE HumanResources.uspGetAllEmployeesTest;  
GO  
CREATE PROCEDURE HumanResources.uspGetAllEmployeesTest  
AS  
    SET NOCOUNT ON;  
    SELECT LastName, FirstName, Department  
    FROM HumanResources.vEmployeeDepartmentHistory;  
GO  
  
--Rename the stored procedure.  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'HumanResources.uspGetAllEmployeesTest', 'P' ) IS NOT NULL   
    DROP PROCEDURE HumanResources.uspGetAllEmployeesTest;  
GO  
CREATE PROCEDURE HumanResources.uspEveryEmployeeTest  
AS  
    SET NOCOUNT ON;  
    SELECT LastName, FirstName, Department  
    FROM HumanResources.vEmployeeDepartmentHistory;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [ALTER PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-procedure-transact-sql)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)   
 [Creazione di una stored procedure](../stored-procedures/create-a-stored-procedure.md)   
 [Modificare una stored procedure](../stored-procedures/modify-a-stored-procedure.md)   
 [Eliminare una stored procedure](../stored-procedures/delete-a-stored-procedure.md)   
 [Visualizzare la definizione di una stored procedure](view-the-definition-of-a-stored-procedure.md)   
 [Visualizzare le dipendenze di una stored procedure](view-the-dependencies-of-a-stored-procedure.md)  
  
  
