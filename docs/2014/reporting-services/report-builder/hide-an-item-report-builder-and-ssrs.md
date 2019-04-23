---
title: Nascondere un elemento (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.shared.visibility.f1
- "10503"
ms.assetid: 9d78f8de-959b-456f-8947-687fa6e2ba91
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: a67d093576076e9822427773afb710c57f801827
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59941627"
---
# <a name="hide-an-item-report-builder-and-ssrs"></a>Nascondere un elemento (Generatore report e SSRS)
  Impostare la visibilità di un elemento del report quando si desidera nascondere in modo condizionale un elemento in base a un parametro del report o ad altre espressioni specificate.  
  
 È inoltre possibile progettare un report per consentire all'utente di attivare o disattivare la visualizzazione di elementi di report facendo clic su caselle di testo nel report, ad esempio per un report drill-down. Per altre informazioni, vedere [Aggiungere un'azione Espandi o Comprimi a un elemento &#40;Generatore report e SSRS&#41;](../report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md).  
  
 Le procedure descritte di seguito illustrano il modo in cui visualizzare o nascondere un elemento di report in un report di cui è stato eseguito il rendering in base a una costante oppure a un'espressione.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-hide-a-report-item"></a>Per nascondere un elemento di report  
  
1.  Nella visualizzazione di progettazione report fare clic con il pulsante destro del mouse sull'elemento del report e aprire la relativa pagina **Proprietà** .  
  
    > [!NOTE]  
    >  Per selezionare un'intera tabella o un'area dati matrice, fare clic nell'area dati per selezionarla, fare clic con il pulsante destro del mouse su una riga, una colonna oppure sul punto di controllo in angolo e quindi scegliere **Proprietà Tablix**.  
  
2.  Fare clic su **Visibilità**.  
  
3.  In **Quando il report viene eseguito inizialmente**specificare se nascondere l'elemento la prima volta che il report viene visualizzato:  
  
    -   Per visualizzare l'elemento, fare clic su **Mostra**.  
  
    -   Per nascondere l'elemento., fare clic su **Nascondi**.  
  
    -   Per specificare un'espressione valutata in fase di esecuzione, fare clic su **Mostra o nascondi in base a un'espressione**. Digitare l'espressione oppure fare clic sul pulsante dell'espressione (**fx**) per creare l'espressione nella finestra di dialogo **Espressione** .  
  
        > [!NOTE]  
        >  Quando si specifica un'espressione per la visibilità, viene impostata la proprietà Hidden dell'elemento di report, come mostrato nell'immagine seguente. L'espressione valutata consente di mostrare l'elemento di report quando il valore è False e di nasconderlo quando il valore è True.   
        > ![Finestra di dialogo Properties_Visibility e proprietà Hidden](../media/hiddenproperty-propertiesvisibility.png "Finestra di dialogo Properties_Visibility e proprietà Hidden")  
  
4.  Fare due volte clic su **OK** .  
  
### <a name="to-hide-static-rows-in-a-table-matrix-or-list"></a>Per nascondere le righe statiche di una tabella, matrice o elenco  
  
1.  In visualizzazione progettazione report fare clic sulla tabella, sulla matrice o sull'elenco per visualizzare gli handle di riga e di colonna.  
  
2.  Fare clic con il pulsante destro del mouse sull'handle di riga e quindi scegliere **Visibilità righe**. Verrà visualizzata la finestra di dialogo **Visibilità righe** .  
  
3.  Per impostare la visibilità, eseguire i passaggi 3 e 4 della prima procedura.  
  
### <a name="to-hide-static-columns-in-a-table-matrix-or-list"></a>Per nascondere colonne statiche in una tabella, in una matrice o in un elenco  
  
1.  In visualizzazione Progettazione selezionare la tabella, la matrice o l'elenco per visualizzare gli handle di riga e di colonna.  
  
2.  Fare clic con il pulsante destro del mouse sull'handle di colonna e quindi scegliere **Visibilità colonne**.  
  
3.  Nella finestra di dialogo **Visibilità colonne** eseguire i passaggi 3 e 4 della prima procedura.  
  
## <a name="see-also"></a>Vedere anche  
 [Azione di drill-down &#40;Generatore report e SSRS &#41;](../report-design/drilldown-action-report-builder-and-ssrs.md)   
 [Aggiungere un'azione Espandi o Comprimi a un elemento &#40;Generatore report e SSRS&#41;](../report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)   
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](../report-design/expression-examples-report-builder-and-ssrs.md)  
  
  
