---
title: Convertire origini dati (Generatore report) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-data
ms.topic: conceptual
helpviewer_keywords:
- data sources [Reporting Services], embedded
- data sources [Reporting Services], shared
ms.assetid: 0e099c7e-8c03-43eb-9ea3-76e52d9ebbe3
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 05aee467c3e69c115bedfa498a546a4e1664ba71
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "77081752"
---
# <a name="convert-data-sources-report-builder-and-ssrs"></a>Conversione di origini dati (Generatore report e SSRS)
  Ogni origine dati nel riquadro dei dati del report è incorporata e specifica del report oppure è condivisa. In Generatore report un'origine dati condivisa punta a un'origine dati condivisa pubblicata in un server di report o in un sito di SharePoint. In Progettazione report un'origine dati condivisa punta a un'origine dati condivisa nella cartella **Origini dati condivise** di Esplora soluzioni.  
  
 Per altre informazioni sulle differenze tra origini dati incorporate e origini dati condivise, vedere [Connessioni dati o origini dati condivise e incorporate &#40;Generatore report e SSRS&#41;](https://msdn.microsoft.com/library/f417782c-b85a-4c4d-8a40-839176daba56).  
  
 Per altre informazioni sulla creazione di un'origine dati condivisa, vedere [Creare un'origine dati incorporata o condivisa &#40;SSRS&#41;](https://msdn.microsoft.com/library/b111a8d0-a60d-4c8b-b00a-51644b19c34b).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="report-designer"></a>Progettazione report  
  
#### <a name="to-convert-a-data-source-from-embedded-to-shared"></a>Per convertire un'origine dati da incorporata a condivisa  
  
-   Nel riquadro dei dati del report fare clic con il pulsante destro del mouse sull'origine dati e quindi scegliere **Converti in origine dati condivisa**.  
  
    > [!NOTE]  
    >  Se il riquadro dei dati del report non è visualizzato, scegliere **Dati report** dal menu **Visualizza**. Se il riquadro è visualizzato come una finestra mobile, è possibile ancorarlo. Per altre informazioni, vedere [Ancorare il riquadro dei dati del report in Progettazione report &#40;SSRS&#41;](../../reporting-services/tools/dock-the-report-data-pane-in-report-designer-ssrs.md).  
  
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
 [Gestire origini dati dei report](../../reporting-services/report-data/manage-report-data-sources.md)   
 [Creare stringhe di connessione dati - Generatore report e SSRS](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
  
