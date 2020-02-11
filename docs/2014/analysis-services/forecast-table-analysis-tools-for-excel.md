---
title: Previsione (strumenti di analisi tabelle per Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- forecasting
- mining model, time series
- time series [data mining]
ms.assetid: 22bb0b5e-78f5-484e-883d-2b5985a12749
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: dc620811209d854af5a9c874956847236819f462
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66081050"
---
# <a name="forecast-table-analysis-tools-for-excel"></a>Previsione (Strumenti di analisi tabelle per Excel)
  ![Pulsante Previsione in Strumenti di analisi tabelle](media/tat-forecast.gif "Pulsante Previsione in Strumenti di analisi tabelle")  
  
 Lo strumento **previsione** consente di eseguire stime basate sui dati in una tabella dati di Excel o in un'altra origine dati e, facoltativamente, di visualizzare le probabilità associate a ogni valore stimato. Se ad esempio nei dati sono contenute una colonna per la data e una colonna con il totale delle vendite per ogni giorno del mese, è possibile stimare le vendite per i giorni futuri. È inoltre possibile specificare il numero di stime da creare. È ad esempio possibile fare una stima relativa a cinque giorni o a trenta.  
  
 Al termine dell'esecuzione dello strumento, le nuove stime vengono aggiunte alla fine della tabella dati di origine e i nuovi valori vengono evidenziati. I nuovi valori della serie temporale non vengono aggiunti, in modo da consentire innanzitutto un esame delle stime.  
  
 Tramite lo strumento viene inoltre creato un nuovo foglio di il **report di previsione**. in cui viene segnalato se tramite la procedura guidata è stato possibile creare una stima e in cui è contenuto un grafico a linee delle tendenze cronologiche.  
  
 Se si estende la serie temporale in modo da includere le nuove stime, i valori stimati verranno aggiunti al grafico a linee. I valori cronologici vengono riportati come linee continue, mentre le stime vengono riportate come linee tratteggiate.  
  
## <a name="using-the-forecast-tool"></a>Utilizzo dello strumento Previsione  
  
1.  Aprire una tabella di Excel contenente dati numerici stimabili.  
  
2.  Fare clic su **previsione** nella scheda **analizza** .  
  
3.  Specificare le colonne per la previsione. Lo strumento seleziona automaticamente le colonne nei dati con tipo di dati stimabile, ovvero dati numerici continui. È possibile che alcune colonne con dati numerici continui non vengano selezionate dallo strumento, se contengono numerosi valori Null o zero, in quanto i dati mancanti potrebbero influire sui risultati. In tal caso, è possibile correggere i dati utilizzando lo strumento modifica [etichette &#40;SQL Server componente aggiuntivo&#41;data mining](relabel-sql-server-data-mining-add-ins.md) .  
  
4.  Specificare la colonna che contiene l'identificatore di data e ora o altri identificatori di serie. Se si seleziona l'opzione ** \<nessun timestamp>** lo strumento creerà una serie in base alla sequenza di righe nei dati di origine.  
  
5.  Specificare il numero di stime da effettuare.  
  
6.  È possibile fornire un hint all'algoritmo per indicare se si prevede che i dati si ripetano su base settimanale, mensile o per altri periodi. Se i dati non rientrano in uno dei modelli specificati o se non si conoscono i modelli, selezionare ** \<rileva automaticamente>** in modo che lo strumento trovi i periodi di tempo ripetuti.  
  
7.  Tramite la procedura guidata le stime vengono aggiunte alla tabella di origine e viene creato un report di previsione in un nuovo foglio di lavoro.  
  
8.  Per aggiungere i nuovi valori al grafico di stima, estendere la serie temporale in modo da includere i valori previsti.  
  
### <a name="requirements"></a>Requisiti  
 Le colonne per cui eseguire la stima devono contenere dati numerici continui, ad esempio valori di valuta o altri numeri.  
  
 Se possibile, i dati devono inoltre includere una colonna contenente una serie di date o ore. È possibile utilizzare una serie numerica (1, 2, 3....) anziché dati di data e ora. I valori della colonna della serie tuttavia devono essere univoci. Se lo strumento di **previsione** rileva valori duplicati nella colonna serie, si verifica un errore.  
  
 Non è possibile prevedere una data utilizzando lo strumento **previsione** . Benché non si verifichi necessariamente un errore, tale algoritmo non è stato sviluppato per utilizzare le date come valori stimabili.  
  
### <a name="understanding-time-stamps"></a>Informazioni sui timestamp  
 È necessario identificare una colonna da utilizzare come *timestamp*. Il timestamp ha due scopi. Innanzitutto, consente di identificare in modo univoco un valore in una serie temporale. Se, ad esempio, si stanno registrando le vendite su base giornaliera, deve essere presente un solo valore relativo alle vendite per ogni giorno. La data di calendario può essere utilizzata come timestamp. In secondo luogo, la colonna timestamp indica l'unità per le stime. Se si stanno registrando le vendite giornaliere, anche le stime saranno in unità di giorni.  
  
 Se i dati non includono una colonna di data o ora, tramite lo strumento verrà creata automaticamente una chiave di serie temporanea, denominata _RowIndex. La chiave sarà basata sull'ordine delle righe nel set di dati.  
  
 Per specificare il numero di stime, è necessario immettere un numero intero che indica il numero di unità di tempo. Le unità di tempo dipendono dalle unità utilizzate nelle serie di data e ora presenti nei dati. Se i dati elencano i risultati delle vendite per mese, la stima verrà eseguita per una serie di mesi. Non è possibile modificare l'unità di tempo, a meno che non si cambino i dati di origine.  
  
### <a name="understanding-periodicity"></a>Informazioni sulla periodicità  
 Una previsione è basata su nodelli ripetuti in un periodo di tempo. Tramite l'algoritmo Microsoft Time Series vengono pertanto eseguiti i calcoli per determinare i periodi di tempo che presentano i modelli più marcati. La *periodicità* fa riferimento a questi periodi di tempo.  
  
 Una serie temporale può contenere numerosi modelli potenziali. Se si è certi che i dati contengano un determinato modello, è possibile migliorare la qualità della stima fornendo un hint all'algoritmo.  
  
 Se, ad esempio, ci si aspetta che i dati si ripetano su base settimanale, è possibile selezionare Settimanale per indicare che l'algoritmo deve cercare modelli settimanali. Se, tuttavia, non vengono individuati modelli settimanali marcati, l'hint viene ignorato dall'algoritmo.  
  
## <a name="understanding-the-forecasting-report"></a>Informazioni sul Report previsione  
 In questo grafico i valori cronologici della tabella dati vengono visualizzati con una linea scura, mentre i valori stimati vengono visualizzati con linee tratteggiate. È possibile fare clic su un punto sulla linea per visualizzare il valore previsto.  
  
> [!NOTE]  
>  Se non vengono visualizzate etichette sull'asse temporale per i valori stimati nel grafico, aprire il foglio di lavoro che contiene i valori stimati e utilizzare la funzione **Fill, serie** in Excel per estendere la colonna timestamp in modo da includere i valori stimati.  
  
 In alcuni casi è possibile che nella previsione non siano inclusi tutti i gli intervalli di tempo necessari. Questo problema in genere si verifica se i dati non sono sufficienti per consentire all'algoritmo di effettuare una previsione estendendosi così lontano nel tempo. Lo strumento di **previsione** farà solo previsioni che soddisfano una soglia di probabilità minima.  
  
## <a name="related-tools"></a>Strumenti correlati  
 Il client di data mining per Excel è un componente aggiuntivo separato che offre ulteriori funzionalità avanzate di data mining e una procedura guidata per la previsione.  
  
 Sia lo strumento **previsione** (in strumenti di analisi tabelle per Excel) che la procedura guidata **previsione** (nel client di data mining per Excel) utilizzano [!INCLUDE[msCoName](../includes/msconame-md.md)] l'algoritmo Time Series.  
  
-   Lo strumento **previsione** è più facile da utilizzare perché configura automaticamente l'algoritmo per l'utilizzo delle impostazioni migliori per i dati.  
  
-   La procedura guidata **previsione** nel client di data mining per Excel offre la possibilità di personalizzare i parametri.  
  
 Per ulteriori informazioni sulla procedura guidata **previsione** , vedere la [procedura guidata previsione &#40;componenti aggiuntivi data mining per&#41;Excel ](forecast-wizard-data-mining-add-ins-for-excel.md). Per ulteriori informazioni sull'algoritmo utilizzato per la previsione, vedere l'argomento "Algoritmo Microsoft Time Series" nella documentazione online di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Vedere anche  
 [Strumenti di analisi tabelle per Excel](table-analysis-tools-for-excel.md)  
  
  
