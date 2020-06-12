---
title: 'Lezione 10: creare gerarchie | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 1e2561d3-4890-4495-a9cd-84eb88508938
author: minewiskan
ms.author: owend
ms.openlocfilehash: b6b57669eed30abf010b9d2775950bf0cd6c6e67
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84542153"
---
# <a name="lesson-10-create-hierarchies"></a>Lezione 10: Creare gerarchie
  In questa lezione si procederà alla creazione di gerarchie. Le gerarchie sono gruppi di colonne disposti in livelli. Una gerarchia Geografia potrebbe ad esempio includere i sottolivelli Paese, Stato, Regione e Città. Le gerarchie possono essere visualizzate separatamente da altre colonne in un elenco di campi dell'applicazione client per la creazione di report, in modo che sia più semplice per gli utenti del client individuare i campi appropriati da includere in un report. Per altre informazioni, vedere [Gerarchie &#40;SSAS tabulare&#41;](tabular-models/hierarchies-ssas-tabular.md).  
  
 Per creare le gerarchi viene usata la funzionalità Progettazione modelli in *Vista diagramma*. La creazione e la gestione di gerarchie non sono supportate in Progettazione modelli in Vista dati.  
  
 Tempo previsto per il completamento della lezione: **20 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
 Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato. Prima di eseguire le attività in questa lezione è necessario aver completato la lezione precedente: [Lezione 9: Creare prospettive](lesson-8-create-perspectives.md).  
  
## <a name="create-hierarchies"></a>Creare gerarchie  
  
#### <a name="to-create-a-category-hierarchy-in-the-product-table"></a>Per creare una gerarchia Category nella tabella Product  
  
1.  In Progettazione modelli fare clic sul `Model` menu, scegliere **vista modelli**, quindi fare clic su **vista diagramma**.  
  
    > [!TIP]  
    >  Utilizzare i controlli della mini mappa in alto a destra in Progettazione modelli per modificare la modalità di visualizzazione degli oggetti nella vista diagramma. Se si riposizionano gli oggetti nella vista diagramma, la vista verrà mantenuta quando si salva il progetto.  
  
2.  In Progettazione modelli fare clic con il pulsante destro del mouse sulla `Product` tabella, quindi scegliere **Crea gerarchia**. Verrà visualizzata una nuova gerarchia nella parte inferiore della finestra della tabella.  
  
3.  Nel nome della gerarchia rinominare la gerarchia digitando `Category` e quindi premere INVIO.  
  
4.  Nella `Product` tabella fare clic sulla colonna **Product Category Name** , quindi trascinarla nella `Category` gerarchia e quindi rilasciare il pulsante sopra il `Category` nome.  
  
5.  Nella `Category` gerarchia, fare clic con il pulsante destro del mouse sulla colonna **Product Category Name** , scegliere **Rinomina**, quindi digitare `Category` .  
  
    > [!NOTE]  
    >  La ridenominazione di una colonna in una gerarchia non comporta la ridenominazione della colonna nella tabella. Una colonna in una gerarchia è solo una rappresentazione della colonna nella tabella.  
  
6.  Nella `Product` tabella fare clic con il pulsante destro del mouse sulla colonna **Product Subcategory Name** , scegliere **Aggiungi a gerarchia**dal menu di scelta rapida e quindi fare clic su `Category` .  
  
7.  Rinominare **Product Subcategory Name** in `Subcategory` .  
  
8.  Utilizzando clic e trascina o utilizzando il comando **Aggiungi a gerarchia** nel menu di scelta rapida, aggiungere le colonne **nome modello** e **nome prodotto** (in ordine) e posizionarle sotto la colonna **Product Subcategory Name** . Rinominare queste colonne `Model` e `Product` , rispettivamente.  
  
#### <a name="to-create-hierarchies-in-the-date-table"></a>Per creare gerarchie nella tabella Date  
  
1.  In Progettazione modelli fare clic con il pulsante destro del mouse sulla tabella **Date** e scegliere **Crea gerarchia**.  
  
2.  Rinominare la gerarchia in **Calendar**.  
  
3.  Aggiungere le colonne seguenti, in ordine, quindi rinominarle:  
  
    |Colonna|Rinominare in:|  
    |------------|----------------|  
    |Calendar Year|Year|  
    |Calendar Semester|Semester|  
    |Calendar Quarter|Quarter|  
    |Month Calendar|Month|  
    |Day Of Month|Giorno|  
  
4.  Nella tabella **Date** ripetere i passaggi precedenti, creando una gerarchia **Fiscal** e includendo le colonne seguenti:  
  
    |Colonna|Rinominare in:|  
    |------------|----------------|  
    |Fiscal Year|Year|  
    |Fiscal Semester|Semester|  
    |Fiscal Quarter|Quarter|  
    |Month Calendar|Month|  
    |Day Of Month|Giorno|  
  
5.  Infine, nella tabella **Date** ripetere i passaggi precedenti, creando una gerarchia **Production Calendar** e includendo le colonne seguenti:  
  
    |Colonna|Rinominare in:|  
    |------------|----------------|  
    |Calendar Year|Year|  
    |Week Number Of Year|Settimana|  
    |Day Of Week|Giorno|  
  
## <a name="next-steps"></a>Passaggi successivi  
 Per continuare questa esercitazione, passare alla lezione successiva: [Lezione 11: Creare partizioni](lesson-10-create-partitions.md).  
  
  
