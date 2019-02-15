---
title: Aggiungere un segnalibro a un report (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: f130562e-5673-40e3-8e01-de7227a21d41
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 497d1ca02640f31f1628583d76a06006276b7e2d
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56287509"
---
# <a name="add-a-bookmark-to-a-report-report-builder-and-ssrs"></a>Aggiungere un segnalibro a un report (Generatore report e SSRS)
  Aggiungere segnalibri e collegamenti a segnalibro a un report quando si desidera fornire un sommario personalizzato o collegamenti interni personalizzati nel report. In genere i segnalibri vengono aggiunti a posizioni del report cui si desidera indirizzare gli utenti, ad esempio a ogni tabella o grafico o ai valori di gruppo univoci visualizzati in una tabella o una matrice. È possibile creare stringhe da utilizzare come segnalibri o, per i gruppi, è possibile impostare il segnalibro sull'espressione di raggruppamento.  
  
 Dopo avere creato i segnalibri, è possibile aggiungere elementi di report su cui l'utente può fare clic su per passare a ogni segnalibro. Tali elementi sono in genere costituiti da caselle di testo o immagini.  
  
 Se nel report ad esempio è visualizzata una tabella raggruppata in base al colore, è possibile aggiungere un segnalibro basato sull'espressione di raggruppamento all'intestazione di gruppo. Successivamente è possibile aggiungere una tabella con una sola casella di testo all'inizio del report in cui sono visualizzati i valori relativi al colore e impostare il collegamento a segnalibro in tale casella di testo. Quando si fa clic sul colore, si passa alla pagina del report in cui viene visualizzata la riga dell'intestazione di gruppo per il colore specifico.  
  
 È possibile aggiungere un segnalibro a qualsiasi elemento di report e un collegamento a qualsiasi elemento cui sia associata una proprietà **Azione** , ad esempio una casella di testo, un'immagine oppure una serie calcolata in un grafico. Per altre informazioni, vedere [Finestra di dialogo Proprietà azione &#40;Generatore report e SSRS&#41;](../action-properties-dialog-box-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-add-a-bookmark"></a>Per aggiungere un segnalibro  
  
1.  In visualizzazione struttura report selezionare la casella di testo, l'immagine, il grafico o un altro elemento del report a cui si desidera aggiungere un segnalibro. Le proprietà per l'elemento selezionato verranno visualizzate nel riquadro Proprietà.  
  
2.  Nella casella di testo accanto a **Segnalibro**digitare una stringa che rappresenta l'etichetta per il segnalibro specifico. Ad esempio, è possibile digitare **BikePhoto** come segnalibro per un'immagine nel report. In alternativa, fare clic sul pulsante Espressione (**fx**) per aprire la finestra di dialogo **Espressione** in cui specificare un'espressione che restituisca un'etichetta. Per un gruppo, l'espressione digitata deve essere quella di raggruppamento.  
  
    > [!NOTE]  
    >  Il segnalibro può essere rappresentato da qualsiasi stringa, ma deve essere univoca nell'ambito del report. In caso contrario, un collegamento al segnalibro individuerà il primo segnalibro corrispondente.  
  
### <a name="to-add-a-bookmark-link"></a>Per aggiungere un collegamento a segnalibro  
  
1.  Nella visualizzazione della struttura fare clic con il pulsante destro del mouse sulla casella di testo, immagine o grafico cui si vuole aggiungere un collegamento, quindi scegliere **Proprietà**.  
  
2.  Nella finestra di dialogo **Proprietà** relativa a tale elemento di report fare clic su **Azione**.  
  
3.  Selezionare **Vai al segnalibro**. Nella finestra di dialogo verrà visualizzata una sezione aggiuntiva per questa opzione.  
  
4.  Nella casella **Selezionare un segnalibro** digitare o selezionare un segnalibro o un'espressione che restituisca un segnalibro. Utilizzando l'esempio precedente, digitare **BikePhoto** per creare un collegamento all'immagine nel report.  
  
5.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
6.  (Facoltativo) Il testo non viene formattato automaticamente come un collegamento. Per il testo è utile modificare il colore e l'effetto del testo per indicare che si tratta di un collegamento. È possibile, ad esempio, modificare il colore in blu e sottolineare il testo nella sezione **Carattere** nella scheda Home della barra multifunzione.  
  
7.  Per verificare il collegamento, fare clic su **Esegui** per visualizzare il report in anteprima, quindi fare clic sull'elemento del report su cui è stato impostato il collegamento.  
  
## <a name="see-also"></a>Vedere anche  
 [Ordinamento interattivo, mappe documento e collegamenti &#40;Generatore report e SSRS&#41;](interactive-sort-document-maps-and-links-report-builder-and-ssrs.md)   
 [Espressioni &#40;Generatore report e SSRS&#41;](expressions-report-builder-and-ssrs.md)   
 [Filtro, raggruppamento e ordinamento di dati &#40;Generatore report e SSRS&#41;](filter-group-and-sort-data-report-builder-and-ssrs.md)  
  
  
