---
title: Aggiungere un'immagine di sfondo (Generatore report) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: c777fefb-8695-44a7-b5cd-a18c587583f2
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0c8b53c0e259a9a0c99ae1bd06cc9cab9cc14355
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "77081343"
---
# <a name="add-a-background-image-report-builder-and-ssrs"></a>Aggiungere un'immagine di sfondo (Generatore report e SSRS)
  È possibile aggiungere un'immagine di sfondo a un elemento del report, ad esempio un rettangolo, una casella di testo, un elenco, una matrice, una tabella e ad alcune parti di un grafico, o a una sezione del report, ad esempio un'intestazione di pagina, un piè di pagina o il corpo del report. È possibile definire un'immagine di sfondo per qualsiasi elemento selezionato nell'area di progettazione per il quale la proprietà **BackgroundImage** sia visualizzata nel riquadro Proprietà. Analogamente ad altre immagini, quella di sfondo può essere l'URL di un'immagine nel server di report, un'immagine da un campo del set di dati o un'immagine incorporata nella definizione del report. Per utilizzare un'immagine incorporata nel report, è necessario innanzitutto aggiungere l'immagine alla definizione del report prima di poterla aggiungere all'area di progettazione.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-embed-an-image-in-the-report-definition"></a>Per incorporare un'immagine nella definizione del report  
  
1.  Nel riquadro dei dati del report fare clic con il pulsante destro del mouse sul nodo **Immagini** , quindi scegliere **Aggiungi immagine**.  
  
    > [!NOTE]  
    >  Se il riquadro dei dati del report non è visualizzato, scegliere **Dati report** dal menu **Visualizza**.  
  
2.  Passare all'immagine da incorporare nella definizione del report, quindi fare clic su **OK**.  
  
### <a name="to-add-a-background-image"></a>Per aggiungere un'immagine di sfondo  
  
1.  Nella visualizzazione di progettazione report selezionare l'elemento del report a cui si desidera aggiungere un'immagine di sfondo.  
  
2.  Se il riquadro Proprietà non è visualizzato, selezionare **Proprietà** nella scheda **Visualizza**.  
  
3.  Nel riquadro Proprietà espandere la proprietà **BackgroundImage**, quindi eseguire le operazioni seguenti:  
  
    -   Per un'immagine incorporata:  
  
         Impostare **Source** su **Embedded**.  
  
         Impostare **Value** sul nome di un'immagine incorporata nel report.  
  
    -   Per un'immagine esterna:  
  
         Impostare **Source** su **External**.  
  
         Impostare **Value** su un percorso valido a un'immagine. Tale percorso può essere su un server di report in modalità nativa o in modalità integrata SharePoint o può essere su qualsiasi altro sito Web. Per altre informazioni, vedere [Aggiungere un'immagine esterna &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-an-external-image-report-builder-and-ssrs.md).  
  
    -   Per un'immagine contenuta in un campo del database al quale è connesso l'elemento del report:  
  
         Impostare **Source** su **Database**.  
  
         Impostare **Value** sul nome di un campo nel set di dati del report. Per altre informazioni, vedere [Aggiungere un'immagine con associazione a dati &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-a-data-bound-image-report-builder-and-ssrs.md).  
  
         Per **MIMEType**o un formato di file, selezionare il tipo MIME appropriato per l'immagine, ad esempio bmp.  
  
        > [!NOTE]  
        >  Il valore MIMEType viene applicato solo se la proprietà **Source** è impostata su **Database**. Se la proprietà **Source** è impostata su **External** o **Embedded**, il valore di **MIMEType** verrà ignorato.  
  
    -   Per **BackgroundRepeat**, selezionare un'espressione, **Default**, **Repeat**, **RepeatX**, **RepeatY**o **Clip**.  
  
         Per immagini di sfondo in un grafico **BackgroundRepeat** può essere impostato su **Default**, **Repeat**, **Fit**e **Clip**, ma non su **RepeatX** o **RepeatY**.  
  
## <a name="see-also"></a>Vedere anche  
 [Immagini &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/images-report-builder-and-ssrs.md)   
 [Finestra di dialogo Proprietà immagine, Generale &#40;Generatore report e SSRS&#41;](https://msdn.microsoft.com/library/c2218b93-f7fe-46ef-995f-d7dadf9752ec)  
  
  
