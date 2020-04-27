---
title: Finestra di dialogo Visibilità righe | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.rowvisibility.f1
- "10126"
ms.assetid: 557ecf70-62b1-47f5-9322-0ebdc809d018
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fe9af16c34fa70bb8fcda0dcaae64a39786e3cd3
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66102411"
---
# <a name="row-visibility-dialog-box"></a>Finestra di dialogo Visibilità righe
  Utilizzare la finestra di dialogo **Visibilità righe** per visualizzare o nascondere la riga selezionata quando il report viene eseguito per la prima volta oppure per utilizzare un altro elemento del report per attivare/disattivare la visibilità della riga.  
  
## <a name="options"></a>Opzioni  
 **Quando il report viene eseguito inizialmente**  
 Selezionare un'opzione per indicare come deve essere visualizzato inizialmente l'elemento nel report.  
  
 **Mostra**  
 Selezionare questa opzione per visualizzare l'elemento del report.  
  
 **Nascondi**  
 Selezionare questa opzione per nascondere l'elemento del report.  
  
 **Mostra o nascondi in base a un'espressione**  
 Selezionare questa opzione per modificare l'impostazione di visibilità iniziale tramite un'espressione.  
  
 Digitare un'espressione che restituisca un valore `Boolean``True` per nascondere l'elemento e `False` per visualizzarlo. Fare clic sul pulsante espressione (**FX**) per modificare l'espressione.  
  
 **La visualizzazione può essere attivata/disattivata tramite questo elemento del report**  
 Selezionare questa opzione per visualizzare l'immagine dell'elemento Toggle che consente all'utente di visualizzare o nascondere l'elemento del report in un visualizzatore di report HTML.  
  
 Digitare o selezionare il nome di una casella di testo del report in cui visualizzare l'immagine dell'elemento Toggle, ad esempio Textbox1. La casella di testo selezionata deve trovarsi nell'ambito corrente o contenitore dell'elemento del report. Ad esempio, per attivare/disattivare la visibilità di righe associate a un gruppo figlio, selezionare una casella di testo in una riga associata al gruppo padre. Per attivare/disattivare la visibilità di un grafico, selezionare una casella di testo che si trovi nello stesso ambito contenitore del grafico, ad esempio il corpo del report o un rettangolo.  
  
## <a name="see-also"></a>Vedi anche  
 [Esempi di espressioni &#40;Generatore report e SSRS&#41;](report-design/expression-examples-report-builder-and-ssrs.md)   
 [Aggiungere un'azione Espandi o Comprimi a un elemento &#40;Generatore report e SSRS&#41;](report-design/add-an-expand-or-collapse-action-to-an-item-report-builder-and-ssrs.md)   
 [Immagini &#40;Generatore report e SSRS&#41;](report-design/images-report-builder-and-ssrs.md)   
 [Guida sensibile al contesto di Progettazione report](tools/report-designer-f1-help.md)  
  
  
