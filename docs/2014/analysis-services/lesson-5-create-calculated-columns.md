---
title: 'Lezione 6: Creare colonne calcolate | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: d126766a-5699-4e9f-8213-8c7eea0fc14e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: adc7b7bf3335c8c9c7530d18f4d553492cfe9e1b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62728645"
---
# <a name="lesson-6-create-calculated-columns"></a>Lezione 6: Creare colonne calcolate
  In questa lezione verranno creati nuovi dati nel modello aggiungendo colonne calcolate. Una colonna calcolata è basata sui dati già presenti nel modello. Per altre informazioni, vedere [Colonne calcolate &#40;SSAS tabulare&#41;](tabular-models/ssas-calculated-columns.md).  
  
 Verranno create cinque nuove colonne calcolate in tre tabelle diverse. I passaggi sono leggermente diversi per ogni attività. L'obiettivo è quello di mostrare che vi sono diversi metodi per creare nuove colonne, rinominarle e collocarle in diverse posizioni in una tabella.  
  
 Tempo stimato per il completamento della lezione: **15 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  
 Questo argomento fa parte di un'esercitazione relativa alla modellazione tabulare che deve essere completata nell'ordine specificato. Prima di eseguire le attività in questa lezione, è necessario avere completato la lezione precedente: [Lezione 5: Creare relazioni](lesson-4-create-relationships.md).  
  
## <a name="create-calculated-columns"></a>Creare colonne calcolate  
  
#### <a name="create-a-month-calendar-calculated-column-in-the-date-table"></a>Creare una colonna calcolata Month Calendar nella tabella Date  
  
1.  In [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] scegliere **Vista modelli** nel menu **Modello**, quindi fare clic su **Vista dati**.  
  
     Le colonne calcolate possono essere create solo tramite Progettazione modelli in Vista dati.  
  
2.  In Progettazione modelli fare clic sulla tabella (scheda) **Data** .  
  
3.  Fare doppio clic il **Calendar Quarter** colonna e quindi fare clic su **Inserisci colonna**.  
  
     Una nuova colonna denominata **CalculatedColumn1** verrà inserita a sinistra del **Calendar Quarter** colonna.  
  
4.  Sulla barra della formula sopra la tabella digitare la formula seguente. La funzionalità Completamento automatico consente di digitare i nomi completi di colonne e tabelle ed elencare le funzioni disponibili.  
  
     `=RIGHT(" " & FORMAT([Month],"#0"), 2) & " - " & [Month Name]`  
  
     Dopo avere completato la compilazione della formula, premere INVIO.  
  
     I valori vengono quindi popolati per tutte le righe nella colonna calcolata. Scorrendo la tabella verso il basso, si vedrà che le righe possono avere valori diversi per questa colonna, in base ai dati presenti in ogni riga.  
  
    > [!NOTE]  
    >  Se si riceve un errore, verificare i nomi di colonna nella formula corrispondano ai nomi di colonna modificati in [lezione 3: Rinominare le colonne](rename-columns.md).  
  
5.  Rinominare la colonna `Month Calendar`.  
  
 La colonna calcolata Month Calendar fornisce un nome ordinabile per il mese.  
  
#### <a name="create-a-day-of-week-calculated-column-in-the-date-table"></a>Creare una colonna calcolata Day of Week nella tabella Date  
  
1.  Con la tabella **Date** ancora attiva, fare clic sul menu **Colonna** , quindi scegliere **Aggiungi colonna**.  
  
     Una nuova colonna verrà aggiunta all'estremità destra della tabella.  
  
2.  Sulla barra della formula digitare la formula seguente:  
  
     `=RIGHT(" " & FORMAT([Day Number Of Week],"#0"), 2) & " - " & [Day Name]`  
  
     Dopo avere completato la compilazione della formula, premere INVIO.  
  
3.  Rinominare la colonna in `Day of Week`.  
  
4.  Fare clic sull'intestazione di colonna, quindi trascinare la colonna tra le colonne **Day Name** e **Day of Month** .  
  
    > [!TIP]  
    >  Lo spostamento delle colonne nella tabella semplifica l'esplorazione.  
  
 La colonna calcolata Day of Week fornisce un nome ordinabile per il giorno della settimana.  
  
#### <a name="create-a-product-subcategory-name-calculated-column-in-the-product-table"></a>Creare una colonna calcolata Product Subcategory Name nella tabella Product  
  
1.  In Progettazione modelli selezionare la tabella **Product** .  
  
2.  Scorrere fino all'estremità destra della tabella. Si noti che la colonna all'estrema destra è denominata **Aggiungi colonna** (in corsivo). Fare clic sull'intestazione di colonna.  
  
3.  Sulla barra della formula digitare la formula seguente.  
  
     `=RELATED('Product Subcategory'[Product Subcategory Name])`  
  
     Dopo avere completato la compilazione della formula, premere INVIO.  
  
4.  Rinominare la colonna in `Product Subcategory Name`.  
  
 La colonna calcolata Product Subcategory Name viene utilizzata per creare una gerarchia nella tabella Product, che include dati della colonna Product Subcategory Name della tabella Product Subcategory. Le gerarchie non possono estendersi in più di una tabella. La creazione di gerarchie verrà eseguita più avanti, nella lezione 7.  
  
#### <a name="create-a-product-category-name-calculated-column-in-the-product-table"></a>Creare una colonna calcolata Product Category Name nella tabella Product  
  
1.  Con la tabella **Product** ancora attiva, fare clic sul menu **Colonna** , quindi scegliere **Aggiungi colonna**.  
  
2.  Sulla barra della formula digitare la formula seguente:  
  
     `=RELATED('Product Category'[Product Category Name])`  
  
     Dopo avere completato la compilazione della formula, premere INVIO.  
  
3.  Rinominare la colonna in `Product Category Name`.  
  
 La colonna calcolata Product Category Name viene utilizzata per creare una gerarchia nella tabella Product, che include dati della colonna Product Category Name della tabella Product Category. Le gerarchie non possono estendersi in più di una tabella.  
  
#### <a name="create-a-margin-calculated-column-in-the-internet-sales-table"></a>Creare una colonna calcolata Margin nella tabella Internet Sales  
  
1.  In Progettazione modelli selezionare la tabella **Internet Sales** .  
  
2.  Aggiungere una nuova colonna.  
  
3.  Sulla barra della formula digitare la formula seguente:  
  
     `=[Sales Amount]-[Total Product Cost]`  
  
     Dopo avere completato la compilazione della formula, premere INVIO.  
  
4.  Rinominare la colonna in `Margin`.  
  
5.  Trascinare la colonna tra le colonne **Sales Amount** e **Tax Amt** .  
  
 La colonna calcolata Margin viene utilizzata per analizzare i margini di profitto per ogni riga (prodotto).  
  
## <a name="next-step"></a>Passaggio successivo  
 Per continuare questa esercitazione, passare alla lezione successiva: [Lezione 7: Creare misure](lesson-6-create-measures.md).  
  
  
