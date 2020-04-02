---
title: Aggiungere gli strumenti di spostamento ai report di Reporting Services per dispositivi mobili | Microsoft Docs
description: In Mobile Report Publisher aggiungere gli strumenti di spostamento per filtrare i dati in base all'ora o alla selezione. Gli strumenti di spostamento sono simili ai filtri dei dati in Power BI e nelle tabelle pivot di Excel.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: e141f50e-49a9-46c6-983c-f656013aa07c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 6749853bc1717077a4d65f4f27546c0fe260cdaf
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "79448206"
---
# <a name="add-navigators-to-reporting-services-mobile-reports"></a>Aggiungere gli strumenti di spostamento ai report di Reporting Services per dispositivi mobili
In [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)], si aggiungono gli *strumenti di spostamento* per filtrare i dati in visualizzazioni in base all'ora o alla selezione. 

Gli strumenti di spostamento sono simili ai filtri dei dati in Power BI e alle tabelle pivot di Excel, ma si distinguono per alcuni elementi univoci.

Gli**strumenti di spostamento basati sul tempo** filtrano le tabelle selezionando le righe che rientrano in un intervallo di tempo specifico. 

Gli**strumenti di spostamento basati sulla selezione** filtrano le tabelle selezionando le righe in cui il valore di una specifica colonna corrisponde al valore di chiave selezionato oppure, nel caso di alberi gerarchici, in cui il valore di una specifica colonna appartiene al sottoalbero del valore della chiave selezionato. Esistono due tipi di strumenti di spostamento di selezione:
* Gli elenchi di selezione sono tabelle a colonna singola che è possibile usare per filtrare il report per dispositivi mobili, in modo analogo ai filtri dei dati in Power BI ed Excel.
* Anche le griglie scorecard filtrano il report per dispositivi mobili e possono contenere 
  
## <a name="time-navigators"></a>Strumenti di spostamento temporali   
  
Come suggerisce il nome, lo strumento di spostamento temporale viene usato per filtrare un intervallo di dati entro un intervallo di tempo.   
  
![SSMRP_TimeNav](../../reporting-services/mobile-reports/media/ssmrp-timenav.png)  
*I quattro grafici a linee sulla sinistra sono impostati in Intervalli di tempo preimpostati. Il grafico a linee sulla destra è il filtro.*  
  
Quando si visualizza il report in anteprima o nel portale Web di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] , si trascinano le frecce nello strumento di spostamento temporale per filtrare la parte restante del report.  
  
![SSMRP_TimeNavPreview](../../reporting-services/mobile-reports/media/ssmrp-timenavpreview.png)  
  
Per impostazione predefinita, lo strumento di spostamento temporale filtra tutti gli oggetti visivi del report connessi ai dati basati sul tempo. Se una tabella contiene più di una colonna basata sul tempo, solo la prima viene usata per le operazioni di filtro. La tabella della serie determina la visualizzazione incorporata e l'intervallo di date generale del report per dispositivi mobili.  
  
È possibile disconnettere una visualizzazione dallo strumento di spostamento temporale.   
1. Selezionare la visualizzazione, quindi selezionare la scheda **Dati** .  
2. In **Proprietà dati**selezionare **Opzioni**.  
3. Deselezionare la casella di controllo **Filtrato in base a** .  
  
   ![SSMRP_ClearTimeFilter](../../reporting-services/mobile-reports/media/ssmrp-cleartimefilter.png)  
  
## <a name="selection-lists"></a>Elenchi di selezione   
  
L'elenco di selezione filtra i dati in un report per dispositivi mobili abbinando il valore selezionato nell'elenco al valore di una colonna specificata per ogni riga di una tabella filtrata. 

1. Dalla scheda **Layout** trascinare **Elenco di selezione** nell'area di progettazione e ridimensionarlo nel modo desiderato.

2. Selezionare la scheda **Dati** e, nel riquadro **Proprietà dati** in **Chiavi**, selezionare la tabella e la colonna che rappresenteranno il filtro. 

3. In **Etichette**selezionare la colonna con l'etichetta che verrà visualizzata. La colonna chiave e la colonna dell'etichetta possono essere la stessa colonna.  
  
   Nel caso dei dati in un albero gerarchico, selezionare una colonna chiave padre.  
  
4. Dopo aver impostato le proprietà dei dati, in **Tabelle Filtrato in base a Elenco di selezione**selezionare le tabelle da filtrare e la colonna in base a cui filtrare. Questa colonna deve avere i valori corrispondenti alla colonna chiave dell'elenco di selezione. 

Per ogni visualizzazione nel report per dispositivi mobili per cui si vuole che l'elenco di selezione applichi il filtro:

1. Selezionare la visualizzazione, selezionare la scheda **Dati** e nel riquadro **Proprietà dati** selezionare **Opzioni** accanto al nome del campo.

   ![mobile-report-set-selection-list](../../reporting-services/mobile-reports/media/mobile-report-set-selection-list.png)

