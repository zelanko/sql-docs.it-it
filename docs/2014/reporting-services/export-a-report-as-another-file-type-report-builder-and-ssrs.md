---
title: Esportare un Report come tipo di un altro File (Generatore Report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: b577568b-ecbd-44c3-be88-31dab6fc38a2
author: maggiesmsft
ms.author: maghan
manager: kfile
ms.openlocfilehash: e1f048a91f8e20255050772f1503e6dfa387954b
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56017352"
---
# <a name="export-a-report-as-another-file-type-report-builder-and-ssrs"></a>Esportare un report in un altro tipo di file (Generatore report e SSRS)
  È possibile eseguire il rendering di un report in un altro formato di file, ad esempio CSV, immagine, PDF, [!INCLUDE[ofprword](../includes/ofprword-md.md)]o [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)], durante la visualizzazione in anteprima in Generatore report o Progettazione report oppure durante la visualizzazione nel server di report. Il rendering del report in un formato specifico risulta utile quando si desidera salvare immediatamente il report in un altro tipo di file senza pubblicarlo sul server di report oppure quando si desidera visualizzare l'aspetto che avrà il report quando verrà recapitato ai lettori in un formato specifico. Il rendering del report nel server di report risulta utile quando si impostano sottoscrizioni o si recapitano i report tramite posta elettronica oppure se si desidera salvare un report disponibile nel server di report. Per altre informazioni, vedere [Sottoscrizioni e recapito &#40;Reporting Services&#41;](subscriptions/subscriptions-and-delivery-reporting-services.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
### <a name="to-export-a-report-as-another-file-type-in-report-builder"></a>Per esportare un report in un altro tipo di file in Generatore report  
  
1.  Visualizzare l'anteprima del report.  
  
2.  Sulla barra multifunzione fare clic su **Esporta**.  
  
3.  Selezionare il formato che si desidera usare.  
  
     Verrà visualizzata la finestra di dialogo **Salva con nome** . Per impostazione predefinita, il nome del file è quello del report esportato. Se lo si desidera, tale nome può essere modificato.  
  
4.  Passare al percorso in cui è stato salvato il report esportato e aprirlo.  
  
> [!NOTE]  
>  Se il programma non consente di aprire il report nel formato scelto dal momento che non si dispone di un'applicazione associata a questo tipo di file, verrà richiesto di salvare il report esportato o di trovare un programma online che ne permette l'apertura.  
  
### <a name="to-export-a-report-as-another-file-type-in-report-manager"></a>Per esportare un report in un altro tipo di file in Gestione report  
  
1.  Dalla pagina Gestione report **Home**, accedere al report che si desidera esportare.  
  
2.  Fare clic sul report.  
  
     Il report verrà generato.  
  
3.  Sulla barra degli strumenti del Visualizzatore report fare clic sulla freccia a discesa **Selezionare un formato** .  
  
4.  Selezionare il formato che si desidera usare.  
  
5.  Fare clic su **Esporta**.  
  
     Verrà visualizzato un messaggio in cui si chiede se si desidera aprire o salvare il file.  
  
6.  Per visualizzare il report nel formato di esportazione selezionato, fare clic su **Apri**.  
  
     \- - oppure -  
  
     Per salvare immediatamente il report nel formato di esportazione selezionato, fare clic su **Salva**.  
  
     Il report verrà visualizzato o salvato con l'applicazione associata al formato scelto. Se si fa clic su **Salva**, verrà richiesto di specificare un percorso in cui salvare il report.  
  
     **Nota** Se non è possibile aprire il report nel formato selezionato perché non è stato associato alcun programma a questo tipo di file, verrà richiesto di salvare il report esportato o di individuare un programma online con cui aprirlo.  
  
### <a name="to-export-a-report-as-another-file-type-in-a-sharepoint-library"></a>Per esportare un report in un altro tipo di file in una raccolta di SharePoint.  
  
1.  Visualizzare l'anteprima del report.  
  
2.  Nella barra degli strumenti, fare clic su **Azioni**, scegliere **Esporta**, quindi selezionare il formato che si desidera usare.  
  
     Viene visualizzata la finestra di dialogo **Download file** .  
  
3.  Per visualizzare il report nel formato di esportazione selezionato, fare clic su **Apri**.  
  
     \- - oppure -  
  
     Per salvare immediatamente il report nel formato di esportazione selezionato, fare clic su **Salva**.  
  
     Il report verrà visualizzato o salvato con l'applicazione associata al formato scelto. Se si fa clic su **Salva**, verrà richiesto di specificare un percorso in cui salvare il report.  
  
     Se lo si desidera, modificare il nome del file del report esportato.  
  
     **Nota** Se non è possibile aprire il report nel formato selezionato perché non è stato associato alcun programma a questo tipo di file, verrà richiesto di salvare il report esportato o di individuare un programma online con cui aprirlo.  
  
## <a name="see-also"></a>Vedere anche  
 [Esportazione di report &#40;Report e SSRS&#41;](report-builder/export-reports-report-builder-and-ssrs.md)   
 [Paginazione in Reporting Services &#40;Generatore report e SSRS&#41;](report-design/pagination-in-reporting-services-report-builder-and-ssrs.md)   
 [Funzionalità interattiva per estensioni di Rendering del Report diversi &#40;Report e SSRS&#41;](report-builder/interactive-functionality-different-report-rendering-extensions.md)  
  
  
