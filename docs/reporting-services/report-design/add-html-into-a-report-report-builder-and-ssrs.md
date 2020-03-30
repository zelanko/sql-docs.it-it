---
title: Aggiungere codice HTML a un report (Generatore report) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 30bd631a-f774-48e7-a13a-b6c2eb54d9bb
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: e18753c105eb63343bf57977f8ced3a0cf0fe9e6
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "77081628"
---
# <a name="add-html-into-a-report-report-builder-and-ssrs"></a>Aggiungere il codice HTML a un report (Generatore report e SSRS)
  Utilizzando un segnaposto, è possibile importare codice HTML da un campo nel set di dati per utilizzarlo nel report. Per impostazione predefinita, un segnaposto rappresenta un testo normale e pertanto è necessario modificarne il tipo di markup in codice HTML. Per altre informazioni, vedere [Importazione di codice HTML in un report &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/importing-html-into-a-report-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-html-from-a-field-in-your-dataset-into-a-text-box"></a>Per aggiungere codice HTML da un campo del set di dati in una casella di testo  
  
1.  Fare clic su **Elenco** nella scheda **Inserisci**. Fare clic nell'area di progettazione, quindi trascinare il mouse per creare una casella delle dimensioni desiderate.  
  
     Verrà visualizzata la finestra di dialogo **Proprietà set di dati** . È possibile utilizzare un set di dati condiviso o un set di dati incorporato nel report. Per altre informazioni, fare clic su [Finestra di dialogo Proprietà set di dati, Query &#40;Generatore report&#41;](../../reporting-services/report-data/dataset-properties-dialog-box-query-report-builder.md) o [Finestra di dialogo Proprietà set di dati, Query](https://msdn.microsoft.com/library/1fa34a4b-7de0-4e92-99fa-bc28a206773f).  
  
2.  Fare clic su **Casella testo** nella scheda **Inserisci**. Fare clic nell'elenco, quindi trascinare il mouse per creare una casella con le dimensioni desiderate.  
  
3.  Trascinare un campo HTML dal set di dati nella casella di testo. Verrà creato un segnaposto per il campo.  
  
4.  Fare clic con il pulsante destro del mouse sul segnaposto, quindi scegliere **Proprietà segnaposto**.  
  
5.  Nella scheda **Generale** verificare che la casella **Valore** contenga un'espressione che restituisce il campo rilasciato nel passaggio 3.  
  
6.  Fare clic su **HTML - Interpreta tag HTML come stili**. In questo modo il campo verrà valutato come HTML.  
  
7.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Formattazione di numeri e date &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)   
 [Formattazione di linee, colori e immagini &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/formatting-lines-colors-and-images-report-builder-and-ssrs.md)   
 [Finestra di dialogo Proprietà segnaposto, Generale &#40;Generatore report e SSRS&#41;](https://msdn.microsoft.com/library/7a867736-a3b0-4b5a-b3e5-fe7c8d7618a8)  
  
  
