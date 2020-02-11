---
title: 'Lezione 7: creare misure | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 01bd2ad7-09b7-49ae-ad80-83f25da301aa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ef207028ab1b4f6bc084f3f4e515ae37630b771d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66078425"
---
# <a name="lesson-7-create-measures"></a>Lezione 7: Creare misure
  In questa lezione verranno create misure da includere nel modello. Analogamente alle colonne calcolate create nella lezione precedente, una misura è essenzialmente un calcolo creato utilizzando una formula DAX. Tuttavia, a differenza delle colonne calcolate, le misure vengono valutate in base a un *filtro* selezionato dall'utente, ad esempio, una particolare colonna o filtro dei dati aggiunto al campo Etichette di riga in una tabella pivot.   Con la misura applicata viene quindi calcolato un valore per ogni cella nel filtro. Le misure sono calcoli potenti e flessibili che può essere utile includere in pressoché tutti i modelli tabulari per eseguire calcoli dinamici sui dati numerici. Per altre informazioni, vedere [Misure &#40;SSAS tabulare&#41;](tabular-models/measures-ssas-tabular.md).  
  
 Per creare misure, è necessario utilizzare la griglia delle misure. Per impostazione predefinita, ogni tabella ha una griglia delle misure vuota, ma di solito non si creano misure per ogni tabella. La griglia delle misure viene visualizzata sotto una tabella di Progettazione modelli se si trova in Vista dati. Per mostrare o nascondere la griglia delle misure per una tabella, fare clic sul menu **Tabella** e quindi fare clic su **Mostra griglia delle misure**.  
  
 È possibile creare una misura facendo clic su una cella vuota nella griglia delle misure e quindi digitando una formula DAX nella barra della formula. Quando si preme INVIO per completare la formula, la misura verrà quindi visualizzata nella cella. È anche possibile creare misure con una funzione di aggregazione standard facendo clic su una colonna e quindi sul pulsante Somma automatica (**∑**) sulla barra degli strumenti. Le misure create utilizzando la funzionalità Somma automatica vengono visualizzate nella cella della griglia delle misure sotto la colonna, tuttavia, se necessario, possono essere spostate.  
  
 In questa lezione verranno create misure sia immettendo una formula DAX sulla barra della formula che utilizzando la funzionalità Somma automatica.  
  
 Tempo stimato per il completamento della lezione: **30 minuti**  
  
## <a name="prerequisites"></a>Prerequisites  
 Questo argomento fa parte di un'esercitazione sulla creazione di modelli tabulari, con lezioni che è consigliabile completare nell'ordine indicato. Prima di eseguire le attività in questa lezione è necessario aver completato la lezione precedente: [Lezione 6: Creare colonne calcolate](lesson-5-create-calculated-columns.md).  
  
## <a name="create-measures"></a>Creare misure  
  
#### <a name="to-create-a-days-current-quarter-to-date-measure-in-the-date-table"></a>Per creare una misura Days Current Quarter to Date nella tabella Date  
  
1.  In Progettazione modelli fare clic sulla tabella **date** .  
  
2.  Se sotto la tabella non è già visualizzata una griglia delle misure vuota, fare clic sul menu **Tabella**, quindi su **Mostra griglia delle misure**.  
  
3.  Nella griglia delle misure fare clic sulla cella vuota in alto a sinistra.  
  
4.  Nella barra della formula sopra la tabella digitare la formula seguente:  
  
     `=COUNTROWS( DATESQTD( 'Date'[Date]))`  
  
     Dopo avere completato la compilazione della formula, premere INVIO.  
  
     Si noti che la cella in alto a sinistra contiene ora un nome di misura, **Measure 1**, seguito dal risultato **30**. Il nome di misura precede inoltre la formula sulla barra della formula.  
  
5.  Per rinominare la misura, nella barra della formula evidenziare il nome, **Measure 1**, quindi digitare `Days Current Quarter to Date`, quindi premere INVIO.  
  
    > [!TIP]  
    >  Quando si digita una formula sulla barra della formula, è anche possibile digitare innanzitutto il nome della misura seguito dai due punti (:), quindi uno spazio e infine la formula. Utilizzando questo metodo, non è necessario rinominare la misura.  
  
#### <a name="to-create-a-days-in-current-quarter-measure-in-the-date-table"></a>Per creare una misura Days in Current Quarter nella tabella Date  
  
1.  Con la tabella **Date** ancora attiva in Progettazione modelli, fare clic sulla cella vuota nella griglia delle misure sotto la misura appena creata.  
  
