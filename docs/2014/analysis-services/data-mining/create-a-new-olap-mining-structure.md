---
title: Creazione di una nuova struttura di data mining OLAP | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining structures [Analysis Services], OLAP
- mining structures [Analysis Services], creating
- OLAP [Analysis Services], mining models
ms.assetid: 368f4273-a016-4748-bcb6-505a3e745af3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 62f8fc247986609e3822168bff5aace34f3d1aa9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66085456"
---
# <a name="create-a-new-olap-mining-structure"></a>Creare una nuova struttura di data mining OLAP
  È possibile utilizzare la creazione guidata modello di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] data mining in per creare una struttura di data mining che utilizza i dati di un modello multidimensionale. I modelli di data mining basati su cubi OLAP possono utilizzare la colonna e i valori di tabelle dei fatti, dimensioni e gruppi di misure come attributi per l'analisi.  
  
### <a name="to-create-a-new-olap-mining-structure"></a>Per creare una nuova struttura di data mining OLAP  
  
1.  In Esplora soluzioni in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]fare clic con il pulsante destro del mouse sulla cartella **Strutture di data mining** in un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , quindi scegliere **Nuova struttura di data mining** per aprire la Creazione guidata modello di data mining.  
  
2.  Nella pagina iniziale **Creazione guidata modello di data mining** fare clic su **Avanti**.  
  
3.  Nella pagina **Selezione metodo di definizione** selezionare **Da cubo esistente**, quindi fare clic su **Avanti**.  
  
     Se si riceve il messaggio di errore Impossibile recuperare un elenco degli algoritmi di data mining supportati, aprire la finestra di dialogo **Proprietà progetto** e verificare di avere specificato il nome di un'istanza di Analysis Services che supporta i modelli multidimensionali. Non è possibile creare modelli di data mining in un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che supporta la modellazione tabulare.  
  
4.  Nella pagina **Crea la struttura di data mining** scegliere se creare solo una struttura di data mining o una struttura di data mining e un modello di data mining correlato. È in genere più facile creare contemporaneamente un modello di data mining in modo da ricevere le richieste di includere le colonne necessarie.  
  
     Se si crea un modello di data mining, selezionare l'algoritmo di data mining da usare, quindi fare clic su **Avanti**. Per altre informazioni su come scegliere un algoritmo, vedere [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](data-mining-algorithms-analysis-services-data-mining.md).  
  
5.  Nella pagina **Selezione dimensione cubo di origine** , in **Selezionare una dimensione del cubo di origine**, trovare la dimensione che contiene la maggior parte dei dati del case.  
  
     Se ad esempio si tenta di identificare i raggruppamenti del cliente, è possibile scegliere la dimensione Customer, se si tenta di analizzare gli acquisti nelle transazioni, è possibile scegliere la dimensione Dettagli ordine vendita Internet. Non si è limitati all'utilizzo dei soli dati di questa dimensione, tuttavia dovrebbe contenere attributi importanti per l'utilizzo nell'analisi.  
  
     Fare clic su **Avanti**.  
  
6.  Nella pagina **Selezione chiave del case** , in **Attributi**, selezionare l'attributo che costituirà la chiave della struttura di data mining, quindi fare clic su **Avanti**.  
  
     In genere, l'attributo utilizzato come chiave per la struttura di data mining è anche una chiave per la dimensione e risulterà pre-selezionata.  
  
7.  Nella pagina **Selezione colonne livello case** , in **Attributi e misure correlati**, selezionare gli attributi e le misure che contengono i valori da aggiungere alla struttura di data mining come dati del case. Fare clic su **Avanti**.  
  
8.  Nella pagina **Impostazione utilizzo colonne modello di data mining** , in **Struttura modello di data mining**, impostare la colonna stimabile, quindi scegliere le colonne da usare come input.  
  
    -   Selezionare la casella di controllo nella colonna più a sinistra per includere i dati nella struttura di data mining. È possibile includere le colonne nella struttura che verranno utilizzate come riferimento, ma non per l'analisi.  
  
    -   Selezionare la casella di controllo nella colonna **Input** per usare l'attributo come variabile nell'analisi.  
  
    -   Selezionare la casella di controllo nella colonna **Stima** solo per gli attributi stimabili.  
  
     Si noti che colonne definite come chiavi non possono essere utilizzate per l'input o la stima.  
  
     Fare clic su **Avanti**.  
  
