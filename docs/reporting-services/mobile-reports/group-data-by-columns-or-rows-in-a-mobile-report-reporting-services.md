---
title: Raggruppare i dati in colonne o righe in un report per dispositivi mobili | Reporting Services | Microsoft Docs
description: In Mobile Report Publisher è possibile organizzare i dati per colonne o per righe in diversi tipi di grafici. Questo articolo illustra i dati strutturati in base alle colonne o alle righe.
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: mobile-reports
ms.topic: conceptual
ms.assetid: b9ebd36c-a337-47ae-83e5-6c2f2144eb52
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: f28c3feb8d8cd2fe68ab093241ac4390768b6487
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "79448238"
---
# <a name="group-data-by-columns-or-rows-in-a-mobile-report--reporting-services"></a>Raggruppare i dati in colonne o righe in un report per dispositivi mobili | Reporting Services
È possibile organizzare i dati per colonne o per righe in diversi tipi di grafici in [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)]. Seguire questa procedura dettagliata.

Nei grafici temporali, totali, a torta e a imbuto è possibile organizzare i dati per righe o per colonne. 
* L'organizzazione per colonne è utile se una tabella ha diverse colonne di dati da confrontare. 
* L'organizzazione per righe è più appropriata se una colonna della tabella contiene i nomi delle varie categorie. 

La procedura seguente usa una tabella di confronto dei totali con i dati simulati in [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] , per illustrare la differenza tra la strutturazione dei dati per righe o per colonne in un grafico.  

1. Trascinare un **grafico totali di confronto** dalla scheda **Layout** nell'area di progettazione e ingrandirlo.

2. Selezionare la scheda **Dati** . Si noti che la tabella SimulatedTable contiene una serie di colonne, da **Metrica1** a **Metrica5** e da **Confronto1** a **Confronto5**. 

   ![mobile-report-data-group-column](../../reporting-services/mobile-reports/media/mobile-report-data-group-column.png)

3. Nel riquadro **Proprietà dati** **Serie principale** corrisponde a **SimulatedTable**. Selezionare la freccia nella casella accanto a **Serie principale**e verranno selezionate le colonne da **Metrica1** a **Metrica5** .

   ![mobile-report-properties-columns](../../reporting-services/mobile-reports/media/mobile-report-properties-columns.png)

   Allo stesso modo, per il valore **Serie di confronto** --  vengono selezionate le colonne da **Confronto1** a **Confronto5**.
   
4. Selezionare **Anteprima**.

   ![mobile-report-chart-by-columns](../../reporting-services/mobile-reports/media/mobile-report-chart-by-columns.png)

   Ogni barra nel grafico rappresenta una colonna della tabella. Le barre più spesse rappresentano le metriche e le barre più sottili rappresentano le colonne di confronto.

5. Selezionare la freccia Indietro nell'angolo in alto a sinistra per uscire dalla modalità di anteprima.

6. Nella riquadro **Proprietà visive** della scheda **Layout** modificare il valore **Struttura dei dati** da **Per colonne** a **Per righe**.  

7. Selezionare la scheda **Dati** . A questo punto la tabella SimulatedTable contiene una colonna **Categoria** oltre alle colonne **Metrica** e **Confronto**, con categorie dalla A alla E. 

   ![mobile-report-data-group-rows](../../reporting-services/mobile-reports/media/mobile-report-data-group-rows.png)

8.  Nel riquadro **Proprietà dati** è ora presente una casella Category Column (Colonna Categoria) in cui viene visualizzata la colonna Categoria di SimulatedTable. In Serie principale è possibile selezionare la colonna da usare per i valori. Per impostazione predefinita, [!INCLUDE[SS_MobileReptPub_Short](../../includes/ss-mobilereptpub-short.md)] seleziona le colonne da Metrica1 a Metrica5 per la serie principale e da Confronto1 a Confronto5 per la serie di confronto. 

    ![mobile-report-properties-rows](../../reporting-services/mobile-reports/media/mobile-report-properties-rows.png)

9. Selezionare **Anteprima**.

   ![mobile-report-chart-by-rows](../../reporting-services/mobile-reports/media/mobile-report-chart-by-rows.png)

   Ogni barra nel grafico rappresenta ora i valori per ogni categoria presente nella colonna Categoria.

### <a name="see-also"></a>Vedere anche
* [Visualizations to Reporting Services mobile reports (Visualizzazioni nei report per dispositivi mobili di Reporting Services)](../../reporting-services/mobile-reports/add-visualizations-to-reporting-services-mobile-reports.md)
