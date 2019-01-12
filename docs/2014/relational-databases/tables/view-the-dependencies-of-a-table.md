---
title: Visualizzare le dipendenze di una tabella | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- table dependencies [SQL Server]
- dependencies [SQL Server], tables
- displaying dependences
- viewing dependencies
ms.assetid: c4351ef5-e7d0-46e7-8367-88695e9974f8
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f5f30232a4f6d382af6e3a21f022b86cdf1a4fd4
ms.sourcegitcommit: 78e32562f9c1fbf2e50d3be645941d4aa457e31f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/08/2019
ms.locfileid: "54100746"
---
# <a name="view-the-dependencies-of-a-table"></a>Visualizzare le dipendenze di una tabella
  Le dipendenze di una tabella possono essere visualizzate in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] usando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per visualizzare le dipendenze di una tabella:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Permissions  
 Sono richieste l'autorizzazione VIEW DEFINITION sul database e l'autorizzazione SELECT su sys.sql_expression_dependencies per il database. L'autorizzazione SELECT è concessa per impostazione predefinita solo ai membri del ruolo predefinito del database di db_owner. Quando le autorizzazioni SELECT e VIEW DEFINITION vengono concesse a un altro utente, l'utente autorizzato può visualizzare tutte le dipendenze nel database.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-view-the-dependencies-of-a-table"></a>Per visualizzare le dipendenze di una tabella  
  
1.  In **Esplora oggetti**espandere **Database**, espandere un database e quindi espandere **Tabelle**.  
  
2.  Fare clic con il pulsante destro del mouse su una tabella e quindi scegliere **Visualizza dipendenze**.  
  
3.  Nella finestra di dialogo **Dipendenze oggetto**_\<nome oggetto>_ selezionare **Oggetti che dipendono da** _\<nome oggetto>_ oppure **Oggetti da cui** **dipende**_\<nome oggetto>_.  
  
4.  Selezionare un oggetto nella griglia **Dipendenze** . Il tipo di oggetto, ad esempio "Trigger" o "Stored procedure", viene visualizzato nella casella **Tipo** .  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-view-the-objects-that-depend-on-a-table"></a>Per visualizzare gli oggetti che dipendono da una tabella.  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra delle query e fare clic su **Esegui**.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT * FROM sys.sql_expression_dependencies  
    WHERE referencing_id = OBJECT_ID(N'Production.vProductAndDescription');   
    GO  
  
    ```  
  
#### <a name="to-view-the-objects-on-which-a-table-depends"></a>Per visualizzare gli oggetti dai quali dipende una tabella.  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Nell'esempio seguente restituire gli oggetti che dipendono dalla tabella `Production.Product`. Copiare e incollare l'esempio seguente nella finestra delle query e fare clic su **Esegui**.  
  
    ```  
    USE AdventureWorks2012;   
    GO  
    SELECT * FROM sys.sql_expression_dependencies  
    WHERE referenced_id = OBJECT_ID(N'Production.Product');   
    GO  
  
    ```  
  
 Per alte informazioni, vedere [Sys. sql_expression_dependencies &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql)  
  
  