9. Nella pagina **Impostazione utilizzo colonne modello di data mining** è anche possibile aggiungere e rimuovere le tabelle annidate dalla struttura di data mining, usando **Aggiungi tabelle annidate** e **Tabelle annidate**.  
  
     In un modello di data mining OLAP, una tabella nidificata è un altro set di dati all'interno del cubo che presenta una relazione uno-a-molti con la dimensione che rappresenta gli attributi del case. Di conseguenza, quando viene visualizzata la finestra di dialogo, i gruppi di misure già correlati alla dimensione selezionata come tabella del case vengono preselezionati. A questo punto, si dovrebbe scegliere una dimensione diversa che contenga informazioni aggiuntive utili per l'analisi.  
  
     Ad esempio, se si analizzano i clienti, si dovrebbe usare la dimensione [Customer] come tabella del case. Per la tabella annidata, è possibile aggiungere il motivo indicato dai clienti al momento di un acquisto, incluso nella dimensione [Sales Reason].  
  
     Se si aggiungono dati nidificati, è necessario specificare due colonne aggiuntive:  
  
    -   Chiave della tabella annidata: deve essere preselezionata nella pagina **Selezione chiave tabella annidata**.  
  
    -   Attributi o attributi da usare per l'analisi: nella pagina **Selezione colonne tabella annidata**è contenuto un elenco delle misure e degli attributi nella selezione della tabella annidata.  
  
        -   Per ogni attributo incluso nel modello, selezionare la casella nella colonna sinistra.  
  
        -   Se si desidera usare l'attributo solo per l'analisi, selezionare **Input**.  
  
        -   Se si desidera includere la colonna come uno degli attributi stimabili per il modello, selezionare **Stima**.  
  
        -   Qualsiasi elemento incluso nella struttura, ma non specificato come un input o attributo stimabile viene aggiunto alla struttura con il flag `Ignore`. Ciò significa che i dati vengono elaborati quando si compila il modello, ma non vengono utilizzati nell'analisi e sono disponibili solo per il drill-through. Questa operazione può essere utile se si desidera includere dettagli come i nomi dei clienti, ma non si desidera utilizzarli nell'analisi.  
  
     Fare clic su **Fine** per chiudere la parte della procedura guidata correlata alle tabelle annidate. È possibile ripetere il processo per aggiungere più colonne nidificate.  
  
10. Nella pagina **Impostazione tipo di contenuto e dati delle colonne** , in **Struttura modello di data mining**, impostare il tipo di contenuto e il tipo di dati per ogni colonna.  
  
    > [!NOTE]  
    >  I modelli di data mining OLAP non supportano l'uso della caratteristica **Rileva** per rilevare automaticamente se una colonna contiene dati continui o discreti.  
  
     Fare clic su **Avanti**.  
  
11. Nella pagina **Sezionamento cubo di origine** è possibile filtrare i dati usati per creare la struttura di data mining.  
  
     Sezionando il cubo si limitano i dati utilizzati per la compilazione del modello. È ad esempio possibile compilare modelli separati per ogni area sezionando in base alla gerarchia Geography e  
  
    -   **Dimensione**: scegliere una dimensione correlata dall'elenco a discesa.  
  
    -   **Gerarchia**: selezionare il livello della gerarchia di dimensione al quale si desidera applicare il filtro. Ad esempio, se si seziona in base alla dimensione [Geography], è necessario scegliere un livello di gerarchia come [Region Country Name].  
  
    -   **Operatore**: scegliere un operatore dall'elenco.  
  
    -   **Espressione filtro**: digitare un valore o un'espressione da usare come condizione di filtro oppure usare l'elenco a discesa per selezionare un valore dall'elenco dei membri al livello specificato della gerarchia.  
  
         Ad esempio, se si è selezionato [Geography] come dimensione e [Region Country Name] come livello della gerarchia, l'elenco a discesa contiene tutti i paesi validi che è possibile usare come condizione di filtro. È possibile effettuare più selezioni. Di conseguenza, i dati nella struttura di data mining saranno limitati ai dati del cubo da queste aree geografiche.  
  
    -   **Parametri**: ignorare questa casella di controllo. Questa finestra di dialogo supporta più scenari di applicazione filtri del cubo e questa opzione non è attinente alla compilazione di una struttura di data mining.  
  
     Fare clic su **Avanti**.  
  
12. Nella pagina **Divisione dei dati in set di training e in set di testing** specificare la percentuale di dati della struttura di data mining da riservare al test oppure specificare il numero massimo di test case. Fare clic su **Avanti**.  
  
     Se si specificano entrambi valori, i limiti vengono combinati per utilizzare quello più basso.  
  
13. Nella pagina **Completamento procedura guidata** specificare un nome per la nuova struttura di data mining OLAP e per il modello di data mining iniziale.  
  
14. Fare clic su **Fine**.  
  
15. Nella pagina **Completamento procedura guidata** è anche disponibile l'opzione per creare una dimensione del modello di data mining e/o un cubo usando la dimensione del modello di data mining. Queste opzioni sono supportate solo per i modelli compilati utilizzando gli algoritmi seguenti:  
  
    -   Algoritmo Microsoft Clustering  
  
    -   Algoritmo Microsoft Decision Trees  
  
    -   Algoritmo Microsoft Association Rules  
  
     **Crea dimensione del modello di data mining**: selezionare questa casella di controllo e specificare un tipo per la dimensione del modello di data mining. Quando si utilizza questa opzione, viene creata una nuova dimensione all'interno del cubo originale utilizzato per compilare la struttura di data mining. È possibile utilizzare questa dimensione per eseguire il drill-down ed effettuare ulteriori analisi. Poiché si trova all'interno del cubo, viene automaticamente eseguito il mapping della dimensione alla dimensione dei dati del case.  
  
     **Crea il cubo utilizzando la dimensione del modello di data mining**: selezionare questa casella di controllo e specificare un nome per il nuovo cubo. Quando si utilizza questa opzione, viene creato un nuovo cubo contenente sia le dimensioni esistenti utilizzate nella compilazione della struttura sia la nuova dimensione di data mining contenente i risultati del modello.  
  
## <a name="see-also"></a>Vedi anche  
 [Attività e procedure relative alla struttura di data mining](mining-structure-tasks-and-how-tos.md)  
  
  
