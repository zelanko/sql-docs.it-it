---
title: Caselle di testo (Generatore report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10134"
- sql12.rtp.rptdesigner.textproperties.general.f1
- "10120"
- sql12.rtp.rptdesigner.textboxproperties.general.f1
ms.assetid: df49e4e3-f279-4c63-a03b-b70c095f4ba2
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: fb96831c54a67a6ea74ca984cb346dcaaf50a335
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66104625"
---
# <a name="text-boxes-report-builder-and-ssrs"></a>Caselle di testo (Generatore report e SSRS)
  In genere si pensa a una casella di testo come a una casella autonoma contenente testo in un'area quale [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office PowerPoint. In Generatore report, alcune caselle di testo sono di questo tipo e consentono di visualizzare un testo letterale per titoli, descrizioni ed etichette o un testo dinamico basato sulle espressioni. Tuttavia anche in tutte le celle di una tabella o di una matrice (area dati Tablix) è contenuta una casella di testo che può essere formattata esattamente come le caselle di testo autonome di un report.  
  
> [!NOTE]  
>  Se si trascina il valore di un campo del set di dati di un report direttamente nell'area di progettazione del report o in una casella di testo in tale area, al momento dell'esecuzione del report sarà visibile solo il primo valore nel set di risultati. Per visualizzare tutti i valori per un campo, è necessario trascinare il campo in una cella di una tabella o di una matrice. In questo modo, all'esecuzione del report verranno visualizzati tutti i valori in quel campo.  
  
 Per visualizzare il testo ripetuto in un layout in formato libero, posizionare una casella di testo in un'area dati elenco. Usare un elenco quando si desidera ripetere un form per più valori, ad esempio il form di una fattura ripetuto una volta per ogni cliente. Per altre informazioni, vedere [sono elencati &#40;Generatore Report e SSRS&#41;](create-invoices-and-forms-with-lists-report-builder-and-ssrs.md).  
  
 Usare un contenitore rettangolare se si desidera controllare il layout della casella di testo e lo spazio vuoto sotto l'ultima casella di testo. Per altre informazioni, vedere [Rettangoli e linee &#40;Generatore report e SSRS&#41;](rectangles-and-lines-report-builder-and-ssrs.md).  
  
 Le espressioni in una casella di testo possono contenere testo letterale, puntare a un campo del database o calcolare dati. Tutte le espressioni vengono visualizzate come testo segnaposto per consentire la formattazione di numeri, colori e altre proprietà relative all'aspetto. È inoltre possibile combinare segnaposti e testo letterale nella stessa casella di testo.  
  
 È possibile formattare il testo in qualsiasi casella di testo con più tipi di carattere, colori, stili e azioni. Per altre informazioni, vedere [Formattazione di testo e segnaposto &#40;Generatore report e SSRS&#41;](formatting-text-and-placeholders-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="GrowShrinkTextBox"></a> Espansione e riduzione di una casella di testo  
 Per impostazione predefinita, le caselle di testo presentano dimensioni fisse. È possibile ridurre o espandere verticalmente una casella di testo in base al contenuto. Per altre informazioni, vedere [Espansione o riduzione di una casella di testo &#40;Generatore report e SSRS&#41;](allow-a-text-box-to-grow-or-shrink-report-builder-and-ssrs.md).  
  
## <a name="orienting-a-text-box"></a>Orientamento di una casella di testo  
 Orientando le caselle di testo è possibile migliorare la leggibilità dei report, supportare un orientamento di testo specifico delle impostazioni locali, adattare più colonne in un report stampato con dimensioni di pagina fisse e creare report più soddisfacenti dal punto di vista grafico. Una casella di testo può essere orientata in diverse direzioni: orizzontale, verticale o con una rotazione di 270 gradi. L'opzione verticale è più usata per le lingue dell'Asia orientale, che si scrivono dall'alto verso il basso. Nella maggior parte dei renderer l'opzione verticale consente di gestire la proprietà di rotazione del glifo in modo che il testo venga scritto dall'alto verso il basso, ma i caratteri non risultino ai lati. Per le altre lingue, le opzioni verticale e di 270 gradi determinano che il testo venga scritto lateralmente.  
  
 È possibile applicare l'orientamento alle caselle di testo che contengono testo letterale, campi di un set di dati del report o dati calcolati. La casella di testo può essere autonoma nel corpo del report, in una tabella o una matrice oppure nell'intestazione e nel piè di pagina di un report.  
  
 Nell'immagine seguente vengono mostrate tre versioni di un report tabella in cui i dati sono raggruppati per mese. La casella di testo contenente il valore del mese presenta un orientamento diverso.  
  
 ![rs_TextBoxOrientation](../media/rs-textboxorientation.gif "rs_TextBoxOrientation")  
  
 L'orientamento viene impostato sulla casella di testo e si applica a tutto il testo contenuto nella casella. Non è possibile specificare un orientamento diverso per varie parti della casella di testo.  
  
 Per iniziare rapidamente con la modifica l'orientamento del testo, vedere la sezione sulla rotazione del testo nel [esercitazione: Formattazione di testo &#40;Generatore report&#41;](../tutorial-format-text-report-builder.md). Per altre informazioni, vedere [impostare orientamento della casella di testo &#40;Generatore Report e SSRS&#41;](set-text-box-orientation-report-builder-and-ssrs.md).  
  
##  <a name="HowTo"></a> Procedure  
 [Aggiungere, spostare o eliminare una casella di testo &#40;Generatore report e SSRS&#41;](add-move-or-delete-a-text-box-report-builder-and-ssrs.md)  
  
 [Formattare il testo in una casella di testo &#40;Generatore report e SSRS&#41;](format-text-in-a-text-box-report-builder-and-ssrs.md)  
  
 [Impostare l'orientamento della casella di testo &#40;Generatore report e SSRS&#41;](set-text-box-orientation-report-builder-and-ssrs.md)  
  
 [Espansione o riduzione di una casella di testo &#40;Generatore report e SSRS&#41;](allow-a-text-box-to-grow-or-shrink-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Formattazione di testo e segnaposto &#40;Generatore report e SSRS&#41;](formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [Formattazione di numeri e date &#40;Generatore report e SSRS&#41;](formatting-numbers-and-dates-report-builder-and-ssrs.md)  
  
  
