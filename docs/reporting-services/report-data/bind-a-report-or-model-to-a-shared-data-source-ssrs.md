---
title: Associare un report a un'origine dati condivisa | Microsoft Docs
ms.date: 05/24/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- shared data sources [Reporting Services]
- data sources [Reporting Services], shared
ms.assetid: 23cc15f2-2883-48e2-bc6c-fa0ab61a2e21
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c5aa5e504c8434d3634b903c08b6a03c0e62345c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "77081417"
---
# <a name="bind-a-report-to-a-shared-data-source-ssrs"></a>Associare un report a un'origine dati condivisa (SSRS)
  In alcune situazioni, ad esempio quando si sposta un report da un server di test a uno di produzione, può essere necessario salvare il file nel computer locale e quindi caricarlo in un altro server di report. Quando si carica il report nel nuovo server è necessario riassociarlo a un'origine dati condivisa archiviata nel nuovo server di report. Se il report non viene riassociato non funzionerà correttamente quando vi si accede dal nuovo server di report.  
  
> [!IMPORTANT]  
>  Per poter riassociare un report a un'origine dati condivisa, quest'ultima deve esistere già nel server di report o nella raccolta di SharePoint. Per altre informazioni sulle origini dati, vedere [Creare, modificare ed eliminare origini dati condivise &#40;SSRS&#41;](../../reporting-services/report-data/create-modify-and-delete-shared-data-sources-ssrs.md).  
  
## <a name="to-bind-a-report-to-a-shared-data-source-on-a-report-server-running-in-native-mode"></a>Per associare un report a un'origine dati condivisa in un server di report in esecuzione in modalità nativa  
  
1.  Nel portale Web fare clic sui puntini di sospensione (...) nell'angolo superiore destro del riquadro di report > **Gestisci**.  

2.  Fare clic su **Origini dati**.  
  
3.  Fare clic su **Origine dati condivisa** e trovare l'origine dati a cui si vuole associare il report.  
  
4.  Selezionare l'origine dati e fare clic su **Salva**.  
  
5.  Fare clic su **Apply**.  
  
     Il report viene associato all'origine dati selezionata.  
  
## <a name="to-bind-a-report-to-a-shared-data-source-on-a-report-server-running-in-sharepoint-integrated-mode"></a>Per associare un report a un'origine dati condivisa in un server di report in esecuzione in modalità integrata SharePoint  
  
1.  Se la raccolta non è già aperta, fare clic sul suo nome sulla barra di avvio veloce. Se il nome della raccolta non è visualizzato, fare clic su **Visualizza tutto il contenuto del sito**e quindi sul nome della raccolta desiderata.  
  
2.  Selezionare il report e fare clic sulla freccia verso il basso.  
  
3.  Fare clic su **Gestisci origini dati**.  
  
4.  Fare clic su **dataSource1**.  
  
5.  Nell'area **Tipo di connessione** verificare che **Origine dati condivisa** sia selezionata.  
  
6.  Nell'area **Collegamento origine dati** fare clic sul pulsante con i puntini di sospensione (...).  
  
7.  Individuare l'origine dei dati da utilizzare.  
  
8.  Selezionare l'origine dati e fare clic su **OK**.  
  
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
10. Fare clic su **Close**.  
  
## <a name="see-also"></a>Vedere anche  
 [Caricare documenti in una raccolta di SharePoint &#40;Reporting Services in modalità SharePoint&#41;](../../reporting-services/report-server-sharepoint/upload-documents-to-a-sharepoint-library-reporting-services-in-sharepoint-mode.md)   
 [Creare e gestire origini dati condivise &#40;Reporting Services in modalità integrata SharePoint&#41;](https://msdn.microsoft.com/library/2d3428e4-a810-4e66-a287-ff18e57fad76)   
 [Creare stringhe di connessione dati - Generatore report e SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)   
 [Origini dei dati supportate da Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md)  
  
  
