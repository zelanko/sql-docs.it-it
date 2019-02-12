---
title: Convertire un'origine dati da incorporata a condivisa (Generatore Report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- data sources [Reporting Services], embedded
- data sources [Reporting Services], shared
ms.assetid: 0e099c7e-8c03-43eb-9ea3-76e52d9ebbe3
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: bc8c9b65c70fef86887ed80a8049b4e930188ffe
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56038392"
---
# <a name="convert-a-data-source-from-embedded-to-shared-report-builder-and-ssrs"></a>Convertire un'origine dati da incorporata a condivisa (Generatore report e SSRS)
  Ogni origine dati nel riquadro dei dati del report è incorporata e specifica del report oppure è condivisa. In Generatore report un'origine dati condivisa punta a un'origine dati condivisa pubblicata in un server di report o in un sito di SharePoint. In Progettazione report un'origine dati condivisa punta a un'origine dati condivisa nella cartella **Origini dati condivise** di Esplora soluzioni.  
  
 Per altre informazioni sulle differenze tra origini dati incorporate e origini dati condivise, vedere [Connessioni dati o origini dati condivise e incorporate &#40;Generatore report e SSRS&#41;](../embedded-and-shared-data-connections-or-data-sources-report-builder-and-ssrs.md).  
  
 Per altre informazioni sulla creazione di un'origine dati condivisa, vedere [Creare un'origine dati incorporata o condivisa &#40;SSRS&#41;](../create-an-embedded-or-shared-data-source-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-designer"></a>Progettazione report  
  
#### <a name="to-convert-a-data-source-from-embedded-to-shared"></a>Per convertire un'origine dati da incorporata a condivisa  
  
-   Nel riquadro dei dati del report fare clic con il pulsante destro del mouse sull'origine dati e quindi scegliere **Converti in origine dati condivisa**.  
  
    > [!NOTE]  
    >  Se il riquadro dei dati del report non è visualizzato, scegliere **Dati report** dal menu **Visualizza**. Se il riquadro è visualizzato come una finestra mobile, è possibile ancorarlo. Per altre informazioni, vedere [Ancorare il riquadro dei dati del report in Progettazione report &#40;SSRS&#41;](../tools/dock-the-report-data-pane-in-report-designer-ssrs.md).  
  
     Nel riquadro dei dati del report, l'icona dell'origine dati viene modificata nell'icona dell'origine dati condivisa. In Esplora soluzioni un'origine dati condivisa con lo stesso nome viene visualizzata nella cartella **Origini dati condivise** .  
  
### <a name="to-convert-a-data-source-from-shared-to-embedded"></a>Per convertire un'origine dati da condivisa a incorporata  
  
-   Nel riquadro dei dati del report fare clic con il pulsante destro del mouse sull'origine dati, aprire la finestra di dialogo **Proprietà origine dati** e quindi fare clic su **Connessione incorporata**. Immettere le informazioni necessarie.  
  
     Nel riquadro dei dati del report, l'icona dell'origine dati viene modificata nell'icona dell'origine dati condivisa.  
  
## <a name="report-builder"></a>Generatore report  
  
#### <a name="to-convert-a-data-source-from-embedded-to-shared"></a>Per convertire un'origine dati da incorporata a condivisa  
  
-   Nel riquadro dei dati del report fare clic con il pulsante destro del mouse sull'origine dati per aprire la finestra di dialogo **Proprietà origine dati** e quindi fare clic su **Connessione incorporata**. Immettere le informazioni necessarie.  
  
     Nel riquadro dei dati del report, l'icona dell'origine dati viene modificata nell'icona dell'origine dati condivisa.  
  
#### <a name="to-convert-a-data-source-from-shared-to-embedded"></a>Per convertire un'origine dati da condivisa a incorporata  
  
-   Nel riquadro dei dati del report fare clic con il pulsante destro del mouse sull'origine dati, aprire la finestra di dialogo **Proprietà origine dati** e quindi fare clic su **Connessione incorporata**. Immettere le informazioni necessarie.  
  
     Nel riquadro dei dati del report, l'icona dell'origine dati viene modificata nell'icona dell'origine dati condivisa.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestire origini dati dei report](manage-report-data-sources.md)   
 [Connessioni dati, origini dati e stringhe di connessione in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)  
  
  
