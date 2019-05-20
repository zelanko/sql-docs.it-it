---
title: Pubblicare un report in una raccolta di SharePoint | Microsoft Docs
ms.date: 03/07/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reports
ms.topic: conceptual
helpviewer_keywords:
- deploying [Reporting Services], reports in SharePoint integrated mode
- SharePoint integration [Reporting Services], publishing to a library
- publishing reports [Reporting Services], to a SharePoint library
ms.assetid: 3f6dfc28-50d8-4231-bd25-871b5f77cce6
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 1b10c9dbfa67a632ce007c1406f8b806a03475b4
ms.sourcegitcommit: dda9a1a7682ade466b8d4f0ca56f3a9ecc1ef44e
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 05/14/2019
ms.locfileid: "65571043"
---
# <a name="publish-a-report-to-a-sharepoint-library"></a>Pubblicare un report in una raccolta di SharePoint
  Per pubblicare un report in un sito di SharePoint configurato per l'integrazione con SharePoint, è necessario impostare le proprietà del progetto in Progettazione report. Nelle proprietà del progetto tutti i riferimenti a server, report e origini dati condivise devono essere URL completi. Nella definizione di un report tutti i riferimenti a sottoreport, report drill-through e risorse quali immagini basate su Web devono essere rappresentati da URL completi.  
  
 Per impostare le proprietà del progetto, è necessario disporre dell'autorizzazione **Membro** o **Proprietario** per il sito di SharePoint. Per altre informazioni, vedere [Esempi di URL per elementi di report pubblicati in un server di report in modalità SharePoint &#40;SSRS&#41;](../../reporting-services/tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md).  
  
### <a name="to-publish-a-report-to-a-sharepoint-site"></a>Per pubblicare un report in un sito di SharePoint  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire un progetto del server di report esistente o nuovo.  
  
2.  Scegliere **Proprietà** dal menu **Progetto**. Verrà visualizzata la finestra di dialogo _\<Pagine delle proprietà_ **del progetto**.  
  
3.  Nell'elenco **Configurazione** selezionare il nome di una configurazione della build della soluzione da usare per compilare e pubblicare il report. La configurazione corrente viene elencata come **Attiva**(*\<configurazione>*).  
  
4.  Se si desidera pubblicare le origini dati condivise nel progetto e sovrascrivere origini dati condivise pubblicate in precedenza, impostare **OverwriteDataSources** su **True**.  
  
5.  (Facoltativo) Per **TargetDataSourceFolder**digitare l'URL di una raccolta o della cartella di una raccolta di SharePoint, ad esempio `https://TestServer/TestSite/Documents/DataSources`).  
  
     Se non si specifica alcun valore, verrà utilizzato il valore **TargetReportFolder** .  
  
6.  Per **TargetReportFolder**digitare l'URL di una raccolta o di una cartella della raccolta, ad esempio `https://TestServer/TestSite/Documents/Reports`).  
  
7.  Per **TargetServerURL**, digitare l'URL di un sito principale o secondario di SharePoint. Se non si specifica un sito, verrà usato il sito principale predefinito, ad esempio `https://servername`, `https://servername/site`o `https://servername/site/subsite`).  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
9. In Esplora soluzioni fare clic con il pulsante destro del mouse sul report da pubblicare, quindi scegliere **Distribuisci**. Il report verrà pubblicato nel percorso specificato in **TargetReportFolder**. Gli eventuali errori di distribuzioni verranno visualizzati nella finestra di output.  
  
## <a name="see-also"></a>Vedere anche  
 [Finestra di dialogo Pagine delle proprietà del progetto](../../reporting-services/tools/project-property-pages-dialog-box.md)   
 [Impostare le proprietà di distribuzione &#40;Reporting Services&#41;](../../reporting-services/tools/set-deployment-properties-reporting-services.md)   
 [Pubblicazione dei report in un server di report](../../reporting-services/reports/publishing-reports-to-a-report-server.md)   
 [Esempi di URL per elementi di report pubblicati in un server di report in modalità SharePoint &#40;SSRS&#41;](../../reporting-services/tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md)   
 [Usare una connessione Office Data Connection &#40;.odc&#41; ai report &#40;Reporting Services in modalità integrata SharePoint&#41;](../../reporting-services/report-data/use-an-office-data-connection-odc-with-reports.md)  
  
  
