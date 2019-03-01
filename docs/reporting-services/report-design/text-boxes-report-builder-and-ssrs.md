---
title: Caselle di testo (Generatore report e SSRS) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-design
ms.topic: conceptual
f1_keywords:
- "10134"
- "10120"
- sql13.rtp.rptdesigner.textproperties.general.f1
- sql13.rtp.rptdesigner.textboxproperties.general.f1
ms.assetid: df49e4e3-f279-4c63-a03b-b70c095f4ba2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ef1eb498077cf7d2592592f9c74b5af0516dbceb
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56294655"
---
# <a name="text-boxes-report-builder-and-ssrs"></a>Caselle di testo (Generatore report e SSRS)
  Quando si pensa a una casella di testo, di solito si immagina una casella autonoma contenente testo in un'area, ad esempio, di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office PowerPoint. Nei report impaginati di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] alcune caselle di testo sono esattamente questo e possono visualizzare testo statico per titoli, descrizioni ed etichette oppure testo dinamico basato su espressioni. Tuttavia, anche ogni cella in una tabella o matrice (o in un'area dati Tablix) contiene una casella di testo, che può essere formattata esattamente allo stesso modo delle caselle di testo autonome di un report.  
  
> [!NOTE]  
>  Se si trascina il valore di un campo del set di dati di un report direttamente nell'area di progettazione del report o in una casella di testo in tale area, al momento dell'esecuzione del report sarà visibile solo il primo valore nel set di risultati. Per visualizzare tutti i valori per un campo, prima di tutto è necessario creare una tabella, una matrice o un'area dati elenco e quindi trascinare il campo in una cella nell'area dati. In questo modo, all'esecuzione del report verranno visualizzati tutti i valori in quel campo.  
  
 Per visualizzare il testo ripetuto in un layout in formato libero, creare un'area dati elenco e posizionare la casella di testo al suo interno. Usare un elenco quando si desidera ripetere un form per più valori, ad esempio il form di una fattura ripetuto una volta per ogni cliente. Per altre informazioni, vedere l'argomento sulla [creazione di fatture e moduli con elenchi](../../reporting-services/report-design/create-invoices-and-forms-with-lists-report-builder-and-ssrs.md).  
  
 Usare un contenitore rettangolare se si desidera controllare il layout della casella di testo e lo spazio vuoto sotto l'ultima casella di testo. Per altre informazioni, vedere [Rettangoli e linee &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/rectangles-and-lines-report-builder-and-ssrs.md).  
  
 Le espressioni in una casella di testo possono contenere testo letterale, puntare a un campo del database o calcolare dati. Tutte le espressioni vengono visualizzate come testo segnaposto per consentire la formattazione di numeri, colori e altre proprietà relative all'aspetto. È inoltre possibile combinare segnaposti e testo letterale nella stessa casella di testo.  
  
 È possibile formattare il testo in qualsiasi casella di testo con più tipi di carattere, colori, stili e azioni. Per altre informazioni, vedere [Formattazione di testo e segnaposto &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md).  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
##  <a name="GrowShrinkTextBox"></a> Espansione e riduzione di una casella di testo  
 Per impostazione predefinita, le caselle di testo presentano dimensioni fisse. È possibile ridurre o espandere verticalmente una casella di testo in base al contenuto. Per altre informazioni, vedere [Espansione o riduzione di una casella di testo &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/allow-a-text-box-to-grow-or-shrink-report-builder-and-ssrs.md).  
  
## <a name="rotating-a-text-box"></a>Rotazione di una casella di testo  
 Ruotando le caselle di testo è possibile migliorare la leggibilità dei report, supportare un orientamento di testo specifico delle impostazioni locali, adattare più colonne in un report stampato con dimensioni di pagina fisse e creare report più interessanti dal punto di vista grafico. Una casella di testo può essere ruotata in diverse direzioni: orizzontale, verticale (rotazione di 90 gradi) o di 270 gradi. L'opzione verticale è più usata per le lingue dell'Asia orientale, che si scrivono dall'alto verso il basso. Nella maggior parte dei renderer l'opzione verticale permette di gestire correttamente la rotazione del glifo in modo che il testo venga scritto dall'alto verso il basso, senza che i caratteri appaiano ai lati. Per le altre lingue, le opzioni verticale e di 270 gradi determinano che il testo venga scritto lateralmente.  
  
 È possibile ruotare caselle di testo che contengono testo statico, campi di un set di dati di un report o dati calcolati. La casella di testo può essere autonoma nel corpo del report, in una tabella o una matrice oppure nell'intestazione e nel piè di pagina di un report.  
  
 Nell'immagine seguente vengono mostrate tre versioni di un report tabella in cui i dati sono raggruppati per mese. La casella di testo contenente il valore del mese presenta un orientamento diverso.  
  
 ![rs_TextBoxOrientation](../../reporting-services/report-design/media/rs-textboxorientation.gif "rs_TextBoxOrientation")  
  
 L'orientamento viene impostato sulla casella di testo e si applica a tutto il testo contenuto nella casella. Non è possibile specificare un orientamento diverso per varie parti della casella di testo.  
  
 Per informazioni introduttive, vedere la sezione relativa alla rotazione del testo in [Esercitazione: Formattazione di testo &#40;Generatore report&#41;](../../reporting-services/tutorial-format-text-report-builder.md) e [Impostare l'orientamento della casella di testo &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/set-text-box-orientation-report-builder-and-ssrs.md).  
  
##  <a name="HowTo"></a> Procedure  
 [Aggiungere, spostare o eliminare una casella di testo &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/add-move-or-delete-a-text-box-report-builder-and-ssrs.md)  
  
 [Formattare il testo in una casella di testo &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/format-text-in-a-text-box-report-builder-and-ssrs.md)  
  
 [Impostare l'orientamento della casella di testo &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/set-text-box-orientation-report-builder-and-ssrs.md)  
  
 [Espansione o riduzione di una casella di testo &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/allow-a-text-box-to-grow-or-shrink-report-builder-and-ssrs.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Formattazione di testo e segnaposto &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/formatting-text-and-placeholders-report-builder-and-ssrs.md)   
 [Formattazione di numeri e date &#40;Generatore report e SSRS&#41;](../../reporting-services/report-design/formatting-numbers-and-dates-report-builder-and-ssrs.md)  
  
  
