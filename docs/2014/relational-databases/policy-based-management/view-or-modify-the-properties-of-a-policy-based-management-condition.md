---
title: Visualizzare o modificare le proprietà di una condizione della gestione basata su criteri | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, view policy conditions
- Policy-Based Management, modify policy conditions
ms.assetid: 890d7384-8444-4767-bb6f-f5debb155747
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 340423e23037ae401b1e5749fbed38b1822cfb41
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62677017"
---
# <a name="view-or-modify-the-properties-of-a-policy-based-management-condition"></a>Visualizzare o modificare le proprietà di una condizione della gestione basata su criteri
  In questo argomento verrà descritto come visualizzare o modificare le proprietà di una condizione della gestione basata su criteri in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **Contenuto dell'argomento**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per visualizzare o modificare le proprietà della condizione tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È necessaria l'appartenenza al ruolo PolicyAdministratorRole nel database msdb.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-view-or-modify-a-conditions-properties"></a>Per visualizzare o modificare le proprietà di una condizione  
  
1.  In **Esplora oggetti**fare clic sul segno più per espandere il server contenente la condizione da visualizzare o modificare.  
  
2.  Fare clic sul segno più per espandere la cartella **Gestione** .  
  
3.  Fare clic sul segno più per espandere la cartella **Gestione criteri**.  
  
4.  Fare clic sul segno più per espandere la cartella **Condizioni** .  
  
5.  Fare clic con il pulsante destro del mouse sulla condizione da visualizzare o modificare e scegliere **Proprietà**. Per altre informazioni sulle opzioni disponibili nella finestra di dialogo ***Apri condizione -** _nome_condizione_, vedere [Finestra di dialogo Crea nuova condizione o Apri condizione, pagina Generale](../../integration-services/general-page-of-integration-services-designers-options.md), [Finestra di dialogo Apri condizione, pagina Criteri dipendenti](open-condition-dialog-box-dependent-policies-page.md), [Finestra di dialogo Crea nuova condizione o Apri condizione, pagina Descrizione](create-new-condition-or-open-condition-dialog-box-description-page.md) e [Finestra di dialogo Modifica avanzata &#40;Condizione&#41;](advanced-edit-condition-dialog-box.md).  
  
6.  Al termine, fare clic su **OK**.  
  
##  <a name="TsqlProcedure"></a> Utilizzo di Transact-SQL  
  
#### <a name="to-view-a-conditions-properties"></a>Per visualizzare le proprietà di una condizione  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra Query, quindi fare clic su **Esegui**.  
  
    ```  
    USE msdb;  
    GO  
    SELECT name,  
       description,  
       facet,  
       expression,  
       is_name_condition,  
       obj_name  
    FROM syspolicy_conditions;  
    GO  
  
    ```  
  
 Per altre informazioni, vedere [syspolicy_conditions &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/syspolicy-conditions-transact-sql).  
  
  
