---
title: Risolvere i problemi relativi a un'installazione di PowerPivot per SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 97bc2ce7-af04-4372-ad79-c96b8c3417ab
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: f70af740fb3fe8310a5306368c1bf48c6f357419
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "71951997"
---
# <a name="troubleshoot-a-powerpivot-for-sharepoint-installation"></a>Risoluzione dei problemi di un'installazione di PowerPivot per SharePoint
  Se vengono generati errori anziché le pagine e le caratteristiche previste, effettuare le operazioni riportate di seguito.  
  
-   Esaminare le note sulla versione di SharePoint e di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] per ottenere soluzioni alternative a problemi di installazione noti. Le note sulla versione vengono fornite con il supporto di installazione oppure sono disponibili nel sito Microsoft da cui si scarica il software.  
  
    -   [Note sulla versione di SQL Server 2014](https://technet.microsoft.com/library/dn169381\(v=sql.15\).aspx).  
  
-   Vedere l'argomento di Wiki di TechNet relativo alla [risoluzione dei problemi nelle installazioni di PowerPivot (e altri componenti aggiuntivi)](https://social.technet.microsoft.com/wiki/contents/articles/13737.troubleshooting-installations-of-powerpivot-and-other-add-ins.aspx).  
  
## <a name="issues"></a>Problemi  
  
### <a name="powerpivot-gallery-thumbnail-images-show-as-a-red-x"></a>Le immagini di anteprima per Raccolta PowerPivot sono visualizzate come una X rossa.  
 Una delle cause possibile potrebbe essere che **Integrazione della funzionalità di PowerPivot per le raccolte siti** non è attiva. Completare le operazioni seguenti:  
  
1.  Nella libreria della raccolta PowerPivot fare clic su **Impostazioni sito** dall'icona dell'ingranaggio ![impostazioni di SharePoint](https://docs.microsoft.com/analysis-services/analysis-services/media/as-sharepoint2013-settings-gear.gif "Impostazioni di SharePoint") o dall'elenco **Home** .  
  
2.  Nella sezione **Amministrazione raccolta siti** fare clic su **Funzionalità raccolta siti**.  
  
3.  Fare clic su **funzionalità raccolta siti**.  
  
4.  Verificare che **Integrazione delle funzionalità di PowerPivot per le raccolte siti** sia **Attiva**.  
  
 Per ulteriori cause di questo problema, vedere la pagina [relativa alle icone rosse per le icone della raccolta PowerPivot](https://support.microsoft.com/kb/2361559) https://support.microsoft.com/kb/2361559).  
  
  
