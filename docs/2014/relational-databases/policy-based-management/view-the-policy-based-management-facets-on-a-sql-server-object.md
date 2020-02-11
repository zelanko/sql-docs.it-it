---
title: Visualizzare i facet della gestione basata su criteri in un oggetto di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Policy-Based Management, view facets
ms.assetid: 5f423b9f-a6c4-41a7-9d8d-8f4926ce1fb4
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: cb2a08d874dd022fdad3646ea263d34dd65b9739
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62677031"
---
# <a name="view-the-policy-based-management-facets-on-a-sql-server-object"></a>Visualizzare i facet della gestione basata su criteri in un oggetto di SQL Server
  In questo argomento verrà descritto come visualizzare tutti i facet della gestione basata su criteri applicati a un oggetto specifico di SQL Server in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **Contenuto dell'articolo**  
  
-   **Prima di iniziare:**  
  
     [Sicurezza](#Security)  
  
-   **Per visualizzare tutti i facet in un oggetto tramite:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È necessaria l'appartenenza al ruolo PolicyAdministratorRole nel database msdb.  
  
##  <a name="SSMSProcedure"></a> Con SQL Server Management Studio  
  
#### <a name="to-view-all-of-the-facets-in-an-object"></a>Per visualizzare tutti i facet in un oggetto  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse su un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], su un oggetto istanza, su un database o su un oggetto di database, quindi scegliere **Facet**.  
  
2.  Nella finestra di dialogo **Visualizza facet -** _nome_oggetto_ selezionare un facet nell'elenco **Facet** per visualizzarne le proprietà. Per ulteriori informazioni sulle opzioni disponibili in questa finestra di dialogo, vedere [View Facets Dialog Box](view-facets-dialog-box.md).  
  
3.  Al termine, fare clic su **OK**.  
  
  
