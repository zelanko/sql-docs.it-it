---
title: Pubblicare i report | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], publishing
- publishing reports [Reporting Services]
ms.assetid: ef5a514e-e818-4041-a8b0-15835f9a046b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 86ab056f18e69b0b264525377efb0d257ebc2b95
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66108024"
---
# <a name="publish-reports"></a>Pubblicazione di report
  In[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]è possibile pubblicare un solo report oppure pubblicare tutti i report e le origini dati condivise di un progetto server di report in un server di report distribuendo il progetto. Prima di pubblicare un report è necessario specificare l'URL del server di report di destinazione. Per altre informazioni, vedere [Impostare le proprietà di distribuzione &#40;Reporting Services&#41;](tools/set-deployment-properties-reporting-services.md).  
  
 È possibile utilizzare la versione [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] di [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] per aprire, modificare, visualizzare in anteprima, salvare e pubblicare i report di [!INCLUDE[ssRSversion2005](../includes/ssrsversion2005-md.md)] e di [!INCLUDE[ssRSversion10](../includes/ssrsversion10-md.md)] . Per altre informazioni, vedere [Distribuzione e supporto della versione in SQL Server Data Tools &#40;SSRS&#41;](tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md).  
  
### <a name="to-publish-all-reports-in-a-project"></a>Per pubblicare tutti i report di un progetto  
  
-   Nel menu **Compilazione** fare clic su **Distribuisci \<nome progetto report>**. In alternativa, in Esplora soluzioni fare clic con il pulsante destro del mouse sul progetto report e scegliere **Distribuisci**. È possibile visualizzare lo stato del processo di pubblicazione nella finestra Output.  
  
    > [!NOTE]  
    >  Quando si distribuisce un progetto server di report, vengono distribuite anche le origini dati condivise nel progetto report.  
  
### <a name="to-publish-a-single-report"></a>Per pubblicare un solo report  
  
-   In Esplora soluzioni fare clic con il pulsante destro del mouse sul report e scegliere **Distribuisci**. È possibile visualizzare lo stato del processo di pubblicazione nella finestra Output.  
  
    > [!NOTE]  
    >  Quando si pubblica un report, è necessario distribuire anche le origini dati condivise utilizzate dal report.  
  
## <a name="see-also"></a>Vedere anche  
 [Pubblicazione di origini dati e report](reports/publishing-data-sources-and-reports.md)   
 [Anteprima dei report](reports/previewing-reports.md)   
 [Pubblicazione dei report in un server di report](reports/publishing-reports-to-a-report-server.md)   
 [Ricerca, visualizzazione e gestione dei report &#40;Generatore report e SSRS&#41;](report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Esportazione di report &#40;Report e SSRS&#41;](report-builder/export-reports-report-builder-and-ssrs.md)  
  
  
