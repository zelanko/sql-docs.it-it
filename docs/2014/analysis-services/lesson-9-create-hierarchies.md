---
title: 'Lezione 10: Creare gerarchie | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1e2561d3-4890-4495-a9cd-84eb88508938
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: eb70d7d495d88ee62e98bf27f2b92bf569c98387
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66078185"
---
# <a name="lesson-10-create-hierarchies"></a>Lezione 10: Creare gerarchie
  In questa lezione si procederà alla creazione di gerarchie. Le gerarchie sono gruppi di colonne disposti in livelli. Una gerarchia Geografia potrebbe ad esempio includere i sottolivelli Paese, Stato, Regione e Città. Le gerarchie possono essere visualizzate separatamente rispetto alle altre colonne in un elenco di campi di un'applicazione client di creazione di report, per semplificarne l'esplorazione e l'inserimento in un report da parte degli utenti client. Per altre informazioni, vedere [Gerarchie &#40;SSAS tabulare&#41;](tabular-models/hierarchies-ssas-tabular.md).  
  
 Per creare le gerarchi viene usata la funzionalità Progettazione modelli in *Vista diagramma*. La creazione e la gestione di gerarchie non sono supportate in Progettazione modelli in Vista dati.  
  
 Tempo stimato per il completamento della lezione: **20 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
 Questo argomento fa parte di un'esercitazione relativa alla modellazione tabulare che deve essere completata nell'ordine specificato. Prima di eseguire le attività in questa lezione, è necessario avere completato la lezione precedente: [Lezione 9: Creare prospettive](lesson-8-create-perspectives.md).  
  
## <a name="create-hierarchies"></a>Creare gerarchie  
  
#### <a name="to-create-a-category-hierarchy-in-the-product-table"></a>Per creare una gerarchia Category nella tabella Product  
  
1.  In Progettazione modelli fare clic sui `Model` nel menu, quindi scegliere **Vista modelli**e quindi fare clic su **vista diagramma**.  
  
    > [!TIP]  
    >  Utilizzare i controlli della mini mappa in alto a destra in Progettazione modelli per modificare la modalità di visualizzazione degli oggetti nella vista diagramma. Se si riposizionano gli oggetti nella vista diagramma, la vista verrà mantenuta quando si salva il progetto.  
  
2.  In Progettazione modelli fare doppio clic il `Product` tabella e quindi fare clic su **crea gerarchia**. Verrà visualizzata una nuova gerarchia nella parte inferiore della finestra della tabella.  
  
3.  Il nome di gerarchia e rinominare la gerarchia digitando `Category`, quindi premere INVIO.  
  
4.  Nel `Product` , fare clic il **Product Category Name** colonna, quindi trascinarla il `Category` gerarchia e infine rilasciarla sopra il `Category` nome.  
  
5.  Nel `Category` gerarchia, fare doppio clic sul **Product Category Name** colonna, quindi fare clic su **rinominare**, quindi digitare `Category`.  
  
    > [!NOTE]  
    >  La ridenominazione di una colonna in una gerarchia non comporta la ridenominazione della colonna nella tabella. Una colonna in una gerarchia è solo una rappresentazione della colonna nella tabella.  
  
6.  Nel `Product` tabella, fare doppio clic sui **Product Subcategory Name** colonna, quindi nel menu di scelta rapida, scegliere **Aggiungi a gerarchia**e quindi fare clic su `Category`.  
  
7.  Rinominare **Product Subcategory Name** a `Subcategory`.  
  
8.  Tramite selezione e trascinamento oppure utilizzando il **Aggiungi a gerarchia** nel menu di scelta rapida di comando, aggiungere il **Model Name** e **Product Name** colonne (in ordine) e posizionarle sotto la **Product Subcategory Name** colonna. Rinominare queste colonne `Model` e `Product`, rispettivamente.  
  
#### <a name="to-create-hierarchies-in-the-date-table"></a>Per creare gerarchie nella tabella Date  
  
1.  In Progettazione modelli fare clic con il pulsante destro del mouse sulla tabella **Date** e scegliere **Crea gerarchia**.  
  
2.  Rinominare la gerarchia in **Calendar**.  
  
3.  Aggiungere le colonne seguenti, in ordine, quindi rinominarle:  
  
    |colonna|Rinominare in:|  
    |------------|----------------|  
    |Calendar Year|Year|  
    |Calendar Semester|Semester|  
    |Calendar Quarter|Quarter|  
    |Month Calendar|Month|  
    |Day Of Month|Day|  
  
4.  Nella tabella **Date** ripetere i passaggi precedenti, creando una gerarchia **Fiscal** e includendo le colonne seguenti:  
  
    |colonna|Rinominare in:|  
    |------------|----------------|  
    |Fiscal Year|Year|  
    |Fiscal Semester|Semester|  
    |Fiscal Quarter|Quarter|  
    |Month Calendar|Month|  
    |Day Of Month|Day|  
  
5.  Infine, nella tabella **Date** ripetere i passaggi precedenti, creando una gerarchia **Production Calendar** e includendo le colonne seguenti:  
  
    |colonna|Rinominare in:|  
    |------------|----------------|  
    |Calendar Year|Year|  
    |Week Number Of Year|Week|  
    |Day Of Week|Day|  
  
## <a name="next-steps"></a>Passaggi successivi  
 Per continuare questa esercitazione, passare alla lezione successiva: [Lezione 11: Creare partizioni](lesson-10-create-partitions.md).  
  
  
