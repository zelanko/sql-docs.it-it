---
title: Visualizzare la definizione di una stored procedure | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [SQL Server], viewing
- definition of stored procedure
- viewing stored procedures
- displaying stored procedures
ms.assetid: 93318587-a0c5-4788-946f-3b5dc8372ea9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 333d4d9f0ab9feb5d5b5c4d0aa48fd584cef3143
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62856507"
---
# <a name="view-the-definition-of-a-stored-procedure"></a>Visualizzare la definizione di una stored procedure
    
##  <a name="Top"></a> In [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] è possibile visualizzare la definizione di una stored procedure mediante le opzioni di menu di Esplora oggetti o mediante [!INCLUDE[tsql](../../includes/tsql-md.md)]nell'editor di query. In questo argomento viene descritto come visualizzare la definizione di una stored procedura in Esplora oggetti e nell'editor di query mediante una stored procedure di sistema, una funzione di sistema e una vista del catalogo dell'oggetto.  
  
-   **Prima di iniziare:**  [Sicurezza](#Security)  
  
-   **Per visualizzare la definizione di una stored procedure usando:**  [SQL Server Management Studio](#SSMSProcedure), [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Stored procedure di sistema: `sp_helptext`  
 È richiesta l'appartenenza al ruolo **public** . Le definizioni degli oggetti di sistema sono visibili pubblicamente. La definizione degli oggetti utente è visibile al proprietario dell'oggetto o agli utenti autorizzati che dispongono di una delle seguenti autorizzazioni: ALTER, controllo, TAKE OWNERSHIP o VIEW DEFINITION.  
  
 Funzione di sistema: `OBJECT_DEFINITION`  
 Le definizioni degli oggetti di sistema sono visibili pubblicamente. La definizione degli oggetti utente è visibile al proprietario dell'oggetto o agli utenti autorizzati che dispongono di una delle seguenti autorizzazioni: ALTER, controllo, TAKE OWNERSHIP o VIEW DEFINITION. Queste autorizzazioni sono assegnate implicitamente ai membri dei ruoli predefiniti del database **db_owner**, **db_ddladmin**e **db_securityadmin** .  
  
 Vista del catalogo dell'oggetto: `sys.sql_modules`  
 La visibilità dei metadati nelle viste del catalogo è limitata alle entità a protezione diretta di cui l'utente è proprietario o per le quali dispone di autorizzazioni. Per altre informazioni, vedere [Metadata Visibility Configuration](../security/metadata-visibility-configuration.md).  
  
##  <a name="Procedures"></a> Visualizzazione della definizione di una stored procedure  
 È possibile usare uno dei seguenti elementi:  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
 **Per visualizzare la definizione di una stored procedure in Esplora oggetti**  
  
1.  In Esplora oggetti connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)] , quindi espanderla.  
  
2.  Espandere **Database**, espandere il database a cui appartiene la stored procedure, quindi espandere **Programmabilità**.  
  
3.  Espandere **Stored procedure**, fare doppio clic la procedura e quindi fare clic su **lo Script per Stored Procedure**, quindi fare clic su uno dei seguenti: **Per creare**, **Alter in**, o **Drop e Create in**.  
  
4.  Selezionare **Nuova finestra editor di query**. Verrà visualizzata la definizione della stored procedure.  
  
###  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
 **Per visualizzare la definizione di una stored procedure nell'editor di query**  
  
 Stored procedure di sistema: `sp_helptext`  
 1.  In Esplora oggetti connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra degli strumenti fare clic su **Nuova query**.  
  
3.  Nella finestra Query immettere l'istruzione seguente che usano la stored procedure di sistema `sp_helptext`. Modificare il nome del database e della stored procedure in modo da indicare il database e la stored procedure desiderati.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    EXEC sp_helptext N'AdventureWorks2012.dbo.uspLogError';  
    ```  
  
 Funzione di sistema: `OBJECT_DEFINITION`  
 1.  In Esplora oggetti connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra degli strumenti fare clic su **Nuova query**.  
  
3.  Nella finestra Query immettere le istruzioni seguenti che usano la funzione di sistema `OBJECT_DEFINITION`. Modificare il nome del database e della stored procedure in modo da indicare il database e la stored procedure desiderati.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT OBJECT_DEFINITION (OBJECT_ID(N'AdventureWorks2012.dbo.uspLogError'));  
    ```  
  
 Vista del catalogo dell'oggetto: `sys.sql_modules`  
 1.  In Esplora oggetti connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra degli strumenti fare clic su **Nuova query**.  
  
3.  Nella finestra Query immettere le istruzioni seguenti che usano la vista del catalogo `sys.sql_modules`. Modificare il nome del database e della stored procedure in modo da indicare il database e la stored procedure desiderati.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT definition  
    FROM sys.sql_modules  
    WHERE object_id = (OBJECT_ID(N'AdventureWorks2012.dbo.uspLogError'));  
    ```  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di una stored procedure](create-a-stored-procedure.md)   
 [Modificare una stored procedure](modify-a-stored-procedure.md)   
 [Eliminare una stored procedure](delete-a-stored-procedure.md)   
 [Rinominare una stored procedure](rename-a-stored-procedure.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](/sql/t-sql/functions/object-definition-transact-sql)   
 [sys.sql_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql)   
 [sp_helptext &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helptext-transact-sql)   
 [OBJECT_ID &#40;Transact-SQL&#41;](/sql/t-sql/functions/object-id-transact-sql)  
  
  
