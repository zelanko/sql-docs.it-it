---
title: 'Lezione 6: creare colonne calcolate | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d126766a-5699-4e9f-8213-8c7eea0fc14e
author: minewiskan
ms.author: owend
ms.openlocfilehash: b39909acacb29f68b0de49ba2093c9b812510172
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84542713"
---
# <a name="lesson-6-create-calculated-columns"></a>Lezione 6: Creare colonne calcolate
  In questa lezione verranno creati nuovi dati nel modello aggiungendo colonne calcolate. Una colonna calcolata è basata sui dati già presenti nel modello. Per altre informazioni, vedere [Colonne calcolate &#40;SSAS tabulare&#41;](tabular-models/ssas-calculated-columns.md).  
  
 Verranno create cinque nuove colonne calcolate in tre tabelle diverse. I passaggi sono leggermente diversi per ogni attività. L'obiettivo è quello di mostrare che vi sono diversi metodi per creare nuove colonne, rinominarle e collocarle in diverse posizioni in una tabella.  
  
 Tempo previsto per il completamento della lezione: **15 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
 Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato. Prima di eseguire le attività in questa lezione è necessario aver completato la lezione precedente: [Lezione 5: Creare relazioni](lesson-4-create-relationships.md).  
  
## <a name="create-calculated-columns"></a>Creare colonne calcolate  
  
#### <a name="create-a-month-calendar-calculated-column-in-the-date-table"></a>Creare una colonna calcolata Month Calendar nella tabella Date  
  
1.  In [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]scegliere **Vista modelli** nel menu **Modello**, quindi fare clic su **Vista dati**.  
  
     Le colonne calcolate possono essere create solo tramite Progettazione modelli in Vista dati.  
  
2.  In Progettazione modelli fare clic sulla tabella (scheda) **Data** .  
  
3.  Fare clic con il pulsante destro del mouse sulla colonna **Calendar Quarter** , quindi scegliere **Inserisci colonna**.  
  
     Una nuova colonna denominata **CalculatedColumn1** verrà inserita a sinistra della colonna **Calendar Quarter** .  
  
4.  Sulla barra della formula sopra la tabella digitare la formula seguente. La funzionalità Completamento automatico è utile per digitare correttamente i nomi completi di colonne e tabelle ed elenca le funzioni disponibili.  
  
     `=RIGHT(" " & FORMAT([Month],"#0"), 2) & " - " & [Month Name]`  
  
     Dopo avere completato la compilazione della formula, premere INVIO.  
  
     I valori vengono quindi popolati per tutte le righe nella colonna calcolata. Se si scorre verso il basso nella tabella, si noterà che le righe possono avere valori diversi per questa colonna, in base ai dati in ogni riga.  
  
    > [!NOTE]  
    >  Se viene visualizzato un errore, verificare che i nomi di colonna nella formula corrispondano ai nomi di colonna modificati in [Lezione 3: Rinominare colonne](rename-columns.md).  
  
5.  Rinominare la colonna in `Month Calendar` .  
  
 La colonna calcolata Month Calendar fornisce un nome ordinabile per il mese.  
  
#### <a name="create-a-day-of-week-calculated-column-in-the-date-table"></a>Creare una colonna calcolata Day of Week nella tabella Date  
  
1.  Con la tabella **Date** ancora attiva, fare clic sul menu **Colonna** , quindi scegliere **Aggiungi colonna**.  
  
     Una nuova colonna verrà aggiunta all'estremità destra della tabella.  
  
2.  Nella barra della formula digitare la formula seguente:  
  
     `=RIGHT(" " & FORMAT([Day Number Of Week],"#0"), 2) & " - " & [Day Name]`  
  
     Dopo avere completato la compilazione della formula, premere INVIO.  
  
3.  Rinominare la colonna in `Day of Week` .  
  
4.  Fare clic sull'intestazione di colonna, quindi trascinare la colonna tra le colonne **Day Name** e **Day of Month** .  
  
    > [!TIP]  
    >  Lo spostamento delle colonne nella tabella semplifica l'esplorazione.  
  
 La colonna calcolata Day of Week fornisce un nome ordinabile per il giorno della settimana.  
  
#### <a name="create-a-product-subcategory-name-calculated-column-in-the-product-table"></a>Creare una colonna calcolata Product Subcategory Name nella tabella Product  
  
1.  In Progettazione modelli selezionare la tabella **Product** .  
  
2.  Scorrere fino all'estremità destra della tabella. Si noti che la colonna all'estrema destra è denominata **Aggiungi colonna** (in corsivo). Fare clic sull'intestazione di colonna.  
  
3.  Nella barra della formula digitare la formula seguente.  
  
     `=RELATED('Product Subcategory'[Product Subcategory Name])`  
  
     Dopo avere completato la compilazione della formula, premere INVIO.  
  
4.  Rinominare la colonna in `Product Subcategory Name` .  
  
 La colonna calcolata Product Subcategory Name viene utilizzata per creare una gerarchia nella tabella Product, che include dati della colonna Product Subcategory Name della tabella Product Subcategory. Le gerarchie non possono essere estese a più di una tabella. La creazione di gerarchie verrà eseguita più avanti, nella lezione 7.  
  
#### <a name="create-a-product-category-name-calculated-column-in-the-product-table"></a>Creare una colonna calcolata Product Category Name nella tabella Product  
  
1.  Con la tabella **Product** ancora attiva, fare clic sul menu **Colonna** , quindi scegliere **Aggiungi colonna**.  
  
2.  Nella barra della formula digitare la formula seguente:  
  
     `=RELATED('Product Category'[Product Category Name])`  
  
     Dopo avere completato la compilazione della formula, premere INVIO.  
  
3.  Rinominare la colonna in `Product Category Name` .  
  
 La colonna calcolata Product Category Name viene utilizzata per creare una gerarchia nella tabella Product, che include dati della colonna Product Category Name della tabella Product Category. Le gerarchie non possono essere estese a più di una tabella.  
  
#### <a name="create-a-margin-calculated-column-in-the-internet-sales-table"></a>Creare una colonna calcolata Margin nella tabella Internet Sales  
  
1.  In Progettazione modelli selezionare la tabella **Internet Sales** .  
  
2.  Aggiungere una nuova colonna.  
  
3.  Nella barra della formula digitare la formula seguente:  
  
     `=[Sales Amount]-[Total Product Cost]`  
  
     Dopo avere completato la compilazione della formula, premere INVIO.  
  
4.  Rinominare la colonna in `Margin` .  
  
5.  Trascinare la colonna tra le colonne **Sales Amount** e **Tax Amt** .  
  
 La colonna calcolata Margin viene utilizzata per analizzare i margini di profitto per ogni riga (prodotto).  
  
## <a name="next-step"></a>passaggio successivo  
 Per continuare questa esercitazione, passare alla lezione successiva: [Lezione 7: Creare misure](lesson-6-create-measures.md).  
  
  
