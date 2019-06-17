---
title: Riga finestra di dialogo visibilità (Generatore Report) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10126"
ms.assetid: 117fb20c-2fda-437e-bcc5-9010d6d4b53b
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d5ad7e47457aa2d1f1d5e36adec7e988de7b8bbb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66102346"
---
# <a name="row-visibility-dialog-box-report-builder"></a>Finestra di dialogo Visibilità righe (Generatore report)
  Utilizzare la finestra di dialogo **Visibilità righe** per visualizzare o nascondere la riga selezionata quando il report viene eseguito per la prima volta oppure per utilizzare un altro elemento del report per attivare/disattivare la visibilità della riga.  
  
## <a name="options"></a>Opzioni  
 **Quando il report viene eseguito inizialmente**  
 Selezionare un'opzione per indicare come deve essere visualizzata inizialmente la riga nel report.  
  
 **Mostra**  
 Selezionare questa opzione per indicare che la riga deve essere visualizzata.  
  
 **Nascondi**  
 Selezionare questa opzione per indicare che la riga deve essere nascosta.  
  
 **Mostra o Nascondi in base a un'espressione**  
 Selezionare questa opzione per modificare l'impostazione di visibilità iniziale tramite un'espressione.  
  
 Digitare un'espressione che restituisca un valore `Boolean` `True` per nascondere l'elemento e `False` per visualizzarlo. Fare clic sul pulsante **Espressione** (*fx*) per modificare l'espressione.  
  
 **Visualizzazione può essere attivata/disattivata tramite questo elemento del report**  
 Selezionare questa opzione per visualizzare l'immagine dell'elemento Toggle che consente all'utente di visualizzare o nascondere la riga in un visualizzatore di report HTML.  
  
 Digitare o selezionare il nome di una casella di testo del report in cui visualizzare l'immagine dell'elemento Toggle, ad esempio Textbox1. La casella di testo selezionata deve trovarsi nell'ambito corrente o contenitore dell'elemento del report. Ad esempio, per attivare/disattivare la visibilità di righe associate a un gruppo figlio, selezionare una casella di testo in una riga associata al gruppo padre. Per attivare/disattivare la visibilità di un grafico, selezionare una casella di testo che si trovi nello stesso ambito contenitore del grafico, ad esempio il corpo del report o un rettangolo.  
  
## <a name="see-also"></a>Vedere anche  
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)   
 [Aggiungere un'azione Espandi o Comprimi a un elemento &#40;Generatore report e SSRS&#41;](report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)   
 [Immagini &#40;Generatore report e SSRS&#41;](report-design/images-report-builder-and-ssrs.md)   
 [Guida di Generatore report per finestre di dialogo, riquadri e procedure guidate](../../2014/reporting-services/report-builder-help-for-dialog-boxes-panes-and-wizards.md)   
 [Finestra di dialogo Proprietà immagine, Generale &#40;Generatore report e SSRS&#41;](../../2014/reporting-services/image-properties-dialog-box-general-report-builder-and-ssrs.md)  
  
  
