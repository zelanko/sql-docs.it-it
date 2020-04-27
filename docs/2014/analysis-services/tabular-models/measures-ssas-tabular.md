---
title: Misure (SSAS tabulare) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 27ec8f99-e9ef-44c9-a83f-f7c88e128ad3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c1ca545e081826f1b81117e377f370136a7b4998
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66067004"
---
# <a name="measures-ssas-tabular"></a>Misure (SSAS tabulare)
  Nei modelli tabulari una misura è un calcolo creato utilizzando una formula DAX per l'utilizzo in un client di creazione report. Le misure vengono valutate in base ai campi, ai filtri e ai filtri dei dati selezionati dagli utenti nell'applicazione client di creazione report.  
  
 Sezioni dell'argomento:  
  
-   [Vantaggi](#bkmk_understanding)  
  
-   [Definizione delle misure tramite la relativa griglia](#bkmk_def_mg)  
  
-   [Proprietà delle misure](#bkmk_properties)  
  
-   [Utilizzo di una misura in un indicatore KPI](#bkmk_KPI)  
  
-   [Attività correlate](#bkmk_rel_tasks)  
  
##  <a name="benefits"></a><a name="bkmk_understanding"></a>Vantaggi  
 Le misure possono essere basate sulle funzioni di aggregazione standard, ad esempio AVERAGE, COUNT o SUM. In alternativa, è possibile definire formule personalizzate tramite DAX. Oltre alla formula, ogni misura dispone di proprietà definite dal tipo di dati della misura, ad esempio Nome, Dettagli tabella, Formato e Cifre decimali.  
  
 Quando le misure sono state definite in un modello, gli utenti possono aggiungerle a un report o una tabella pivot. A seconda delle prospettive e dei ruoli, le misure vengono visualizzate nell'elenco dei campi con la relativa tabella associata e sono disponibili per tutti gli utenti del modello. In genere, le misure vengono create nelle tabelle dei fatti, tuttavia possono anche essere indipendenti dalla tabella alla quale sono associate.  
  
 È importante comprendere le differenze fondamentali tra una colonna calcolata e una misura. In una colonna calcolata una formula restituisce un valore per ogni riga. In una tabella FactSales, ad esempio, una colonna calcolata denominata TotalProfit a cui è associata la formula seguente consente di calcolare un valore per il profitto totale per ogni riga (una riga per vendita) della tabella FactSales:  
  
```  
=[SalesAmount] - [TotalCost] - [ReturnAmount]  
```  
  
 La colonna calcolata TotalProfit può quindi essere utilizzata in uno strumento client di creazione report come qualsiasi altra colonna.  
  
 Una misura, d'altro canto, restituisce un valore in base alla selezione di un utente, ovvero un contesto di filtro impostato in una tabella pivot o in un report. Ad esempio, una misura della tabella FactSales viene creata con la formula seguente:  
  
```  
Sum of TotalProfit: =SUM([TotalProfit])  
```  
  
 Un analista delle vendite desidera conoscere il profitto totale per una categoria di prodotti utilizzando Excel. Ogni categoria di prodotti è costituita da più prodotti. L'analista delle vendite seleziona la colonna ProductCategoryName e la aggiunge alla finestra del filtro Etichette di riga di una tabella pivot; in quest'ultima viene quindi visualizzata una riga per ogni categoria di prodotti. Successivamente l'utente seleziona la misura Sum of TotalProfit. Per impostazione predefinita verrà aggiunta una misura alla finestra del filtro Valori. La misura consente di calcolare la somma del profitto totale e di visualizzare i risultati per ogni categoria di prodotti. L'analista delle vendite può quindi filtrare ulteriormente la somma del profitto totale per ogni categoria di prodotti tramite un filtro dei dati, ad esempio aggiungendo CalendarYear come filtro dei dati per visualizzare la somma del profitto totale per ogni categoria di prodotti in base all'anno.  
  
|ProductCategoryName|Sum of TotalProfit|  
|-------------------------|------------------------|  
|Audio|$2,731,061,308.69|  
|Cameras and Camcorders (Fotocamere e cineprese)|$620,623,675.75|  
|Computers (Computer)|$392,999,044.59|  
|Tv and Video (Tv e video)|$946,989,702.51|  
|**Grand Total**|**$4,691,673,731.53**|  
  
##  <a name="defining-measures-by-using-the-measure-grid"></a><a name="bkmk_def_mg"></a>Definizione delle misure tramite la griglia delle misure  
 Le misure vengono create in fase di progettazione tramite la relativa griglia in Progettazione modelli. Ogni tabella dispone di una griglia delle misure. Per impostazione predefinita, la griglia delle misure viene visualizzata sotto ogni tabella in Progettazione modelli. È inoltre possibile scegliere di non visualizzare la griglia delle misure per una determinata tabella. Per abilitare o disabilitare la visualizzazione della griglia delle misure di una tabella, fare clic sul menu **tabella** , quindi su **Mostra griglia delle misure**.  
  
 Nella griglia delle misure è possibile creare misure nelle modalità seguenti:  
  
-   Fare clic su una cella vuota della griglia delle misure, quindi digitare una formula DAX nella barra della formula. Quando si preme INVIO per completare la formula, la misura viene visualizzata nella cella della griglia delle misure.  
  
-   Creare una misura utilizzando una funzione di aggregazione standard facendo clic su una colonna, quindi sul pulsante Somma automatica (∑) nella barra degli strumenti e, infine, su una funzione di aggregazione standard. Le aggregazioni standard sono: Sum, Average, Count, DistinctCount, Max, Min. Le misure create utilizzando il pulsante Somma automatica verranno sempre visualizzate direttamente nella griglia delle misure, sotto la colonna.  
  
 Per impostazione predefinita, quando si utilizza la somma automatica, il nome della misura viene definito in base al nome della colonna associata, seguito da due punti e successivamente dalla formula. Il nome può essere modificato nella barra della formula o nell'impostazione della proprietà **Nome misura** nella finestra Proprietà. Quando si crea una misura tramite una formula personalizzata, è possibile digitare un nome nella barra della formula, seguito da due punti e successivamente dalla formula oppure è possibile digitare un nome nell'impostazione delle proprietà **Nome misura** della finestra Proprietà.  
  
 È importante denominare accuratamente le misure. Il nome della misura verrà visualizzato con la tabella associata nell'elenco dei campi dello strumento client di creazione report. In base alla misura base verrà denominato anche un indicatore KPI. Una misura non può avere lo stesso nome di una colonna di qualsiasi tabella del modello.  
  
> [!TIP]  
>  È possibile raggruppare le misure di più tabelle in un'unica tabella creando una tabella vuota e quindi spostando o creando al suo interno le nuove misure. Tenere presente che potrebbe essere necessario includere i nomi di tabella nelle formule DAX per fare riferimento alle colonne in altre tabelle.  
  
 Se sono state definite prospettive per il modello, le misure non vengono aggiunte automaticamente a qualsiasi prospettiva. È necessario aggiungere manualmente misure a una prospettiva tramite la finestra di dialogo Prospettive. Per altre informazioni, vedere [Prospettive &#40;SSAS tabulare&#41;](perspectives-ssas-tabular.md).  
  
##  <a name="measure-properties"></a><a name="bkmk_properties"></a>Proprietà misura  
 Ogni misura dispone di proprietà che ne consentono la definizione. Le proprietà delle misure, insieme a quelle della colonna associata, possono essere modificate nella finestra Proprietà. Di seguito sono riportate le proprietà delle misure:  
  
|Proprietà|Impostazione predefinita|Descrizione|  
|--------------|---------------------|-----------------|  
|**Descrizione**|Vuoto|Descrizione della misura. La descrizione non verrà visualizzata con la misura in uno strumento client di creazione report.|  
|**Formato**|Determinato automaticamente in base al tipo di dati della colonna a cui viene fatto riferimento nell'espressione della formula.|Formato della misura, ad esempio, valuta o percentuale.|  
|**Formula**|Formula immessa nella relativa barra quando è stata creata la misura.|Formula della misura.|  
|**Nome misura**|Se viene utilizzata la somma automatica, il nome della misura precederà il nome della colonna seguito da due punti. Se viene immessa una formula personalizzata, digitare un nome seguito da due punti, quindi la formula.|Nome della misura come viene visualizzato nell'elenco dei campi di uno strumento client di creazione report.|  
  
##  <a name="using-a-measure-in-a-kpi"></a><a name="bkmk_KPI"></a>Utilizzo di una misura in un indicatore KPI  
 Un indicatore KPI (indicatore di prestazioni chiave) viene definito mediante un valore *base* , definito tramite una misura, rispetto a un valore di *destinazione* , anch'esso definito tramite una misura o un valore assoluto. In un indicatore KPI è incluso anche lo *stato*, ovvero un calcolo della restituzione del valore base rispetto al valore di destinazione tra i valori di soglia, visualizzato in formato grafico. Gli indicatori KPI vengono spesso utilizzati dai professionisti aziendali per identificare le tendenze nella metrica aziendale critica.  
  
 Qualsiasi misura può essere utilizzata come misura base di un indicatore KPI. Per creare un indicatore KPI, nella griglia delle misure fare clic con il pulsante destro del mouse su una misura e quindi selezionare **Crea KPI**. Verrà visualizzata la finestra di dialogo relativa all'indicatore di prestazioni chiave in cui è possibile specificare un valore di destinazione (definito tramite una misura o un valore assoluto), nonché definire i valori di soglia dello stato e un tipo di grafico. Per altre informazioni, vedere [Indicatori KPI &#40;SSAS tabulare&#41;](kpis-ssas-tabular.md).  
  
##  <a name="related-tasks"></a><a name="bkmk_rel_tasks"></a> Attività correlate  
  
|Argomento|Descrizione|  
|-----------|-----------------|  
|[Creare e gestire misure &#40;SSAS tabulare&#41;](measures-ssas-tabular.md)|Viene descritto come creare e gestire misure utilizzando la griglia delle misure in Progettazione modelli.|  
  
## <a name="see-also"></a>Vedi anche  
 [Indicatori KPI &#40;&#41;tabulare SSAS](kpis-ssas-tabular.md)   
 [Creare e gestire indicatori KPI &#40;SSAS tabulare&#41;](create-and-manage-kpis-ssas-tabular.md)   
 [Colonne calcolate &#40;SSAS tabulare&#41;](ssas-calculated-columns.md)  
  
  
