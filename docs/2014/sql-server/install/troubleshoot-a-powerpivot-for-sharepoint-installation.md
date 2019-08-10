---
title: Risolvere i problemi relativi a un'installazione di PowerPivot per SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 97bc2ce7-af04-4372-ad79-c96b8c3417ab
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 797405386e8a6c0b9e62328699f3a73a6d845313
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/09/2019
ms.locfileid: "68892440"
---
# <a name="troubleshoot-a-powerpivot-for-sharepoint-installation"></a>Risoluzione dei problemi di un'installazione di PowerPivot per SharePoint
  Se vengono generati errori anziché le pagine e le caratteristiche previste, effettuare le operazioni riportate di seguito.  
  
-   Esaminare le note sulla versione di SharePoint e di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] per ottenere soluzioni alternative a problemi di installazione noti. Le note sulla versione vengono fornite con il supporto di installazione oppure sono disponibili nel sito Microsoft da cui si scarica il software.  
  
    -   [Note sulla versione di SQL Server 2014](https://technet.microsoft.com/library/dn169381\(v=sql.15\).aspx).  
  
-   Vedere l'argomento di Wiki di TechNet relativo alla [risoluzione dei problemi nelle installazioni di PowerPivot (e altri componenti aggiuntivi)](https://social.technet.microsoft.com/wiki/contents/articles/13737.troubleshooting-installations-of-powerpivot-and-other-add-ins.aspx).  
  
## <a name="issues"></a>Problemi  
  
### <a name="powerpivot-gallery-thumbnail-images-show-as-a-red-x"></a>Le immagini di anteprima per Raccolta PowerPivot sono visualizzate come una X rossa.  
 Una delle cause possibile potrebbe essere che **Integrazione della funzionalità di PowerPivot per le raccolte siti** non è attiva. Completare la procedura seguente:  
  
1.  Nella libreria della raccolta PowerPivot fare clic su **Impostazioni sito** dall'icona a forma di ingranaggio ![SharePoint]impostazioni di(https://docs.microsoft.com/analysis-services/analysis-services/media/as-sharepoint2013-settings-gear.gif "SharePoint") o l'elenco **Home** .  
  
2.  Nella sezione **Amministrazione raccolta siti** fare clic su **Funzionalità raccolta siti**.  
  
3.  Fare clic su **Funzionalità raccolta siti**.  
  
4.  Verificare che **Integrazione delle funzionalità di PowerPivot per le raccolte siti** sia **Attiva**.  
  
 Per ulteriori cause di questo problema, vedere la pagina [relativa alle icone rosse per](https://support.microsoft.com/kb/2361559) le icone https://support.microsoft.com/kb/2361559) della raccolta PowerPivot.  
  
  
