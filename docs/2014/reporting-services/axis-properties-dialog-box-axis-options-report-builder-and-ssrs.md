---
title: Finestra di dialogo Proprietà asse, opzioni asse (Generatore Report e SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.rtp.rptdesigner.axisproperties.axisoptions.f1
- "10138"
ms.assetid: b276e210-7a12-48ae-971b-7dabae51df11
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ff9f3281e47cf6dfdf8a189c653d0e061f4a761d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66109956"
---
# <a name="axis-properties-dialog-box-axis-options-report-builder-and-ssrs"></a>Finestra di dialogo Proprietà asse, Opzioni asse (Generatore report e SSRS)
  Selezionare **opzioni dell'asse** nel **orizzontale** oppure **proprietà asse verticale** finestra di dialogo per definire l'aspetto dell'asse specificato del grafico. Nelle versioni precedenti di [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]il grafico visualizzava tutte le etichette sull'asse x per impostazione predefinita. In [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] 2008, tuttavia, il grafico ignora le etichette allo scopo di produrre un'immagine più pulita sul grafico ed evitare la sovrapposizione delle etichette. Per altre informazioni, vedere [Formattazione delle etichette degli assi in un grafico &#40;Generatore report e SSRS&#41;](report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md).  
  
## <a name="options"></a>Opzioni  
 **Abilita cambi di scala**  
 Selezionare questa opzione per abilitare il disegno di interruzioni di scala nel grafico quando è necessario. Se questa opzione è abilitata, verrà automaticamente calcolato se la differenza tra i punti massimo e minimo nel set di dati è sufficiente per disegnare un'interruzione di scala.  
  
 **Inverti direzione**  
 Selezionare questa opzione per invertire la direzione del grafico. Un istogramma, ad esempio, viene visualizzato per impostazione predefinita con l'asse Y sul lato sinistro del diagramma e con le categorie da sinistra a destra. Quando questa opzione è selezionata, l'asse Y del grafico viene visualizzato sul lato destro del grafico e le categorie vengono visualizzate da destra a sinistra.  
  
 **Utilizza colore interlacciamento**  
 Selezionare questa opzione per aggiungere strisce al grafico, quindi selezionare un colore o digitare un'espressione. Le strisce sono bande ombreggiate nell'area del grafico che forniscono l'effetto di alternare aree chiare e scure tra le linee della griglia. Risultano utili per evidenziare modelli ripetuti in un asse.  
  
 **Includi sempre zero**  
 Selezionare questa opzione per includere sempre lo zero sulla scala dell'asse. Se questa opzione non è abilitata, il valore zero non verrà etichettato sull'asse del grafico. L'inclusione di valori zero risulta utile quando il set di dati comprende valori negativi o zero.  
  
 **Asse scalare**  
 Selezionare questa opzione per visualizzare un set di valori dell'asse su una scala continua. Ad esempio, se il set di dati contiene i dati relativi a gennaio, marzo e novembre, in un asse non scalare verranno visualizzati solo questi mesi, mentre in un asse scalare verranno riportati tutti i mesi dell'anno.  
  
 **Usa scala logaritmica**  
 Selezionare questa opzione per indicare che la scala dell'asse è logaritmica. Questa opzione è disponibile solo sull'asse Y se contiene valori numerici positivi.  
  
 Nella casella digitare la base logaritmica da utilizzare quando l'asse è impostato per l'utilizzo di una scala logaritmica. Per impostazione predefinita, viene utilizzata la base 10 per la scala logaritmica di un asse del grafico. Questa opzione è disponibile solo sull'asse Y se è numerico.  
  
 **Minimo**  
 Digitare un'espressione o un valore per il valore minimo dell'asse X. Se omesso, il valore minimo viene determinato in base ai dati restituiti dal set di dati.  
  
 **Massimo**  
 Digitare un'espressione o un valore per il valore massimo dell'asse X. Se omesso, il valore massimo viene determinato in base ai dati restituiti dal set di dati.  
  
 **Interval**  
 Digitare un'espressione o un valore per l'intervallo tra le etichette degli assi. Digitare, ad esempio, 1 per visualizzare ogni etichetta di categoria sull'asse. Digitare 2 per visualizzare tutte le altre etichette di categoria. Se questo valore viene omesso, le etichette vengono calcolate automaticamente in base ai valori del set di dati.  
  
 **Tipo di intervallo**  
 Digitare un'espressione o un valore per il tipo dell'intervallo specificato. Ad esempio, se si vuole che l'intervallo sia di due giorni, specificare **2** per Intervallo e **Giorni** per Tipo di intervallo.  
  
 **Margini laterali**  
 Digitare un'espressione o selezionare un valore per aggiungere o rimuovere un margine tra gli elementi e i lati del grafico. Se questa opzione è impostata su **Automatico**, i margini laterali vengono aggiunti.  
  
## <a name="see-also"></a>Vedere anche  
 [Formattazione delle etichette degli assi in un grafico &#40;Generatore report e SSRS&#41;](report-design/formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Grafici &#40;Generatore report e SSRS&#41;](report-design/charts-report-builder-and-ssrs.md)   
 [Formattazione dei colori delle serie in un grafico &#40;Generatore report e SSRS&#41;](report-design/formatting-series-colors-on-a-chart-report-builder-and-ssrs.md)   
 [Specificare un intervallo dell'asse &#40;Generatore report e SSRS&#41;](report-design/specify-an-axis-interval-report-builder-and-ssrs.md)   
 [Formattazione delle etichette degli assi come date o valute &#40;Generatore report e SSRSSSRS&#41;](report-design/format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [Tracciare i dati su un asse secondario &#40;Report e SSRS&#41;](report-design/plot-data-on-a-secondary-axis-report-builder-and-ssrs.md)   
 [Grafici sparkline e barre dei dati &#40;Generatore report e SSRS&#41;](report-design/sparklines-and-data-bars-report-builder-and-ssrs.md)   
 [Aggiungere o rimuovere i margini da un grafico &#40;Generatore report e SSRS&#41;](report-design/add-or-remove-margins-from-a-chart-report-builder-and-ssrs.md)  
  
  
