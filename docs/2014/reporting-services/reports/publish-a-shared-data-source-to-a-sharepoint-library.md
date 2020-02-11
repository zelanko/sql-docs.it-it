---
title: Pubblicare un'origine dati condivisa in una raccolta di SharePoint | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- data sources [Reporting Services], publishing to a SharePoint library
- SharePoint integration [Reporting Services], publishing to a library
- publishing reports [Reporting Services], to a SharePoint library
ms.assetid: 966ed425-3ce2-4e76-8237-3c1c977954ae
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2866b0b8a72e48dbb6c93b37b2a1a83e20e12821
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66102536"
---
# <a name="publish-a-shared-data-source-to-a-sharepoint-library"></a>Pubblicare un'origine dati condivisa in una raccolta di SharePoint
  Per pubblicare un'origine dati condivisa in un server di report eseguito in modalità integrata SharePoint, è necessario impostare le proprietà del progetto report in Progettazione report. Nelle proprietà del progetto tutti i riferimenti a server, report e origini dati condivise devono essere URL completi.  
  
 È necessario disporre dell'autorizzazione **Membro** o **Proprietario** il sito di SharePoint. Per altre informazioni, vedere [Esempi di URL per elementi di report pubblicati in un server di report in modalità SharePoint &#40;SSRS&#41;](../tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md).  
  
### <a name="to-publish-a-shared-data-source-to-a-sharepoint-site"></a>Per pubblicare un'origine dati condivisa in un sito di SharePoint  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire un progetto del server di report esistente o nuovo.  
  
2.  Scegliere **Proprietà** dal menu **Progetto**. Verrà visualizzata la finestra di dialogo _\<Pagine delle proprietà_ **del progetto**.  
  
3.  Nella casella **Configurazione** scegliere quella da utilizzare per la pubblicazione in un sito di SharePoint.  
  
4.  Se si desidera pubblicare le origini dati condivise nel progetto e sovrascrivere origini dati condivise pubblicate in precedenza, impostare **OverwriteDataSources** su **True**.  
  
5.  (Facoltativo) Per **TargetDataSourceFolder**, digitare un URL a una raccolta di SharePoint oppure a una cartella della raccolta, Ad esempio, *http://TestServer/TestSite/Documents/DataSources*.  
  
     Se non si specifica alcun valore, verrà utilizzato il valore **TargetReportFolder** .  
  
6.  Per **TargetReportFolder**, digitare l'URL di una raccolta o di una cartella della raccolta, ad esempio http:*//TestServer/TestSite/Documents/Reports*.  
  
7.  Per **TargetServerURL**, digitare l'URL di un sito principale o secondario di SharePoint. Se non si specifica un sito, verrà utilizzato il sito principale predefinito, Ad esempio, http://*nomeserver*, http://*nomeserver*/*sito*o http://*nomeserver*/*sito*/*sitosecondario*.  
  
8.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
9. In Esplora soluzioni fare clic con il pulsante destro del mouse sull'origine dati condivisa da pubblicare e quindi scegliere **Distribuisci**. L'origine dei dati verrà pubblicata nel percorso specificato in **TargetDataSourceFolder**. Gli eventuali errori di distribuzioni verranno visualizzati nella finestra di output.  
  
    > [!NOTE]  
    >  Dopo la pubblicazione di un'origine dati condivisa in un sito di SharePoint, l'estensione del file viene cambiata in rsds. È possibile modificare e gestire direttamente un'origine dati condivisa nel sito di SharePoint. Per altre informazioni, vedere [Creare e gestire origini dati condivise &#40;Reporting Services in modalità integrata SharePoint&#41;](../create-manage-shared-data-sources-reporting-services-sharepoint-integrated-mode.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Pubblicare un report in una raccolta di SharePoint](publish-a-report-to-a-sharepoint-library.md)   
 [Esempi di URL per elementi di report pubblicati in un server di report in modalità SharePoint &#40;SSRS&#41;](../tools/url-examples-for-items-on-a-report-server-sharepoint-mode.md)   
 [Finestra di dialogo Pagine delle proprietà del progetto](../tools/project-property-pages-dialog-box.md)   
 [Impostare le proprietà di distribuzione &#40;Reporting Services&#41;](../tools/set-deployment-properties-reporting-services.md)   
 [Pubblicazione dei report in un server di report](publishing-reports-to-a-report-server.md)   
 [Usare una connessione Office Data Connection &#40;.odc&#41; ai report &#40;Reporting Services in modalità integrata SharePoint&#41;](../report-data/use-an-office-data-connection-odc-with-reports.md)  
  
  
