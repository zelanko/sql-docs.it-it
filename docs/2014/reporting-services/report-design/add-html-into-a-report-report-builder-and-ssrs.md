---
title: Aggiungere il codice HTML a un report (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: 30bd631a-f774-48e7-a13a-b6c2eb54d9bb
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 48b2f38635e77f58388cc6d3b04beedd7fdc470c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66106615"
---
# <a name="add-html-into-a-report-report-builder-and-ssrs"></a>Aggiungere il codice HTML a un report (Generatore report e SSRS)
  Utilizzando un segnaposto, è possibile importare codice HTML da un campo nel set di dati per utilizzarlo nel report. Per impostazione predefinita, un segnaposto rappresenta un testo normale e pertanto è necessario modificarne il tipo di markup in codice HTML. Per altre informazioni, vedere [Importazione di codice HTML in un report &#40;Generatore report e SSRS&#41;](importing-html-into-a-report-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-html-from-a-field-in-your-dataset-into-a-text-box"></a>Per aggiungere codice HTML da un campo del set di dati in una casella di testo  
  
1.  Fare clic su **Elenco** nella scheda **Inserisci**. Fare clic nell'area di progettazione, quindi trascinare il mouse per creare una casella delle dimensioni desiderate.  
  
     Verrà visualizzata la finestra di dialogo **Proprietà set di dati** . È possibile utilizzare un set di dati condiviso o un set di dati incorporato nel report. Per altre informazioni, fare clic su [Finestra di dialogo Proprietà set di dati, Query &#40;Generatore report&#41;](../report-data/dataset-properties-dialog-box-query-report-builder.md) o [Finestra di dialogo Proprietà set di dati, Query](../dataset-properties-dialog-box-query.md).  
  
2.  Fare clic su **Casella testo** nella scheda **Inserisci**. Fare clic nell'elenco, quindi trascinare il mouse per creare una casella con le dimensioni desiderate.  
  
3.  Trascinare un campo HTML dal set di dati nella casella di testo. Verrà creato un segnaposto per il campo.  
  
4.  Fare clic con il pulsante destro del mouse sul segnaposto, quindi scegliere **Proprietà segnaposto**.  
  
5.  Nella scheda **Generale** verificare che la casella **Valore** contenga un'espressione che restituisce il campo rilasciato nel passaggio 3.  
  
6.  Fare clic su **HTML - Interpreta tag HTML come stili**. In questo modo il campo verrà valutato come HTML.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Formattazione di numeri e date &#40;Generatore report e SSRS&#41;](formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [Formattazione di linee, colori e immagini &#40;Generatore report e SSRS&#41;](images-report-builder-and-ssrs.md)   
 [Finestra di dialogo Proprietà segnaposto, Generale &#40;Generatore report e SSRS&#41;](../placeholder-properties-dialog-box-general-report-builder-and-ssrs.md)  
  
  
