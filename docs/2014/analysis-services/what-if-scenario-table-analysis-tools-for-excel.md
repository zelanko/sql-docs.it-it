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
ms.openlocfilehash: ed1fe8447064bf224ea3f0e0a576d4e73fb07203
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84938112"
---
# <a name="what-if-scenario-table-analysis-tools-for-excel"></a>Scenario di Analisi di simulazione (Strumenti di analisi tabelle per Excel)
  ![Pulsante di scenario di simulazione in Strumenti di analisi tabelle](media/tat-whatif.gif "Pulsante di scenario di simulazione in Strumenti di analisi tabelle")

 Lo **strumento scenario di simulazione analizza i modelli** nei dati esistenti e quindi consente di valutare l'effetto delle modifiche apportate a una colonna sul valore di una colonna diversa.

 È ad esempio possibile esaminare l'effetto prodotto sulle vendite totali dall'aumento del prezzo di un articolo.

 Lo strumento consente di creare il numero desiderato di stime. Dopo aver completato l'analisi iniziale, è possibile effettuare una stima relativa alle modifiche per tutti i dati della tabella o immettere i valori di prova uno alla volta.

## <a name="using-the-what-if-scenario-tool"></a>Utilizzo dello strumento per scenari di Analisi di simulazione

1.  Aprire una tabella di dati di Excel.

2.  Fare clic su **scenari**, quindi **selezionare simulazione**.

3.  Nella casella **scenario** selezionare la colonna che contiene il valore che si vuole modificare e specificare la modifica come valore specifico o come percentuale di modifica (aumentata o ridotta) sui valori correnti.

4.  Nella casella **cosa accade a** specificare la colonna per la quale si desidera valutare l'effetto.

5.  Facoltativamente, fare clic su **Scegli le colonne da utilizzare per l'analisi** per selezionare le colonne che potrebbero essere utili per eseguire la stima. È inoltre possibile deselezionare le colonne poco utili per l'individuazione di modelli, ad esempio nomi o ID riga.

6.  Nella casella **specificare la riga o la tabella** scegliere se si desidera che l'effetto venga valutato solo per la riga attualmente selezionata o per il set completo di dati nella tabella.

7.  Se si seleziona **questa riga**, lo strumento visualizzerà il risultato nella finestra di dialogo. Fino a quando la finestra di dialogo rimane aperta, è possibile modificare le opzioni selezionate o testare altri scenari.

8.  Se si seleziona **intera tabella**, lo strumento Visualizza un messaggio di stato nella finestra di dialogo e aggiunge due nuove colonne alla tabella dati originale. Fare clic su **Chiudi** per visualizzare i risultati completi nel foglio di esecuzione.

### <a name="requirements"></a>Requisiti
 Questo strumento utilizza l'algoritmo Microsoft Logistic Regression, che supporta la stima di valori numerici o discreti. Per ottenere risultati migliori, è tuttavia consigliabile attenersi alle procedure consigliate seguenti:

-   Selezionare per l'analisi colonne contenenti informazioni utili.

-   Se si include un numero troppo limitato di colonne, potrebbe essere difficile ottenere un risultato.

-   Se si usa l'opzione **per il valore** , è necessario digitare un valore nella casella o selezionare un valore dall'elenco.

-   Se si usa l'opzione **percentuale** , impostare la modifica come aumento o riduzione percentuale. Il valore predefinito è 120%, ovvero un aumento del 20% rispetto al valore corrente.

> [!NOTE]
>  Se non si imposta alcun valore, è possibile che venga visualizzato un errore.

## <a name="understanding-the-results-of-what-if-analysis"></a>Informazioni sui risultati dell'analisi di simulazione
 Quando si crea uno **scenario di** simulazione, lo strumento esegue tre operazioni:

-   Creazione di una struttura di data mining per l'archiviazione dei fatti principali relativi ai dati della tabella.

-   Creazione di un modello di data mining per la regressione logistica basato sui dati.

-   Creazione di una query di stima per ogni valore specificato.

 È possibile restituire tutte le stime contemporaneamente specificando un' **intera tabella**. Verranno quindi create automaticamente due nuove colonne nella tabella dati originale.

 Nelle colonne che vengono aggiunte alla tabella sono contenuti due tipi di informazioni: il valore stimato prodotto dalla modifica e il relativo livello di confidenza. Per confidenza si intende il grado di probabilità che la stima sia corretta.

 È inoltre possibile immettere i valori di modifica uno alla volta nella finestra di dialogo e visualizzare le stime in modo interattivo. Corrisponde alla creazione di una query di *stima singleton*. I risultati della query di stima vengono restituiti come output con le informazioni seguenti: avvenuta o mancata esecuzione della stima, valore stimato e livello di confidenza. Quest'ultimo viene indicato come una barra contenente una linea punteggiata. Più è lunga la linea punteggiata, maggiore è il livello di confidenza del risultato.

 Se, ad esempio, si sta tentando di determinare l'effetto di un aumento della validità del cliente sulla volontà del cliente di acquistare e di aumentare l'età del cliente a 25, **lo strumento di analisi di simulazione** esegue una query sul modello di data mining e restituisce il risultato seguente:

 **Soluzione trovata dall'analisi di simulazione per Purchases Bicycle.**

 **'Purchases Bicycle' = yes**

 **Confidence: Fair**

 Poiché questo risultato è basato su una riga esistente della tabella dati, indica che, se tutti i dati relativi a un determinato cliente rimangono invariati eccetto l'età, che è stata aumentata a 25 anni, è probabile che il cliente acquisterà una bicicletta.

 La restituzione delle stime come output nella tabella dati originale consente di determinare con maggiore facilità se le stime sono utili.

## <a name="related-tools"></a>Strumenti correlati
 Il Client di data mining per Excel, un componente aggiuntivo separato che offre funzionalità di data mining più avanzate, include procedure guidate per la creazione di modelli di data mining in grado di stimare il comportamento. Per ulteriori informazioni, vedere [creazione di un modello di data mining](creating-a-data-mining-model.md).

 Per ulteriori informazioni sull'algoritmo **utilizzato dallo strumento scenario di** simulazione, vedere l'argomento "algoritmo di regressione logistica Microsoft" in documentazione online di SQL Server.

## <a name="see-also"></a>Vedere anche
 [Strumenti di analisi tabelle per Excel](table-analysis-tools-for-excel.md)


