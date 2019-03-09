---
title: 'Analysis Services tutorial-lezione 5: Creare colonne calcolate | Microsoft Docs'
ms.date: 03/08/2019
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: d1e2c4df54313ecc66e5e49904bdc40393c410f7
ms.sourcegitcommit: 0a7beb2f51e48889b4a85f7c896fb650b208eb36
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/09/2019
ms.locfileid: "57685558"
---
# <a name="create-calculated-columns"></a>Creare colonne calcolate

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

In questa lezione, creare i dati nel modello aggiungendo colonne calcolate. È possibile creare colonne calcolate (come colonne personalizzate) quando si usa recupera dati, usando l'Editor di Query o, più avanti in questo tipo di finestra di progettazione modello descritto di seguito. Per altre informazioni, vedere [colonne calcolate](../tabular-models/ssas-calculated-columns.md).
  
Create cinque nuove colonne calcolate in tre tabelle diverse. I passaggi sono leggermente diversi per ogni attività che illustra diversi modi per creare colonne, rinominarle e inserirle in diverse posizioni in una tabella.  

In questa lezione è anche in cui si utilizza innanzitutto Data Analysis Expressions (DAX). DAX è un linguaggio speciale per la creazione di espressioni formule altamente personalizzabili per i modelli tabulari. In questa esercitazione si usano DAX per creare colonne calcolate, misure e filtri di ruolo. Per altre informazioni, vedere [DAX nei modelli tabulari](../tabular-models/understanding-dax-in-tabular-models-ssas-tabular.md). 
  
Tempo stimato per il completamento della lezione: **15 minuti**  
  
## <a name="prerequisites"></a>Prerequisiti  

Questo articolo fa parte di un'esercitazione di modellazione tabulare, che deve essere completata nell'ordine. Prima di eseguire le attività in questa lezione, è necessario avere completato la lezione precedente: [Lezione 4: Creare relazioni](../tutorial-tabular-1400/as-lesson-4-create-relationships.md). 
  
## <a name="create-calculated-columns"></a>Creare colonne calcolate  
  
#### <a name="create-a-monthcalendar-calculated-column-in-the-dimdate-table"></a>Creare una colonna calcolata MonthCalendar nella tabella DimDate  
  
1.  Fare clic sui **Model** menu > **visualizzazione modello** > **vista dati**.  
  
    Le colonne calcolate possono essere create solo tramite Progettazione modelli in Vista dati.  
  
2.  In Progettazione modelli, scegliere il **DimDate** tabella (scheda).  
  
3.  Fare doppio clic il **CalendarQuarter** intestazione di colonna e quindi fare clic su **Inserisci colonna**.  
  
    Una nuova colonna denominata **CalculatedColumn1** verrà inserita a sinistra della colonna **Calendar Quarter** .  
  
4.  Nella barra della formula sopra la tabella digitare la formula DAX seguente: La funzionalità Completamento automatico consente di digitare i nomi completi di colonne e tabelle ed elencare le funzioni disponibili.  
  
    ```  
    =RIGHT(" " & FORMAT([MonthNumberOfYear],"#0"), 2) & " - " & [EnglishMonthName]  
    ``` 
  
    I valori vengono quindi popolati per tutte le righe nella colonna calcolata. Se si scorre verso il basso nella tabella, noterete che le righe possono avere valori diversi per questa colonna, in base ai dati in ogni riga.    
  
5.  Rinominare la colonna **MonthCalendar**. 

    ![as-lesson5-newcolumn](../tutorial-tabular-1400/media/as-lesson5-newcolumn.png) 
  
La colonna calcolata MonthCalendar fornisce un nome ordinabile per il mese.  
  
#### <a name="create-a-dayofweek-calculated-column-in-the-dimdate-table"></a>Creare una colonna calcolata DayOfWeek nella tabella DimDate  
  
1.  Con il **DimDate** ancora attiva, fare clic sul tabella le **colonna** dal menu e quindi fare clic su **Aggiungi colonna**.  
  
2.  Sulla barra della formula digitare la formula seguente:  
    
    ```
    =RIGHT(" " & FORMAT([DayNumberOfWeek],"#0"), 2) & " - " & [EnglishDayNameOfWeek]  
    ```
    
    Al termine della compilazione della formula, premere INVIO. La nuova colonna verrà aggiunta all'estremità destra della tabella.  
  
3.  Rinominare la colonna **DayOfWeek**.  
  
4.  Fare clic sull'intestazione di colonna e quindi trascinare la colonna tra le **EnglishDayNameOfWeek** colonna e il **DayNumberOfMonth** colonna.  
  
    > [!TIP]  
    > Lo spostamento delle colonne nella tabella semplifica l'esplorazione.  
  
La colonna calcolata DayOfWeek fornisce un nome ordinabile per il giorno della settimana.  
  
#### <a name="create-a-productsubcategoryname-calculated-column-in-the-dimproduct-table"></a>Creare una colonna calcolata ProductSubcategoryName nella tabella DimProduct  
  
  
1.  Nel **DimProduct** tabella, scorrere fino all'estrema destra della tabella. Si noti che la colonna all'estrema destra è denominata **Aggiungi colonna** (in corsivo). Fare clic sull'intestazione di colonna.  
  
2.  Sulla barra della formula digitare la formula seguente:  
    
    ```
    =RELATED('DimProductSubcategory'[EnglishProductSubcategoryName])  
    ```
  
3.  Rinominare la colonna **ProductSubcategoryName**.  
  
La colonna calcolata ProductSubcategoryName viene usata per creare una gerarchia nella tabella DimProduct che include i dati dalla colonna EnglishProductSubcategoryName nella tabella DimProductSubcategory. Le gerarchie non possono estendersi in più di una tabella. Creare gerarchie in un secondo momento nella lezione 9.  
  
#### <a name="create-a-productcategoryname-calculated-column-in-the-dimproduct-table"></a>Creare una colonna calcolata ProductCategoryName nella tabella DimProduct  
  
1.  Con il **DimProduct** ancora attiva, fare clic sul tabella le **colonna** dal menu e quindi fare clic su **Aggiungi colonna**.  
  
2.  Sulla barra della formula digitare la formula seguente:  
  
    ```
    =RELATED('DimProductCategory'[EnglishProductCategoryName]) 
    ```
    
3.  Rinominare la colonna **ProductCategoryName**.  
  
La colonna calcolata ProductCategoryName viene usata per creare una gerarchia nella tabella DimProduct che include i dati dalla colonna EnglishProductCategoryName nella tabella DimProductCategory. Le gerarchie non possono estendersi in più di una tabella.  
  
#### <a name="create-a-margin-calculated-column-in-the-factinternetsales-table"></a>Creare una colonna calcolata Margin nella tabella FactInternetSales  
  
1.  Nella finestra di progettazione modelli selezionare la **FactInternetSales** tabella.  
  
2.  Creare una nuova colonna calcolata tra il **SalesAmount** colonna e il **TaxAmt** colonna.  
  
3.  Sulla barra della formula digitare la formula seguente:  
  
    ```
    =[SalesAmount]-[TotalProductCost]
    ``` 

4.  Rinominare la colonna in **Margin**.  
 
      ![as-lesson5-newmargin](../tutorial-tabular-1400/media/as-lesson5-newmargin.png)
      
    La colonna calcolata Margin viene usata per analizzare i margini di profitto per ogni vendita.  
  
## <a name="whats-next"></a>Quali sono le operazioni successive?

[Lezione 6: Creare misure](../tutorial-tabular-1400/as-lesson-6-create-measures.md).
  
  
  
