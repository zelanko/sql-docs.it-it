---
title: Visualizzare o modificare le proprietà dei criteri della gestione basata su criteri | Microsoft Docs
ms.custom: ''
ms.date: 10/06/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, modify policies
- Policy-Based Management, view policies
ms.assetid: ba805504-5db5-4731-a8da-a0e89cb20c37
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: e1d7799abc3a930e72a9040c537e99fe7641a641
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52505897"
---
# <a name="view-or-modify-the-properties-of-a-policy-based-management-policy"></a>Visualizzare o modificare le proprietà dei criteri della gestione basata su criteri
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento verrà descritto come visualizzare o modificare le proprietà dei criteri della gestione basata su criteri in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È necessaria l'appartenenza al ruolo PolicyAdministratorRole nel database msdb.  
  
##  <a name="SSMSProcedure"></a> Utilizzo di SQL Server Management Studio  
  
#### <a name="to-view-the-properties-of-all-policies-on-an-object"></a>Per visualizzare le proprietà di tutti i criteri in un oggetto  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse su un server, un oggetto server, un database o un oggetto di database, scegliere **Criteri** , quindi fare clic su **Visualizza**. Per altre informazioni sulle opzioni disponibili nella finestra di dialogo **Visualizza criteri -***nome_oggetto*, vedere [Finestra di dialogo Visualizza criteri](../../relational-databases/policy-based-management/view-policies-dialog-box.md).  
  
2.  Al termine, fare clic su **Chiudi**.  
  
#### <a name="to-view-or-modify-a-specific-policys-properties"></a>Per visualizzare o modificare le proprietà di criteri specifici:  
  
1.  In **Esplora oggetti**fare clic sul segno più per espandere il server contenente i criteri della gestione basata su criteri da visualizzare o modificare.  
  
2.  Fare clic sul segno più per espandere la cartella **Gestione** .  
  
3.  Fare clic sul segno più per espandere la cartella **Gestione criteri**.  
  
4.  Fare clic sul segno più per espandere la cartella **Criteri** .  
  
5.  Fare clic con il pulsante destro del mouse sui criteri da visualizzare o modificare e selezionare **Proprietà**. Per altre informazioni sulle opzioni disponibili nella finestra di dialogo **Apri criteri -***nome_criteri*, vedere [Finestra di dialogo Crea nuovi criteri o Apri criteri, pagina Generale](../../relational-databases/policy-based-management/create-new-policy-or-open-policy-dialog-box-general-page.md) e [Finestra di dialogo Crea nuovi criteri o Apri criteri, pagina Descrizione](../../relational-databases/policy-based-management/create-new-policy-or-open-policy-dialog-box-description-page.md).  
  
6.  Al termine, fare clic su **OK**.  
  
##  <a name="TsqlProcedure"></a> Uso di Transact-SQL  
  
#### <a name="to-view-a-policys-properties"></a>Per visualizzare le proprietà dei criteri  
  
1.  In **Esplora oggetti**connettersi a un'istanza del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  Sulla barra Standard fare clic su **Nuova query**.  
  
3.  Copiare e incollare l'esempio seguente nella finestra delle query e fare clic su **Esegui**.  
  
    ```  
    USE msdb;  
    GO  
    SELECT name,  
       execution_mode,  
       description,  
       is_enabled,  
       job_id  
    FROM syspolicy_policies;  
    GO  
    ```  
  
 Per altre informazioni, vedere [syspolicy_policies &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syspolicy-policies-transact-sql.md).  
  
  
