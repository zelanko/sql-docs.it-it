---
title: Visualizzare i numeri di pagina o altre proprietà del report (Generatore report e SSRS) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-design
ms.topic: conceptual
ms.assetid: c7d95245-4709-4d04-acb4-59bf71e60d97
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 0f9e826ff115183180ad42a1c065619f2196cd3e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65580887"
---
# <a name="display-page-numbers-or-other-report-properties-report-builder-and-ssrs"></a>Visualizzare i numeri di pagina o altre proprietà del report (Generatore report e SSRS)
  Aggiungere numeri di pagina, un titolo di report, un nome file e altre proprietà alle intestazioni o ai piè di pagina del report è un'operazione semplice. Queste proprietà sono archiviate come campi nella cartella Campi predefiniti nel riquadro dei dati del report:  
  
-   Ora di esecuzione  
  
-   Numero di pagina  
  
-   Cartella dei report  
  
-   Nome report  
  
-   URL del server di report  
  
-   Totale pagine  
  
-   ID utente  
  
-   Linguaggio  
  
 Per un numero di pagina, potrebbe essere necessario aggiungere la parola 'Pagina' prima del numero. Inoltre, potrebbe essere necessario indicare anche il numero complessivo di pagine.  
  
> [!NOTE]  
>  L'aggiunta del numero complessivo di pagine al piè di pagina potrebbe rallentare le prestazioni quando si esegue o si visualizza il report in anteprima.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-page-number-or-other-report-properties"></a>Per aggiungere il numero di pagina o altre proprietà  
  
1.  Espandere la cartella Campi predefiniti nel riquadro dei dati del report.  
  
    > [!NOTE]  
    >  Se il riquadro dei dati del report non viene visualizzato, fare clic su **Dati report**nella scheda Visualizza.  
  
2.  Trascinare il campo **Numero pagina** dal riquadro dei dati del report nell'intestazione o nel piè di pagina del report.  
  
    > [!NOTE]  
    >  Il piè di pagina verrà aggiunto automaticamente al report. Per aggiungere un'intestazione di pagina, nella scheda **Inserisci** fare clic su **Intestazione**e quindi su **Aggiungi intestazione**.  
    >   
    >  Verrà aggiunta una casella di testo contenente l'espressione semplice [&PageNumber].  
  
### <a name="to-add-the-word-page-before-the-page-number"></a>Per aggiungere la parola "Pagina" prima del numero di pagina  
  
1.  Fare clic con il pulsante destro del mouse sulla casella di testo che contiene [&PageNumber], quindi scegliere **Espressioni**.  
  
     La casella di testo **Imposta espressione per: Valore** contiene l'espressione =Globals!PageNumber.  
  
2.  Posizionare il cursore dopo il segno = e digitare **"Pagina " &** .  
  
     L'espressione cambierà in ="Pagina "&Globals!PageNumber  
  
3.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
### <a name="to-add-total-number-of-pages-after-the-page-number"></a>Per aggiungere il numero complessivo di pagine dopo il numero di pagina  
  
1.  Fare clic con il pulsante destro del mouse sulla casella di testo con l'espressione, quindi scegliere **Espressioni**.  
  
2.  Digitare **&" di "&** alla fine dell'espressione.  
  
3.  Nel riquadro Categoria espandere **Campi predefiniti** , quindi fare doppio clic **TotalPages**.  
  
     L'espressione cambierà in ="Page "&Globals!PageNumber &" di "&Globals!TotalPages.  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 [Intestazioni di pagina e piè di pagina &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/page-headers-and-footers-report-builder-and-ssrs.md)   
 [Formattare il testo in una casella di testo &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/format-text-in-a-text-box-report-builder-and-ssrs.md)  
  
  
