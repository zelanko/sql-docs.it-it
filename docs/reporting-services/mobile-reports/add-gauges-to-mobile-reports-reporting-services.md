---
title: Aggiungere indicatori ai report per dispositivi mobili | Reporting Services | Microsoft Docs
ms.date: 03/30/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: 76d8fc8f-c37f-44d3-ab44-45fbeed4e064
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1740846b348449cc1a2d4e072255a1339b96c478
ms.sourcegitcommit: 31800ba0bb0af09476e38f6b4d155b136764c06c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/15/2019
ms.locfileid: "56288549"
---
# <a name="add-gauges-to-mobile-reports--reporting-services"></a>Aggiungere indicatori ai report per dispositivi mobili | Reporting Services
I misuratori sono gli oggetti visivi più semplici e più usati nei report per dispositivi mobili. Visualizzano un singolo valore in un set di dati: soltanto il valore oppure il valore rispetto a un obiettivo.

![PBI_SSMRP_Gauges](../../reporting-services/mobile-reports/media/pbi-ssmrp-gauges.png)  
  
*Visualizzazioni dei misuratori nella scheda Layout*  
  
In SQL Server Mobile Report Publisher tutti i misuratori hanno in comune almeno una proprietà: un valore principale, impostato su un campo numerico in una delle tabelle dati nel report per dispositivi mobili.  

In tutti i misuratori, ad eccezione del misuratore numerico, può essere visualizzato anche un confronto, o valore *delta*, ovvero la relazione tra il valore principale e quello di confronto. Il valore di confronto è spesso l'obiettivo e il misuratore è un indicatore visivo dello stato di avanzamento verso tale obiettivo, oppure il delta tra il valore effettivo e l'obiettivo.

I misuratori possono rappresentare solo un valore aggregato per il valore principale e un valore aggregato per il valore di confronto. Le aggregazioni dei misuratori sono standard: somma, media, minimo, massimo e così via. Il valore misuratore predefinito è la somma, che visualizza il totale di tutti i valori contenuti nei dati filtrati correnti disponibili per il controllo misuratore. 

È possibile filtrare i valori dei misuratori connettendoli a strumenti di navigazione nel report per dispositivi mobili. 

## <a name="set-the-main-and-comparison-values-for-a-gauge"></a>Impostare il valore principale e il valore di confronto per un misuratore

1. Trascinare un misuratore dalla scheda **Layout** alla griglia di struttura e impostare le dimensioni desiderate.

2. Filtrare [i dati da Excel o da un set di dati condiviso](../../reporting-services/mobile-reports/data-for-reporting-services-mobile-reports.md).

3. Selezionare la scheda **Dati** e in **Valore principale** nel riquadro **Proprietà dati** scegliere una tabella dati e un campo numerico.

3. In qualsiasi misuratore, ad eccezione del misuratore numerico, in **Valore di confronto** nel riquadro **Proprietà dati** selezionare una tabella dati e un campo numerico.

4. [facoltativo] Per modificare l'aggregazione, selezionare **Opzioni** e scegliere un'aggregazione diversa.
   
   >**Nota**: quando si modifica l'aggregazione per il valore principale, si consiglia anche di modificare l'aggregazione per il valore di confronto, anche se in alcuni casi è possibile combinare i metodi di aggregazione.  

## <a name="filter-a-gauge"></a>Filtrare un misuratore
  
Se il report per dispositivi mobili include strumenti di navigazione, è possibile associare un misuratore a uno o più strumenti per filtrarlo. Il valore e il valore di confronto di un misuratore possono essere associati a uno o più strumenti di navigazione diversi, con opzioni praticamente illimitate per i misuratori.  

1. Selezionare un misuratore e nel riquadro **Proprietà dati** della scheda **Dati** selezionare **Opzioni** accanto a **Valore principale** o a **Valore di confronto**.

2. In Filtrato per selezionare lo strumento di navigazione da usare per filtrare il misuratore.

   ![mobile-report-gauge-navigator](../../reporting-services/mobile-reports/media/mobile-report-gauge-navigator.png)
 
## <a name="set-visual-properties-for-a-gauge"></a>Impostare le proprietà visive per un misuratore
  
Oltre alle proprietà dei dati che connettono gli elementi del misuratore ai campi dati, è possibile personalizzare diverse proprietà funzionali e visive. 

### <a name="set-value-direction-high-or-low-is-better"></a>Impostare la direzione valori: valori alti o bassi
* Selezionare un misuratore e nel riquadro **Proprietà visive** della scheda **Layout** impostare **Direzione valori** su **I valori più alti sono preferibili** o su **I valori più bassi sono preferibili**. 

Se si seleziona**I valori più alti sono preferibili** , i valori positivi saranno di colore verde, che indica una modifica desiderata in meglio, o di colore rosso, che indica una modifica indesiderata in peggio. 

All'impostazione **I valori più bassi sono preferibili** corrispondono i colori opposti.

La proprietà Direzione valori si applica solo agli elementi del misuratore che supportano un valore di confronto. Il colore del misuratore sarà determinato dal segno del valore integer delta e dall'impostazione della proprietà Direzione valori.  
  
### <a name="set-range-stops-for-a-gauge"></a>Impostare le interruzioni di intervallo per un misuratore
La seconda proprietà non di dati specifica del misuratore è Interruzioni intervallo. 

* Selezionare un misuratore e nel riquadro **Proprietà visive** della scheda **Layout** fare clic su **Interruzioni intervallo**.

Tramite le interruzioni di intervallo è possibile determinare a quale percentuale del valore di confronto la visualizzazione deve essere presentata come in target (verde), neutra (giallo) e fuori target (rosso), quando il target è un valore di confronto del misuratore. Anche in questo caso, la proprietà si applica solo ai misuratori con valori di confronto che supportano le interruzioni di intervallo.  

### <a name="format-the-numbers-in-the-gauge"></a>Formattare i numeri nel misuratore  
Un'altra proprietà non di dati dell'elemento misuratore, condivisa da diversi altri elementi, è Formato numeri. 

* Selezionare un misuratore e nel riquadro **Proprietà visive** della scheda **Layout** fare clic su **Interruzioni intervallo**.

Determina le modalità di formattazione dei numeri visualizzati nel misuratore, ad esempio valuta, percentuale, ora o generale. Impostare la formattazione dei numeri per ogni elemento del report per dispositivi mobili.
  
### <a name="see-also"></a>Vedere anche 

* [Creare report per dispositivi mobili con SQL Server Mobile Report Publisher](../../reporting-services/mobile-reports/create-mobile-reports-with-sql-server-mobile-report-publisher.md)
* [Eseguire il mapping nei report di Reporting Services per dispositivi mobili](../../reporting-services/mobile-reports/maps-in-reporting-services-mobile-reports.md)
* [Aggiungere gli strumenti di navigazione ai report di Reporting Services per dispositivi mobili](../../reporting-services/mobile-reports/add-navigators-to-reporting-services-mobile-reports.md)
* [Visualizations to Reporting Services mobile reports (Visualizzazioni nei report per dispositivi mobili di Reporting Services)](../../reporting-services/mobile-reports/add-visualizations-to-reporting-services-mobile-reports.md)
* [Aggiungere griglie dei dati al report per dispositivi mobili in Reporting Services](../../reporting-services/mobile-reports/add-data-grids-to-mobile-reports-reporting-services.md) 
