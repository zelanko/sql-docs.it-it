---
title: Incorporare un'immagine in un report (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.embeddedimages.f1
- "10060"
ms.assetid: aed77345-5eeb-41f0-96c9-db6b4a11ec6f
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b1541073379aa27c932fcadf7558de7d34c57e8d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62824348"
---
# <a name="embed-an-image-in-a-report-report-builder-and-ssrs"></a>Incorporare un'immagine in un report (Generatore report e SSRS)
  Un report può includere un'immagine incorporata. L'incorporamento di un'immagine assicura che l'immagine sia sempre disponibile per il report, ma può influire sulle dimensioni della definizione del report, ovvero il file che definisce il report. Le immagini incorporate in un report sono elencate nel riquadro dei dati del report.  
  
 È necessario incorporare un'immagine nella definizione del report prima di aggiungerla all'area di progettazione. Per altre informazioni, vedere [Aggiungere un'immagine di sfondo &#40;Generatore report e SSRS&#41;](add-a-background-image-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-embed-an-image-in-a-report"></a>Per incorporare un'immagine in un report  
  
1.  Nella visualizzazione di progettazione report fare clic su **Immagine** nella scheda **Inserisci**.  
  
2.  Nell'area di progettazione fare clic su una casella, quindi trascinarla fino a raggiungere le dimensioni desiderate per l'immagine.  
  
3.  Nella pagina **Generale** della finestra di dialogo **Proprietà immagine** digitare un nome nella casella di testo **Nome** o accettare il nome predefinito.  
  
4.  (Facoltativo) Nella casella di testo **Descrizione comando** digitare il testo da visualizzare quando il puntatore del mouse viene posizionato sull'immagine nel report visualizzabile.  
  
5.  In **Selezionare l'origine dell'immagine**selezionare **Incorporata**.  
  
6.  Fare clic sul pulsante **Importa** accanto alla casella di testo **Utilizzare questa immagine** .  
  
7.  In **Tipo file**selezionare il tipo di file di immagine, passare al file e quindi fare clic su **Apri**.  
  
8.  Nella finestra di dialogo **Proprietà immagine** scegliere **OK**.  
  
     L'immagine viene visualizzata nella casella disegnata nell'area di progettazione mentre il file viene visualizzato sotto la cartella Immagini nel riquadro dei dati del report.  
  
    > [!NOTE]  
    >  Il tipo MIME, ad esempio bmp, viene derivato automaticamente al momento dell'importazione dell'immagine. Per modificare il tipo MIME, vedere la procedura seguente.  
  
### <a name="optional-to-change-the-mime-type-of-an-imported-image"></a>(Facoltativo) Per modificare il tipo MIME di un'immagine importata  
  
1.  Aprire il report in visualizzazione Progettazione.  
  
2.  Selezionare l'immagine nell'area di progettazione. Nel riquadro **Proprietà** verranno visualizzate le proprietà dell'immagine.  
  
    > [!NOTE]  
    >  Se il riquadro Proprietà non è visualizzato, fare clic su **Proprietà** nella scheda **Visualizza**.  
  
3.  Fare clic nella casella di testo accanto alla proprietà **MIMEType** e selezionare un nuovo tipo MIME nell'elenco a discesa.  
  
## <a name="see-also"></a>Vedere anche  
 [Immagini &#40;Generatore report e SSRS&#41;](images-report-builder-and-ssrs.md)   
 [Aggiungere un'immagine di sfondo &#40;Generatore report e SSRS&#41;](add-a-data-bound-image-report-builder-and-ssrs.md)   
 [Finestra di dialogo Proprietà immagine, Generale &#40;Generatore report e SSRS&#41;](../image-properties-dialog-box-general-report-builder-and-ssrs.md)  
  
  
