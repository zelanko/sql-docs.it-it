---
title: Ricerca obiettivo (strumenti di analisi tabelle per Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- scenario analysis
- goal seek scenario
ms.assetid: efe50306-cf7c-46b3-9cc4-e7f0b6968b0c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 85f0c099aba12fe9a4049fe787e248cfe580ff3b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62732002"
---
# <a name="goal-seek-scenario-table-analysis-tools-for-excel"></a>Ricerca obiettivo (Strumenti di analisi tabelle per Excel)
  ![Pulsante Ricerca obiettivo in strumenti di analisi tabelle](media/tat-goalseek.gif "pulsante Ricerca obiettivo in strumenti di analisi tabelle")  
  
 Il **ricerca obiettivo** dello strumento per scenari è complementare ad le [cosa accade se](what-if-scenario-table-analysis-tools-for-excel.md) dello strumento per scenari. Il **simulazione** lo strumento indica l'impatto di una modifica, mentre le **ricerca obiettivo** strumento indica i fattori sottostanti che è necessario modificare per ottenere un risultato desiderato.  
  
 Ad esempio, si supponga che l'obiettivo consiste nel migliorare la soddisfazione dei clienti. È possibile usare **ricerca obiettivo** analysis per determinare quali fattori sarebbe più probabili aumentare la soddisfazione dei clienti e decidere se tali modifiche sono convenienti.  
  
 Al termine dell'analisi, tramite lo strumento vengono create due nuove colonne nella tabella dati di origine. Queste colonne indicano il *probabilità* che è possibile ottenere il risultato di destinazione e la modifica consigliata, se presente.  
  
 Lo strumento consente di analizzare un set di dati e di eseguire stime per l'intero set. Altrimenti, è possibile creare l'analisi, quindi testare uno scenario alla volta.  
  
## <a name="using-the-goal-seek-scenario-tool"></a>Utilizzo dello strumento per l'analisi di scenari Ricerca obiettivo  
  
1.  Aprire una tabella di Excel.  
  
2.  Fare clic su **scenari**e selezionare **ricerca obiettivo**.  
  
3.  Nel **analisi di Scenario: Ricerca obiettivo** finestra di dialogo, seleziona il valore della colonna che contiene la destinazione dall'elenco.  
  
4.  Specificare il valore che si desidera raggiungere.  
  
     Se l'obiettivo della colonna contiene valori numerici continui, è anche possibile specificare la riduzione o l'aumento desiderato per il valore. Ad esempio, è possibile scegliere **Sales** della colonna e specificare che la destinazione è un aumento del 120%.  
  
     In alternativa, è possibile specificare l'obiettivo come intervallo di valori, digitando un limite inferiore e uno superiore.  
  
5.  Specificare la colonna contenente i valori che verranno modificati. In altre parole, scegliere la colonna che verrà modificata per produrre il risultato desiderato.  
  
6.  Facoltativamente, fare clic su **scegliere le colonne da utilizzare per l'analisi**e selezionare le colonne che contengono informazioni utili. Deselezionare le colonne che non contribuiscono all'analisi.  
  
    > [!NOTE]  
    >  Non deselezionare le colonne che verranno utilizzate per l'obiettivo o per la modifica. Queste colonne sono necessarie.  
  
7.  Specificare se si desidera eseguire le stime per l'intera tabella o solo per la riga selezionata.  
  
8.  Se è stata selezionata la **intera tabella** opzione, lo strumento le stime vengono aggiunte alla tabella di origine in due nuove colonne.  
  
9. Se è stata selezionata l'opzione **in questa riga**, i risultati dell'analisi vengono visualizzati nella finestra di dialogo per la revisione. La finestra di dialogo rimane aperta in modo che sia possibile continuare a provare diversi valori e obiettivi.  
  
### <a name="requirements"></a>Requisiti  
 Questo strumento utilizza l'algoritmo Microsoft Logistic Regression, che consente di elaborare valori numerici o discreti.  
  
 È possibile eseguire la stima più volte selezionando colonne diverse, ma ogni combinazione di obiettivo e modifica deve essere calcolata separatamente.  
  
 È possibile ottenere risultati migliori se per l'analisi si selezionano colonne contenenti informazioni utili. Se tuttavia si include un numero di colonne troppo limitato, potrebbe essere difficile ottenere un risultato.  
  
 Quando si crea una stima alla volta, assicurarsi di selezionare una riga che non contenga già il risultato desiderato. In caso contrario, potrebbe verificarsi un errore. In altre parole, se lo scopo della ricerca dell'obiettivo è quello di determinare i fattori che incoraggiano l'acquisto di biciclette, è necessario includere solo i clienti che non hanno acquistato una bicicletta.  
  
## <a name="understanding-the-results-of-goal-seek-analysis"></a>Informazioni sui risultati di un'analisi Ricerca obiettivo  
 Quando si crea uno scenario per la ricerca di un obiettivo, tramite lo strumento vengono eseguite tre operazioni:  
  
-   Creazione di una struttura di data mining per l'archiviazione dei fatti principali relativi ai dati della tabella.  
  
-   Creazione di un modello di data mining per la regressione logistica basato sui dati.  
  
-   Creazione di una stima per ogni valore specificato.  
  
 Se si testano gli scenari di ricerca dell'obiettivo uno alla volta, è possibile visualizzare i risultati in modo interattivo. Questo è quello utilizzato per la creazione di un *query di stima singleton*.  
  
 Lo strumento di report nel **risultati** riquadro della finestra di dialogo casella se è stato possibile trovare uno scenario che raggiunge l'obiettivo desiderato. Se è stata individuata una soluzione appropriata, viene inoltre indicata la modifica necessaria. Ad esempio, il **ricerca obiettivo** strumento potrebbe indicare che la distanza dal lavoro deve essere inferiore a 5 miglia.  
  
 Risultati dell'esempio:  
  
 **Soluzione trovata dall'obiettivo Interest in Buying che la ricerca.**  
  
 **Corrispondenza più vicina ottenuti con la modifica di 'Commute distance' in ' 2-5 miles'.**  
  
 Poiché il risultato è basato su una riga esistente nella tabella dati, significa che per un particolare cliente l'acquisto di una bicicletta sarebbe più probabile se tutti gli altri dati rimanessero invariati, ma la distanza dal lavoro del cliente venisse ridotta a 2-5 miglia.  
  
 Se si creano stime di ricerca dell'obiettivo per tutte le righe nella tabella di Excel specificando **intera tabella**, thetool crea due nuove colonne nella tabella dati originale. La prima colonna aggiunta alla tabella contiene un segno di spunta all'interno di un cerchio verde, per indicare che l'obiettivo può essere raggiunto, oppure un segno X all'interno di un cerchio rosso, per indicare che non è possibile apportare modifiche che permettano di raggiungere l'obiettivo.  
  
 La seconda colonna contiene la modifica consigliata.  
  
> [!NOTE]  
>  Il livello di confidenza dell'indicazione e la relativa efficacia sono predeterminati dall'algoritmo e non possono essere modificati.  
  
## <a name="related-tools"></a>Strumenti correlati  
 Il Client di data mining per Excel, un componente aggiuntivo separato che offre funzionalità di data mining più avanzate, include procedure guidate per la creazione di modelli di data mining in grado di stimare il comportamento. Per altre informazioni, vedere [creazione di un modello di Data Mining](creating-a-data-mining-model.md).  
  
 Per altre informazioni sull'algoritmo utilizzato per il **ricerca obiettivo** scenario strumento, vedere l'argomento "Algoritmo Microsoft Logistic Regression" nella [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] documentazione Online.  
  
## <a name="see-also"></a>Vedere anche  
 [Strumenti di analisi tabelle per Excel](table-analysis-tools-for-excel.md)  
  
  