2.  Nella barra della formula digitare la formula seguente:  
  
     `Days in Current Quarter :=COUNTROWS( DATESBETWEEN( 'Date'[Date], STARTOFQUARTER( LASTDATE('Date'[Date])), ENDOFQUARTER('Date'[Date])))`  
  
     Si noti che in questa formula è stato innanzitutto incluso il nome della misura seguito da due punti (:).  
  
     Dopo avere completato la compilazione della formula, premere INVIO.  
  
 Quando si crea un rapporto di confronto tra un periodo incompleto e il periodo precedente, la formula deve tenere conto della proporzione del periodo trascorso e confrontarla con la stessa proporzione del periodo precedente. In questo caso, [Days Current Quarter to Date]/[Days in Current Quarter] fornisce la proporzione trascorsa nel periodo corrente.  
  
#### <a name="to-create-an-internet-distinct-count-sales-order-measure-in-the-internet-sales-table"></a>Per creare una misura Internet Distinct Count Sales Order nella tabella Internet Sales  
  
1.  In Progettazione modelli fare clic sulla tabella (scheda) **Internet Sales** .  
  
     Se la griglia delle misure non è già visualizzata, fare clic con il pulsante destro del mouse sulla tabella (scheda) **Internet Sales**, quindi scegliere **Mostra griglia delle misure**.  
  
2.  Fare clic sull'intestazione di colonna **Sales Order Number**.  
  
3.  Sulla barra degli strumenti fare clic sulla freccia in giù accanto a Somma automatica (**∑**) e quindi selezionare **DistinctCount**.  
  
     La funzionalità Somma automatica crea automaticamente una misura per la colonna selezionata usando la formula di aggregazione standard DistinctCount.  
  
     Si noti che la cella superiore sotto la colonna nella griglia delle misure contiene ora un nome di misura, **Distinct Count Sales Order Number**. Le misure create utilizzando la funzionalità Somma automatica vengono posizionate automaticamente nella cella di livello superiore nella griglia delle misure sotto la colonna associata.  
  
4.  Nella griglia delle misure fare clic sulla nuova misura, quindi nella finestra **Proprietà** in **Nome misura** rinominare la misura in **Internet Distinct Count Sales Order**.  
  
#### <a name="to-create-additional-measures-in-the-internet-sales-table"></a>Per creare misure aggiuntive nella tabella Internet Sales  
  
1.  Usare la funzionalità Somma automatica e creare le misure seguenti con i nomi indicati:  
  
    |Nome misura|Colonna|Somma automatica (∑)|Formula|  
    |------------------|------------|-------------------|-------------|  
    |Internet Order Lines Count|Sales Order Line Number|Conteggio|=COUNT([Sales Order Line Number])|  
    |Internet Total Units|Order Quantity|SUM|=SUM([Order Quantity])|  
    |Internet Total Discount Amount|Discount Amount|SUM|=SUM([Discount Amount])|  
    |Internet Total Product Cost|Total Product Cost|SUM|=SUM([Total Product Cost])|  
    |Internet Total Sales|Sales Amount|SUM|=SUM([Sales Amount])|  
    |Internet Total Margin|Margin|SUM|=SUM([Margin])|  
    |Internet Total Tax Amt|Tax Amt|SUM|=SUM([Tax Amt])|  
    |Internet Total Freight|Freight|SUM|=SUM([Freight])|  
  
2.  Facendo clic su una cella vuota nella griglia delle misure e utilizzando la barra della formula è possibile creare le misure seguenti e assegnare loro un nome:  
  
    > [!IMPORTANT]  
    >  È necessario creare le misure seguenti in ordine. Le formule delle misure elencate alla fine fanno riferimento alle misure elencate all'inizio.  
  
    |Nome misura|Formula|  
    |------------------|-------------|  
    |Internet Previous Quarter Margin|=CALCULATE([Internet Total Margin],PREVIOUSQUARTER('Date'[Date]))|  
    |Internet Current Quarter Margin|=TOTALQTD([Internet Total Margin],'Date'[Date])|  
    |Internet Previous Quarter Margin Proportion to QTD|=[Internet Previous Quarter Margin]*([Days Current Quarter to Date]/[Days In Current Quarter])|  
    |Internet Previous Quarter Sales|=CALCULATE([Internet Total Sales],PREVIOUSQUARTER('Date'[Date]))|  
    |Internet Current Quarter Sales|=TOTALQTD([Internet Total Sales],'Date'[Date])|  
    |Internet Previous Quarter Sales Proportion to QTD|=[Internet Previous Quarter Sales]*([Days Current Quarter to Date]/[Days In Current Quarter])|  
  
 Le misure create per la tabella Internet Sales possono essere utilizzate per analizzare dati finanziari critici, quali vendite, costi e margine di profitto per elementi definiti dal filtro selezionato dall'utente.  
  
## <a name="next-step"></a>passaggio successivo  
 Per continuare questa esercitazione, passare alla lezione successiva, [Lezione 8: Creare indicatori di prestazioni chiave](lesson-7-create-key-performance-indicators.md).  
  
  
