---
title: Inclusione di indicatori e misuratori in un pannello del misuratore (Generatore report) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: 4dff9b67-b483-4c51-a822-6dbe706a6840
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0d9f5cf2619ea26c56f6511b829b5da524776602
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "77082038"
---
# <a name="include-indicators-and-gauges-in-a-gauge-panel-report-builder-and-ssrs"></a>Inclusione di indicatori e misuratori in un pannello del misuratore (Generatore report e SSRS)
  Il pannello del misuratore è il contenitore di livello superiore in cui sono presenti uno o più misuratori e indicatori. Gli indicatori possono essere incorporati nei misuratori o posizionati accanto a essi nel pannello del misuratore.  
  
 Se l'indicatore e il misuratore sono adiacenti all'interno del pannello del misuratore e presentano dati di campi diversi, è consigliabile aggiungere delle etichette per precisare quali dati sono riportati dal misuratore e quali dall'indicatore.  
  
 È possibile impostare le opzioni del misuratore e dell'indicatore tramite espressioni. Per altre informazioni, vedere [Espressioni &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-embed-an-indicator-in-a-gauge"></a>Per incorporare un indicatore in un misuratore  
  
1.  Aprire un report esistente o crearne uno nuovo contenente una tabella e una matrice con i dati che si desidera visualizzare.   
  
2.  Inserire una colonna nella tabella o nella matrice. Per altre informazioni, vedere [Inserire o eliminare una colonna &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/insert-or-delete-a-column-report-builder-and-ssrs.md).  
  
3.  Nel gruppo **Aree dati** della scheda **Inserisci** fare clic su **Misuratore**e quindi fare clic su una cella nella nuova colonna. Verrà visualizzata la finestra di dialogo **Seleziona tipo di misuratore** .  
  
4.  Fare clic su **Radiale**. Viene selezionato il primo misuratore radiale.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  Fare clic sul misuratore. Viene visualizzato il riquadro **Dati del misuratore** .  
  
7.  Nell'elenco a discesa **(Non specificato)** dell'area **Valori** fare clic sul campo di cui si vogliono visualizzare i valori nel misuratore. In alternativa, trascinare il campo da utilizzare dal set di dati del report.  
  
8.  Fare clic con il pulsante destro del mouse sul misuratore, scegliere **Aggiungi indicatore**e quindi fare clic su **Figlio**. Verrà visualizzata la finestra di dialogo **Seleziona tipo indicatore** .  
  
9. Nel riquadro sinistro della finestra di dialogo **Seleziona tipo indicatore** fare clic sul tipo di indicatore desiderato e quindi sul set di indicatori.  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
11. Fare clic sull'indicatore. Viene visualizzato il riquadro **Dati del misuratore** .  
  
12. Nell'elenco a discesa **(Non specificato)** dell'area **Valori** fare clic sul campo di cui si vogliono visualizzare i valori come indicatore. In alternativa, trascinare il campo da utilizzare dal set di dati del report.  
  
     Il campo può essere lo stesso o diverso rispetto a quello utilizzato nel misuratore.  
  
13. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-show-an-indicator-and-gauge-side-by-side"></a>Per visualizzare un indicatore e un misuratore affiancati  
  
1.  Aprire un report esistente o crearne uno nuovo contenente una tabella e una matrice con i dati che si desidera visualizzare.  
  
2.  Inserire una colonna nella tabella o nella matrice. Per altre informazioni, vedere [Inserire o eliminare una colonna &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/insert-or-delete-a-column-report-builder-and-ssrs.md).  
  
3.  Nel gruppo **Aree dati** della scheda **Inserisci** fare clic su **Misuratore**e quindi fare clic su una cella nella colonna inserita. Verrà visualizzata la finestra di dialogo **Seleziona tipo di misuratore** .  
  
4.  Fare clic su **Radiale**. Viene selezionato il primo misuratore radiale.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  Fare clic sul misuratore. Viene visualizzato il riquadro **Dati del misuratore** .  
  
7.  Nell'elenco a discesa **(Non specificato)** dell'area **Valori** fare clic sul campo di cui si vogliono visualizzare i valori nel misuratore. In alternativa, trascinare il campo da utilizzare dal set di dati del report.  
  
8.  Fare clic con il pulsante destro del mouse sul misuratore, scegliere **Aggiungi indicatore**e quindi **Adiacente**. Verrà visualizzata la finestra di dialogo **Seleziona tipo indicatore** .  
  
9. Nel riquadro sinistro della finestra di dialogo **Seleziona tipo indicatore** fare clic sul tipo di indicatore desiderato e quindi sul set di indicatori.  
  
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
11. Fare clic sull'indicatore. Viene visualizzato il riquadro **Dati del misuratore** .  
  
12. Nell'elenco a discesa **(Non specificato)** dell'area **Valori** fare clic sul campo di cui si vogliono visualizzare i valori come indicatore. In alternativa, trascinare il campo da utilizzare dal set di dati del report.  
  
     Il campo può essere lo stesso o diverso rispetto a quello utilizzato nel misuratore.  
  
13. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
14. Fare clic con il pulsante destro del mouse sul pannello del misuratore e scegliere **Aggiungi etichetta**. Al pannello del misuratore viene aggiunta un'etichetta. Ripetere ancora una volta l'operazione.  
  
     Il pannello del misuratore dispone ora di due etichette.  
  
15. Trascinare ogni etichetta in una posizione accanto al misuratore o all'indicatore.  
  
16. Fare clic con il pulsante destro del mouse sull'etichetta accanto al misuratore, fare clic su **Proprietà etichetta**e digitare il testo nella casella **Testo** .  
  
17. Fare clic con il pulsante destro del mouse sull'etichetta accanto all'indicatore, selezionare **Proprietà etichette**e digitare il testo nella casella **Testo** .  
  
18. [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Indicatori &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/indicators-report-builder-and-ssrs.md)  
  
  