2. In **Filtrato in base a**selezionare l'elenco di selezione.

Quando si visualizza il report per dispositivi mobili in anteprima o nel portale Web di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] e si seleziona un valore nell'elenco di selezione, vengono applicati i filtri alle altre visualizzazioni nel report per dispositivi mobili.

![mobile-report-selection-list-filtering](../../reporting-services/mobile-reports/media/mobile-report-selection-list-filtering.png) 
     
## <a name="scorecard-grid"></a>Griglia scorecard  
  
La griglia scorecard filtra le funzioni in modo analogo all'elenco di selezione, ma visualizza anche le colonne di valore e gli indicatori di punteggio, che corrispondono agli indicatori in una griglia dati indicatore. Dopo aver selezionato la chiave, l'etichetta e le colonne chiave padre facoltative, selezionare una tabella e una colonna di input per fornire dati alla scorecard. La colonna dei dati della scorecard deve essere filtrabile in base alla colonna chiave.  

1. Dalla scheda **Layout** trascinare **Griglia scorecard** nell'area di progettazione e ridimensionarlo nel modo desiderato.

2. Selezionare la scheda **Dati** e, nel riquadro **Proprietà dati** in **Chiavi**, selezionare la tabella e la colonna che rappresenteranno il filtro. 

3. In **Etichette**selezionare la colonna con l'etichetta che verrà visualizzata. La colonna chiave e la colonna dell'etichetta possono essere la stessa colonna.  
  
4. Per aggiungere un indicatore di punteggio, nel riquadro **Data Columns** (Colonne dati) selezionare **Aggiungi punteggio**.   
  
5. Denominare l'indicatore di punteggio e selezionare **Opzioni** per impostare le stesse proprietà che si imposterebbero per un indicatore in una griglia dati:  
  
   * Tipo di misuratore
   * Campo valori
   * Comparison field (Campo per i confronti)
   * Direzione valori
  
6. Per aggiungere un indicatore di valore, nel riquadro **Data Columns** (Colonne dati) selezionare **Aggiungi valore**.

7. Assegnare il nome desiderato all'indicatore di valore, scegliere la colonna di origine nella tabella e selezionare la formattazione.  

   ![mobile-report-scorecard-grid-data-properties](../../reporting-services/mobile-reports/media/mobile-report-scorecard-grid-data-properties.png)

8. Dopo aver impostato le proprietà dei dati, in **Tabelle Filtrato in base a Elenco di selezione**selezionare le tabelle da filtrare e la colonna in base a cui filtrare. Questa colonna deve avere i valori corrispondenti alla colonna chiave dell'elenco di selezione. 

Quando si visualizza il report per dispositivi mobili in anteprima o nel portale Web di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] e si seleziona un valore nella griglia scorecard, vengono applicati i filtri alle altre visualizzazioni nel report per dispositivi mobili.

![mobile-report-scorecard-grid](../../reporting-services/mobile-reports/media/mobile-report-scorecard-grid.png)
    
## <a name="set-which-visualizations-are-filtered"></a>Impostare le visualizzazioni filtrate  
  
Gli elementi della raccolta vengono configurati per l'uso dei filtri facendo clic sul pulsante Opzioni per uno specifico input nella vista dati. I filtri vengono abilitati selezionando la casella di controllo appropriata.  

È possibile decidere quali visualizzazioni nel report per dispositivi mobili verranno filtrate dallo strumento di spostamento:

1. Selezionare la visualizzazione, selezionare la scheda **Dati** e nel riquadro **Proprietà dati** selezionare **Opzioni** accanto al nome del campo.

   ![mobile-report-set-selection-list](../../reporting-services/mobile-reports/media/mobile-report-set-selection-list.png)

2. In **Filtrato in base a**selezionare lo strumento di spostamento. Ogni visualizzazione può essere filtrata in base a più strumenti di spostamento.
  
## <a name="cascading-filters"></a>Filtri a catena   
  
I filtri possono anche essere propagati a catena, in modo che il valore selezionato di uno venga usato per filtrare i valori disponibili in un secondo. Per propagare i filtri a catena, applicare i filtri alla colonna chiave come per un elemento regolare della raccolta.  

### <a name="see-also"></a>Vedere anche 
  
* [Eseguire il mapping nei report di Reporting Services per dispositivi mobili](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)
* [Visualizations to Reporting Services mobile reports (Visualizzazioni nei report per dispositivi mobili di Reporting Services)](../../reporting-services/mobile-reports/add-visualizations-to-reporting-services-mobile-reports.md)
* [Aggiungere indicatori ai report per dispositivi mobili | Reporting Services](../../reporting-services/mobile-reports/add-gauges-to-mobile-reports-reporting-services.md)
* [Aggiungere griglie dei dati al report per dispositivi mobili in Reporting Services](../../reporting-services/mobile-reports/add-data-grids-to-mobile-reports-reporting-services.md)  
