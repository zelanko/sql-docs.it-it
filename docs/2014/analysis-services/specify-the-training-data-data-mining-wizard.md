---
title: Specificare i dati di Training (Creazione guidata di Data Mining dati) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.dm.dmwizard.specifytrainingdata.f1
ms.assetid: cb04deeb-0f89-4bba-b3f1-efccada16825
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c06fb99f8e2104e17d9f6d5f8016b3149ab62c76
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62745851"
---
# <a name="specify-the-training-data-data-mining-wizard"></a>Impostazione dati di training (Creazione guidata modello di data mining)
  Usare la pagina **Impostazione dati di training** per identificare le colonne da includere nella struttura di data mining. È possibile selezionare le colonne da includere nella struttura anche se non vengono utilizzate in tutti i modelli. Ad esempio, se si vuole eseguire il drill-through delle colonne dal modello di data mining, è possibile includerle nella struttura ma non nel modello.  
  
 È necessaria almeno una colonna chiave per ogni tabella inclusa nella struttura. La colonna che si sceglie come chiave dipende dalla tabella (se tabella del case o tabella nidificata). Se è una tabella nidificata, la chiave è spesso anche la colonna stimabile, non la chiave esterna relazionale. Per altre informazioni sulle tabelle annidate, vedere [Tabelle annidate &#40;Analysis Services - Data mining&#41;](data-mining/nested-tables-analysis-services-data-mining.md).  
  
> [!NOTE]  
>  Gli algoritmi di data mining differenti utilizzano le chiavi in modo differente. Per altre informazioni sui diversi tipi di chiavi, vedere [Tipi di contenuto &#40;Data mining&#41;](data-mining/content-types-data-mining.md).  
  
 **Per altre informazioni:** [Strutture di data mining &#40;Analysis Services - Data Mining&#41;](data-mining/mining-structures-analysis-services-data-mining.md), [le colonne del modello di Data Mining](data-mining/mining-model-columns.md), [guidata modello di Data &#40;Analysis Services - dati Mining&#41;](data-mining/data-mining-wizard-analysis-services-data-mining.md), [ Creare una struttura di Data Mining relazionale](data-mining/create-a-relational-mining-structure.md)  
  
## <a name="options"></a>Opzioni  
 **Tabelle/colonne**  
 Consente di visualizzare le tabelle e le colonne selezionate nella pagina precedente della procedura guidata.  
  
 **\<casella di controllo >**  
 Consente di selezionare le colonne da includere nella struttura di data mining.  
  
 Se l'origine dati include tabelle nidificate o più viste, espandere l'elenco delle colonne per visualizzare le tabelle nidificate.  
  
 **Key**  
 Selezionare questa opzione per utilizzare la colonna come identificatore univoco per i dati.  
  
 Per una tabella del case, la chiave è generalmente l'identificatore univoco.  
  
 Per le tabelle annidate, **Key** indica l'identificatore di una riga nel contesto del case associato.  
  
 **Input**  
 Selezionare questa opzione per utilizzare la colonna nella creazione di stime.  
  
> [!NOTE]  
>  Questa colonna è disponibile solo durante la creazione di un modello di data mining insieme alla struttura di data mining.  
  
 **Predictable**  
 Selezionare questa opzione affinché la tabella o la colonna risulti stimabile sulla base di input futuri aggiuntivi.  
  
 Se inoltre si contrassegna tale colonna come stimabile, diventerà stimabile l'intera tabella nidificata. Se nella tabella nidificata non è disponibile alcuna colonna contrassegnata come di input o stimabile, la tabella nidificata verrà visualizzata nella struttura di data mining, ma ignorata nel modello.  
  
 **Nota** Questa colonna è disponibile solo quando si crea un modello di data mining insieme alla struttura di data mining.  
  
 **Suggerisci**  
 Fare clic su questo pulsante per aprire la finestra di dialogo **Suggerisci colonne correlate** , che esegue un'analisi di un campione di dati per identificare le colonne di input che in base al valore di entropia sono più strettamente in relazione con la colonna **Stimabile** selezionata. Questa analisi si applica inoltre alle colonne della tabella nidificata o alle strutture di data mining basate su origini OLAP.  
  
 **Nota** Questa colonna è disponibile solo quando si crea un modello di data mining insieme alla struttura di data mining.  
  
## <a name="see-also"></a>Vedere anche  
 [I dati della Guida F1 di procedura guidata di Data Mining &#40;Analysis Services - Data Mining&#41;](data-mining-wizard-f1-help-analysis-services-data-mining.md)   
 [Suggerisci colonne correlate &#40;Creazione guidata di Data Mining&#41;](suggest-related-columns-data-mining-wizard.md)   
 [Specificare i tipi di tabella &#40;Creazione guidata di Data Mining&#41;](specify-table-types-data-mining-wizard.md)   
 [Specificare il contenuto e il tipo di dati della colonna &#40;Creazione guidata di Data Mining&#41;](specify-the-column-s-content-and-data-type-data-mining-wizard.md)  
  
  
