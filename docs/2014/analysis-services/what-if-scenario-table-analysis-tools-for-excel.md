---
title: Scenario di simulazione (strumenti di analisi tabelle per Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- what if scenario
- scenario analysis
ms.assetid: 4df5a5c5-1983-4009-a7c5-cd340649fd2f
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fef8ca20bd3e137d21b5121f42a0d7fee82ae4a7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66065387"
---
# <a name="what-if-scenario-table-analysis-tools-for-excel"></a>Scenario di Analisi di simulazione (Strumenti di analisi tabelle per Excel)
  ![Il pulsante di Scenario in strumenti di analisi tabelle](media/tat-whatif.gif "pulsante lo Scenario di simulazione in strumenti di analisi tabelle")  
  
 Il **simulazione** lo strumento analizza modelli nei dati esistenti e consente quindi di valutare l'effetto che avranno le modifiche in una colonna del valore di una colonna diversa.  
  
 È ad esempio possibile esaminare l'effetto prodotto sulle vendite totali dall'aumento del prezzo di un articolo.  
  
 Lo strumento consente di creare il numero desiderato di stime. Dopo aver completato l'analisi iniziale, è possibile effettuare una stima relativa alle modifiche per tutti i dati della tabella o immettere i valori di prova uno alla volta.  
  
## <a name="using-the-what-if-scenario-tool"></a>Utilizzo dello strumento per scenari di Analisi di simulazione  
  
1.  Aprire una tabella di dati di Excel.  
  
2.  Fare clic su **scenari**, quindi selezionare **simulazione**.  
  
3.  Nel **Scenario** , selezionare la colonna che contiene il valore verrà modificare e specificare la modifica come un valore specifico o come percentuale delle modifiche (sia aumenta o diminuisce) in base ai valori correnti.  
  
4.  Nel **cosa accade ai** , specificare la colonna per cui si desidera valutare l'effetto.  
  
5.  Facoltativamente, fare clic su **scegliere le colonne da utilizzare per l'analisi** per selezionare le colonne che possono risultare utili per la stima. È inoltre possibile deselezionare le colonne poco utili per l'individuazione di modelli, ad esempio nomi o ID riga.  
  
6.  Nel **riga o tabella** scegliere se si desidera che l'impatto venga valutato per riga attualmente selezionata o per l'intero set di dati nella tabella.  
  
7.  Se si seleziona **in questa riga**, lo strumento consente di visualizzare il risultato nella finestra di dialogo. Fino a quando la finestra di dialogo rimane aperta, è possibile modificare le opzioni selezionate o testare altri scenari.  
  
8.  Se si seleziona **intera tabella**, lo strumento consente di visualizzare un messaggio di stato nella finestra di dialogo e aggiunge due nuove colonne alla tabella dati originale. Fare clic su **Chiudi** per visualizzare i risultati completi nel foglio di lavoro.  
  
### <a name="requirements"></a>Requisiti  
 Questo strumento utilizza l'algoritmo Microsoft Logistic Regression, che supporta la stima di valori numerici o discreti. Per ottenere risultati migliori, è tuttavia consigliabile attenersi alle procedure consigliate seguenti:  
  
-   Selezionare per l'analisi colonne contenenti informazioni utili.  
  
-   Se si include un numero troppo limitato di colonne, potrebbe essere difficile ottenere un risultato.  
  
-   Se si usa la **al valore** opzione, è necessario digitare un valore nella casella o selezionare un valore dall'elenco.  
  
-   Se si usa la **percentuale** , impostare la modifica come una percentuale di aumento o diminuzione. Il valore predefinito è 120%, ovvero un aumento del 20% rispetto al valore corrente.  
  
> [!NOTE]  
>  Se non si imposta alcun valore, è possibile che venga visualizzato un errore.  
  
## <a name="understanding-the-results-of-what-if-analysis"></a>Informazioni sui risultati dell'analisi di simulazione  
 Quando si crea una **simulazione** scenario, lo strumento esegue tre operazioni:  
  
-   Creazione di una struttura di data mining per l'archiviazione dei fatti principali relativi ai dati della tabella.  
  
-   Creazione di un modello di data mining per la regressione logistica basato sui dati.  
  
-   Creazione di una query di stima per ogni valore specificato.  
  
 È possibile restituire tutte le stime contemporaneamente specificando **intera tabella**. Verranno quindi create automaticamente due nuove colonne nella tabella dati originale.  
  
 Nelle colonne che vengono aggiunte alla tabella sono contenuti due tipi di informazioni: il valore stimato prodotto dalla modifica e il relativo livello di confidenza. Per confidenza si intende il grado di probabilità che la stima sia corretta.  
  
 È inoltre possibile immettere i valori di modifica uno alla volta nella finestra di dialogo e visualizzare le stime in modo interattivo. Questo è quello utilizzato per la creazione di un *query di stima singleton*. I risultati della query di stima vengono restituiti come output con le informazioni seguenti: avvenuta o mancata esecuzione della stima, valore stimato e livello di confidenza. Quest'ultimo viene indicato come una barra contenente una linea punteggiata. Più è lunga la linea punteggiata, maggiore è il livello di confidenza del risultato.  
  
 Ad esempio, se si tenta di determinare l'effetto di aumentare l'età del cliente nella volontà del cliente di acquistare e si aumenta l'età del cliente a 25, il **simulazione** strumento esegue una query il modello di data mining e viene restituito il risultato seguente:  
  
 **Soluzione trovata dall'analisi di simulazione per Purchases Bicycle.**  
  
 **'Gli acquisti Bicycle' = Sì**  
  
 **Confidenza: Equa**  
  
 Poiché questo risultato è basato su una riga esistente della tabella dati, indica che, se tutti i dati relativi a un determinato cliente rimangono invariati eccetto l'età, che è stata aumentata a 25 anni, è probabile che il cliente acquisterà una bicicletta.  
  
 La restituzione delle stime come output nella tabella dati originale consente di determinare con maggiore facilità se le stime sono utili.  
  
## <a name="related-tools"></a>Strumenti correlati  
 Il Client di data mining per Excel, un componente aggiuntivo separato che offre funzionalità di data mining più avanzate, include procedure guidate per la creazione di modelli di data mining in grado di stimare il comportamento. Per altre informazioni, vedere [creazione di un modello di Data Mining](creating-a-data-mining-model.md).  
  
 Per altre informazioni sull'algoritmo utilizzato per il **simulazione** scenario dello strumento, vedere l'argomento "Algoritmo Microsoft Logistic Regression" nella documentazione Online di SQL Server.  
  
## <a name="see-also"></a>Vedere anche  
 [Strumenti di analisi tabelle per Excel](table-analysis-tools-for-excel.md)  
  
  
