---
title: Specificare un'immagine come indicatore di misura su un misuratore (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 9d73b3c3-a068-4868-a2be-0cd261b6e92b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c7a57987a5d1cd0ac7984db3b716521d9c7a09af
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66101150"
---
# <a name="specify-an-image-as-a-pointer-on-a-gauge-report-builder-and-ssrs"></a>Specificare un'immagine come indicatore di misura su un misuratore (Generatore report e SSRS)
  Il misuratore include tre stili predefiniti utilizzabili per personalizzare l'aspetto dell'indicatore di misura. Per un misuratore radiale, gli stili predefiniti sono Lancetta, Marcatore e Barre, mentre quelli per un misuratore lineare sono Marcatore, Barre e Termometro. Se è necessario un indicatore di misura univoco, l'utente può creare e specificare un'immagine utilizzabile come indicatore di misura con funzionalità complete.  
  
 Quando si specifica un'immagine per l'indicatore di misura, tale immagine deve includere le specifiche seguenti:  
  
-   L'origine dell'indicatore di misura, o centro di rotazione, deve trovarsi nella parte superiore dell'immagine.  
  
-   L'estremità dell'indicatore di misura deve essere rivolta verso il basso.  
  
 Poiché l'indicatore di misura è una forma irregolare, sarà necessario specificare un colore di trasparenza per nascondere le parti non necessarie dell'immagine. Come colore di trasparenza selezionare un colore generalmente non utilizzato per il misuratore, in quanto i colori specificati non verranno visualizzati.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../includes/ssrbrddup-md.md)]  
  
### <a name="to-specify-an-image-as-a-pointer-on-the-gauge"></a>Per specificare un'immagine come indicatore di misura sul misuratore  
  
1.  In visualizzazione della struttura fare clic sull'indicatore di misura del misuratore.  
  
2.  Opzionale Se sul misuratore non è presente alcun puntatore, fare clic con il pulsante destro del mouse sul misuratore e scegliere **Aggiungi puntatore**. Al misuratore verrà aggiunto un indicatore di misura.  
  
3.  Fare clic sulla scheda **Inserisci** sulla barra multifunzione e fare doppio clic sull'icona dell'immagine. Verrà visualizzata la finestra di dialogo **Proprietà immagine**.  
  
4.  Aggiungere un'immagine al report. Per ulteriori informazioni, vedere [incorporare un'immagine in un Report &#40;Generatore report e SSRS&#41;](report-design/embed-an-image-in-a-report-report-builder-and-ssrs.md).  
  
5.  Aprire il riquadro Proprietà.  
  
6.  Nell'area di progettazione fare clic sull'indicatore di misura. Nel riquadro Proprietà verranno visualizzate le proprietà dell'indicatore di misura.  
  
7.  Espandere il nodo PointerImage.  
  
8.  In **origine**selezionare **incorporata** dall'elenco a discesa.  
  
    > [!NOTE]  
    >  Se l'immagine viene archiviata nel database o sul Web, è possibile specificare l'opzione adatta per questa proprietà. Per ulteriori informazioni, vedere finestra di [dialogo Proprietà immagine, generale &#40;Generatore report e SSRS&#41;](../../2014/reporting-services/image-properties-dialog-box-general-report-builder-and-ssrs.md).  
  
9. In **valore**selezionare il nome dell'immagine dall'elenco a discesa.  
  
10. In **TransparentColor**selezionare un valore di colore che si desidera rimuovere dall'immagine. In questo modo, l'aspetto dell'indicatore di misura nel misuratore risulterà migliore.  
  
## <a name="see-also"></a>Vedere anche  
 [Formattazione degli indicatori di misura su un misuratore &#40;Generatore report e SSRS&#41;](report-design/formatting-pointers-on-a-gauge-report-builder-and-ssrs.md)   
 [Aggiungere un misuratore a un report &#40;Generatore report e SSRS&#41;](report-design/add-a-gauge-to-a-report-report-builder-and-ssrs.md)   
 [Formattazione di linee, colori e immagini &#40;Generatore report e SSRS&#41;](report-design/images-report-builder-and-ssrs.md)   
 [Misuratori &#40;Generatore report e SSRS&#41;](report-design/gauges-report-builder-and-ssrs.md)  
  
  
