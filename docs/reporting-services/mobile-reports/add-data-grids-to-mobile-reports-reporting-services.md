---
title: Aggiungere griglie dati a report per dispositivi mobili | Reporting Services | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: fe98a970-90d3-44d1-9189-9141c237f141
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 2658eb0eec1bd99c4e4503e8d8ae8894638e8c23
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63280447"
---
# <a name="add-data-grids-to-mobile-reports--reporting-services"></a>Aggiungere griglie dati a report per dispositivi mobili | Reporting Services
La visualizzazione migliore, talvolta, è proprio quella dei dati. Per visualizzare i dati in *sono disponibili tre*griglie dati [!INCLUDE[SS_MobileReptPub_Long](../../includes/ss-mobilereptpub-long.md)], o tabelle:
* Griglia dati semplice
* Griglia dati indicatore
* Griglia dati grafico

## <a name="simple-data-grid"></a>Griglia dati semplice
La griglia dati più basilare, ovvero la griglia dati semplice, può visualizzare più colonne di dati con formattazione e intestazioni personalizzate. 

![mobile-report-simple-data-grid](../../reporting-services/mobile-reports/media/mobile-report-simple-data-grid.png)

Dopo aver aggiunto una griglia dati nell'area di progettazione, è possibile connetterla a dati reali.

1. Trascinare una griglia dati semplice dalla scheda **Layout** alla griglia di struttura e impostare le dimensioni desiderate.

2. Filtrare [i dati da Excel o da un set di dati condiviso](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md).

3. Selezionare la scheda **Dati** e nel riquadro **Proprietà dati** , in **Dati per la visualizzazione griglia** selezionare una tabella dati.

4. Ne riquadro **Colonne** selezionare le colonne desiderate. Riordinarle, rinominarle e impostarne il formato e l'aggregazione. 

 
##  <a name="indicator-data-grid"></a>Griglia dati indicatore
A una griglia dati indicatore è possibile aggiungere colonne con misuratori.

![mobile-report-indicator-data-grid](../../reporting-services/mobile-reports/media/mobile-report-indicator-data-grid.png)

1. Trascinare una griglia dati indicatore dalla scheda **Layout** alla griglia di struttura e impostare le dimensioni desiderate.

2. Nella riquadro **Colonne** della scheda **Dati** selezionare **Aggiungi colonna misuratore**. 

3. Selezionare **Opzioni**e scegliere un **Tipo di misuratore**. 

4. Impostare i campi **Valore** e **Confronto** e **Direzione valori**come descritto in [Aggiungere indicatori ai report per dispositivi mobili](../../reporting-services/mobile-reports/add-gauges-to-mobile-reports-reporting-services.md).

La griglia dati inserisce automaticamente nel misuratore solo i dati specifici di tale riga della griglia dati.  

## <a name="chart-data-grid"></a>Griglia dati grafico
A una griglia dati grafico è possibile aggiungere colonne con misuratori o grafici. 

![mobile-report-chart-data-grid](../../reporting-services/mobile-reports/media/mobile-report-chart-data-grid.png)

Quando si aggiunge una colonna grafico a una griglia dati, è necessario aggiungere una tabella dati separata con i dati per il grafico specificati in ogni riga. La seconda tabella dati deve condividere un campo con la tabella dati principale per poter collegare ogni riga ai dati del grafico associato. 

1. Trascinare una griglia dati grafico dalla scheda **Layout** alla griglia di struttura e impostare le dimensioni desiderate.

2. Nel riquadro **Colonne** della scheda **Dati** selezionare **Aggiungi colonna grafico**. 

3. Filtrare [i dati da Excel o da un set di dati condiviso](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md) per aggiungere una seconda tabella dati con un campo condiviso con la tabella dati principale, se non è ancora disponibile.

4. In **Proprietà dati**selezionare la tabella dati principale in **Dati per la visualizzazione griglia**e selezionare la seconda tabella in **Dati di riferimento per le visualizzazioni dei grafici**.

5. Selezionare **Opzioni**e scegliere un **Tipo di grafico**.
 
6. Selezionare **Chart data field**(Campo dati del grafico), **Ricerca nell'origine**e **Ricerca nella destinazione**. 
   Queste tre proprietà determinano come la griglia dati deve fornire i dati a ogni grafico nella colonna.
   
   *   **Ricerca nell'origine** è impostato su un campo della tabella dati presente in **Dati per la visualizzazione griglia**. Questo campo svolge la funzione di filtro per riga applicato alla tabella dati di riferimento al grafico per fornire i dati al grafico incorporato a livello di riga. 
   * **Ricerca nella destinazione** è il campo della tabella dati presente in **Dati di riferimento per le visualizzazioni dei grafici**. Verrà creato un join dei dati per il grafico in ogni riga con i due campi.   
   * **Chart data field** (Campo dati del grafico) determina la metrica della tabella **Dati di riferimento per le visualizzazioni dei grafici** da usare come valore dell'asse y o della serie nel grafico a livello di riga.  

## <a name="see-also"></a>Vedere anche 
* [Esegue il mapping nei report di Reporting Services per dispositivi mobili](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)
* [Aggiungere gli strumenti di navigazione ai report di Reporting Services per dispositivi mobili](../../reporting-services/mobile-reports/add-navigators-to-reporting-services-mobile-reports.md)
* [Visualizations to Reporting Services mobile reports (Visualizzazioni nei report per dispositivi mobili di Reporting Services)](../../reporting-services/mobile-reports/add-visualizations-to-reporting-services-mobile-reports.md)
* [Aggiungere indicatori ai report per dispositivi mobili | Reporting Services](../../reporting-services/mobile-reports/add-gauges-to-mobile-reports-reporting-services.md)  
 
  
