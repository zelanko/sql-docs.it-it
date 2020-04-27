---
title: Scenario di ricerca obiettivo (strumenti di analisi tabelle per Excel) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Table Analysis tools
- scenario analysis
- goal seek scenario
ms.assetid: efe50306-cf7c-46b3-9cc4-e7f0b6968b0c
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d547c52bc5d4cb02870fc647469b5f63af9ab7cb
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66080743"
---
# <a name="goal-seek-scenario-table-analysis-tools-for-excel"></a>Ricerca obiettivo (Strumenti di analisi tabelle per Excel)
  ![Pulsante Ricerca obiettivo in Strumenti di analisi tabelle](media/tat-goalseek.gif "Pulsante Ricerca obiettivo in Strumenti di analisi tabelle")  
  
 Lo strumento per lo scenario di **Ricerca obiettivo** è complementare allo strumento [What If](what-if-scenario-table-analysis-tools-for-excel.md) scenario. Lo **strumento di** simulazione indica l'effetto di apportare una modifica, mentre lo strumento **Ricerca obiettivo** indica i fattori sottostanti che devono essere modificati per ottenere un risultato desiderato.  
  
 Si immagini, ad esempio, che l'obiettivo sia quello di aumentare la soddisfazione dei clienti. È possibile utilizzare l'analisi **Ricerca obiettivo** per determinare quali fattori potrebbero aumentare la soddisfazione dei clienti e decidere se tali modifiche sono convenienti.  
  
 Al termine dell'analisi, tramite lo strumento vengono create due nuove colonne nella tabella dati di origine. Queste colonne indicano la *probabilità* che il risultato di destinazione possa essere ottenuto e la modifica consigliata, se disponibile.  
  
 Lo strumento consente di analizzare un set di dati e di eseguire stime per l'intero set. Altrimenti, è possibile creare l'analisi, quindi testare uno scenario alla volta.  
  
## <a name="using-the-goal-seek-scenario-tool"></a>Utilizzo dello strumento per l'analisi di scenari Ricerca obiettivo  
  
1.  Aprire una tabella di Excel.  
  
2.  Fare clic su **scenari**e selezionare **Ricerca obiettivo**.  
  
3.  Nella finestra di dialogo **analisi dello scenario: ricerca obiettivo** selezionare la colonna che contiene il valore di destinazione dall'elenco.  
  
4.  Specificare il valore che si desidera raggiungere.  
  
     Se l'obiettivo della colonna contiene valori numerici continui, è anche possibile specificare la riduzione o l'aumento desiderato per il valore. È ad esempio possibile scegliere **Sales** come colonna e specificare che la destinazione è un aumento del 120%.  
  
     In alternativa, è possibile specificare l'obiettivo come intervallo di valori, digitando un limite inferiore e uno superiore.  
  
5.  Specificare la colonna contenente i valori che verranno modificati. In altre parole, scegliere la colonna che verrà modificata per produrre il risultato desiderato.  
  
6.  Facoltativamente, fare clic su **Scegli le colonne da utilizzare per l'analisi**e selezionare le colonne contenenti informazioni utili. Deselezionare le colonne che non contribuiscono all'analisi.  
  
    > [!NOTE]  
    >  Non deselezionare le colonne che verranno utilizzate per l'obiettivo o per la modifica. Queste colonne sono necessarie.  
  
7.  Specificare se si desidera eseguire le stime per l'intera tabella o solo per la riga selezionata.  
  
8.  Se è stata selezionata l'opzione **intera tabella** , lo strumento aggiunge le stime alla tabella di origine in due nuove colonne.  
  
9. Se è stata selezionata l'opzione **in questa riga**, i risultati dell'analisi vengono restituiti alla finestra di dialogo per la revisione. La finestra di dialogo rimane aperta in modo che sia possibile continuare a provare diversi valori e obiettivi.  
  
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
  
 Se si testano gli scenari di ricerca dell'obiettivo uno alla volta, è possibile visualizzare i risultati in modo interattivo. Corrisponde alla creazione di una query di *stima singleton*.  
  
 Lo strumento segnala nel riquadro dei **risultati** della finestra di dialogo se la ricerca di uno scenario che raggiunge l'obiettivo desiderato è stata completata. Se è stata individuata una soluzione appropriata, viene inoltre indicata la modifica necessaria. Ad esempio, lo strumento **Ricerca obiettivo** potrebbe indicare che la distanza di commutazione deve essere inferiore a 5 km.  
  
 Risultati dell'esempio:  
  
 **Soluzione trovata per la ricerca dell'obiettivo Interest in Buying.**  
  
 **Risultato migliore ottenuto con la modifica di 'Commute distance' in '2-5 miles'.**  
  
 Poiché il risultato è basato su una riga esistente nella tabella dati, significa che per un particolare cliente l'acquisto di una bicicletta sarebbe più probabile se tutti gli altri dati rimanessero invariati, ma la distanza dal lavoro del cliente venisse ridotta a 2-5 miglia.  
  
 Se si creano stime di ricerca obiettivo per tutte le righe nella tabella di Excel specificando l' **intera tabella**, theTool crea due nuove colonne nella tabella dati originale. La prima colonna aggiunta alla tabella contiene un segno di spunta all'interno di un cerchio verde, per indicare che l'obiettivo può essere raggiunto, oppure un segno X all'interno di un cerchio rosso, per indicare che non è possibile apportare modifiche che permettano di raggiungere l'obiettivo.  
  
 La seconda colonna contiene la modifica consigliata.  
  
> [!NOTE]  
>  Il livello di confidenza dell'indicazione e la relativa efficacia sono predeterminati dall'algoritmo e non possono essere modificati.  
  
## <a name="related-tools"></a>Strumenti correlati  
 Il Client di data mining per Excel, un componente aggiuntivo separato che offre funzionalità di data mining più avanzate, include procedure guidate per la creazione di modelli di data mining in grado di stimare il comportamento. Per ulteriori informazioni, vedere [creazione di un modello di data mining](creating-a-data-mining-model.md).  
  
 Per ulteriori informazioni sull'algoritmo utilizzato dallo strumento per lo scenario di **Ricerca obiettivo** , vedere l'argomento "algoritmo di regressione logistica Microsoft [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] " nella documentazione online di.  
  
## <a name="see-also"></a>Vedi anche  
 [Strumenti di analisi tabelle per Excel](table-analysis-tools-for-excel.md)  
  
  
