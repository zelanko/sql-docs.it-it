---
title: Risolvere i problemi relativi alle parti del report (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: d9fe1932-46e7-421b-a8a9-4c54d9576e94
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: df37de909461ace62edbbf3cfe9e7b9dd8448b56
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66099385"
---
# <a name="troubleshoot-report-parts-report-builder-and-ssrs"></a>Risoluzione dei problemi relativi alle parti del report (Generatore report e SSRS)
  Questi suggerimenti possono risultare utili durante l'utilizzo di parti del report.  
  
## <a name="why-do-my-co-worker-and-i-see-different-instances-of-the-same-report-part-when-we-search-for-it"></a>Visualizzazione di istanze diverse della stessa parte del report tra colleghi di lavoro durante la relativa ricerca  
 In un server di report o in un sito di SharePoint integrato con un server di report possono essere presenti più istanze di una sola parte di report, tutte dotate dello stesso identificatore univoco globale (GUID). Nell'elenco di risultati ricerca viene visualizzata solo l'istanza più recente. In alcuni casi, istanze diverse di una singola parte di report possono avere autorizzazioni differenti. Se un collega di lavoro dispone di autorizzazioni sul server diverse da un altro collega, quest'ultimo non visualizzerà la stessa istanza. Si supponga, ad esempio, che più copie di una parte di report, tutte con lo stesso GUID, vengano salvate in cartelle diverse su un server di report in modalità integrata SharePoint. Se le cartelle dispongono di autorizzazioni diverse, anche le parti di report in esse contenute disporranno di autorizzazioni diverse.  
  
 Per conoscere le autorizzazioni di cui dispongono i colleghi, chiedere all'amministratore del server di report.  
  
## <a name="when-i-search-for-report-parts-that-i-uploaded-to-a-sharepoint-server-i-do-not-see-them-why-not"></a>Impossibilità di visualizzare parti di report caricate in un server SharePoint in seguito alla Perché?  
 È possibile che le parti di report caricate manualmente in una raccolta documenti di SharePoint, anziché pubblicate tramite Generatore report, non vengano visualizzate nella relativa raccolta. Potrebbe essere necessario sincronizzare il server di report utilizzato per la ricerca nella raccolta con il contenuto della raccolta documenti di SharePoint. Per ulteriori informazioni, vedere [attivare la funzionalità Sincronizzazione file server di report in Amministrazione centrale SharePoint](../../2014/reporting-services/activate-report-server-file-sync-feature-sharepoint-central-administration.md) nella [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [documentazione online](https://go.microsoft.com/fwlink/?LinkId=154888) di MSDN.Microsoft.com.  
  
## <a name="why-cant-others-see-the-image-in-their-reports"></a>Impossibilità di visualizzare l'immagine nei report di altri utenti  
 Se si pubblica una parte di report rappresentata da un collegamento a un file di immagine, tale parte di report costituirà in effetti un semplice collegamento. Se altri utenti non riescono a visualizzare l'immagine quando aggiungono la parte di report immagine nei relativi report, potrebbero non disporre delle autorizzazioni per l'immagine a cui ci si sta collegando.  
  
 Esistono diverse soluzioni possibili:  
  
-   Creare una parte di report con il file di immagine, anziché con il collegamento al file di immagine.  
  
-   Spostare il file di immagine in un percorso per il quale gli altri utenti dispongono delle autorizzazioni.  
  
-   Chiedere all'amministratore del server di report di modificare le autorizzazioni.  
  
## <a name="why-do-i-get-a-circular-reference-error-message-when-i-try-to-publish-my-report-part"></a>Visualizzazione di un messaggio di errore relativo a un "riferimento circolare" durante il tentativo di pubblicazione della parte di report  
 Se gli elementi del report presentano un riferimento circolare, non sarà possibile pubblicarli come parti di report. Un elemento del report punta, ad esempio, a un set di dati che a sua volta punta a un parametro. Il parametro, infine, punta nuovamente al set di dati. Sarà necessario anzitutto eliminare uno dei riferimenti prima di poter pubblicare la parte di report.  
  
## <a name="see-also"></a>Vedere anche  
 [Parti del report &#40;Generatore report e SSRS&#41;](report-parts-report-builder-and-ssrs.md)  
  
  
