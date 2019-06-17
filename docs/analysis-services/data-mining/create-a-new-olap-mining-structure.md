---
title: Creare una nuova struttura di Data Mining OLAP | Microsoft Docs
ms.date: 05/01/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d0a12d7fad2deb138d2dac445492ffce55f1493a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62911285"
---
# <a name="create-a-new-olap-mining-structure"></a>Creare una nuova struttura di data mining OLAP
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  È possibile usare la Creazione guidata modello di data mining in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] per creare una struttura di data mining che usa dati da un modello multidimensionale. I modelli di data mining basati su cubi OLAP possono utilizzare la colonna e i valori di tabelle dei fatti, dimensioni e gruppi di misure come attributi per l'analisi.  
  
### <a name="to-create-a-new-olap-mining-structure"></a>Per creare una nuova struttura di data mining OLAP  
  
1.  In Esplora soluzioni in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]fare clic con il pulsante destro del mouse sulla cartella **Strutture di data mining** in un progetto di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , quindi scegliere **Nuova struttura di data mining** per aprire la Creazione guidata modello di data mining.  
  
2.  Nella pagina iniziale **Creazione guidata modello di data mining** fare clic su **Avanti**.  
  
3.  Nella pagina **Selezione metodo di definizione** selezionare **Da cubo esistente**, quindi fare clic su **Avanti**.  
  
     Se si riceve il messaggio di errore Impossibile recuperare un elenco degli algoritmi di data mining supportati, aprire la finestra di dialogo **Proprietà progetto** e verificare di avere specificato il nome di un'istanza di Analysis Services che supporta i modelli multidimensionali. Non è possibile creare modelli di data mining in un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che supporta la modellazione tabulare.  
  
4.  Nella pagina **Crea la struttura di data mining** scegliere se creare solo una struttura di data mining o una struttura di data mining e un modello di data mining correlato. È in genere più facile creare contemporaneamente un modello di data mining in modo da ricevere le richieste di includere le colonne necessarie.  
  
     Se si crea un modello di data mining, selezionare l'algoritmo di data mining da usare, quindi fare clic su **Avanti**. Per altre informazioni su come scegliere un algoritmo, vedere [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](../../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md).  
  
5.  Nella pagina **Selezione dimensione cubo di origine**, in **Selezionare una dimensione del cubo di origine**, trovare la dimensione che contiene la maggior parte dei dati del case.  
  
     Se ad esempio si tenta di identificare i raggruppamenti del cliente, è possibile scegliere la dimensione Customer, se si tenta di analizzare gli acquisti nelle transazioni, è possibile scegliere la dimensione Dettagli ordine vendita Internet. Non si è limitati all'utilizzo dei soli dati di questa dimensione, tuttavia dovrebbe contenere attributi importanti per l'utilizzo nell'analisi.  
  
     Scegliere **Avanti**.  
  
6.  Nella pagina **Selezione chiave del case** , in **Attributi**, selezionare l'attributo che costituirà la chiave della struttura di data mining, quindi fare clic su **Avanti**.  
  
     In genere, l'attributo utilizzato come chiave per la struttura di data mining è anche una chiave per la dimensione e risulterà pre-selezionata.  
  
7.  Nella pagina **Selezione colonne livello case** , in **Attributi e misure correlati**, selezionare gli attributi e le misure che contengono i valori da aggiungere alla struttura di data mining come dati del case. Scegliere **Avanti**.  
  
8.  Nella pagina **Impostazione utilizzo colonne modello di data mining** , in **Struttura modello di data mining**, impostare la colonna stimabile, quindi scegliere le colonne da usare come input.  
  
    -   Selezionare la casella di controllo nella colonna più a sinistra per includere i dati nella struttura di data mining. È possibile includere le colonne nella struttura che verranno utilizzate come riferimento, ma non per l'analisi.  
  
    -   Selezionare la casella di controllo nella colonna **Input** per usare l'attributo come variabile nell'analisi.  
  
    -   Selezionare la casella di controllo nella colonna **Stima** solo per gli attributi stimabili.  
  
     Si noti che colonne definite come chiavi non possono essere utilizzate per l'input o la stima.  
  
     Scegliere **Avanti**.  
  
9. Nella pagina **Impostazione utilizzo colonne modello di data mining** è anche possibile aggiungere e rimuovere le tabelle annidate dalla struttura di data mining, usando **Aggiungi tabelle annidate** e **Tabelle annidate**.  
  
     In un modello di data mining OLAP, una tabella nidificata è un altro set di dati all'interno del cubo che presenta una relazione uno-a-molti con la dimensione che rappresenta gli attributi del case. Di conseguenza, quando viene visualizzata la finestra di dialogo, i gruppi di misure già correlati alla dimensione selezionata come tabella del case vengono preselezionati. A questo punto, si dovrebbe scegliere una dimensione diversa che contenga informazioni aggiuntive utili per l'analisi.  
  
     Ad esempio, se si analizzano i clienti, si dovrebbe usare la dimensione [Customer] come tabella del case. Per la tabella annidata, è possibile aggiungere il motivo indicato dai clienti al momento di un acquisto, incluso nella dimensione [Sales Reason].  
  
     Se si aggiungono dati nidificati, è necessario specificare due colonne aggiuntive:  
  
    -   La chiave della tabella nidificata: Questo deve essere preselezionato nella pagina **Selezione chiave tabella annidata**.  
  
    -   Gli attributi da utilizzare per l'analisi: La pagina **selezione colonne tabella nidificata**, fornisce un elenco delle misure e attributi nella selezione della tabella nidificata.  
  
        -   Per ogni attributo incluso nel modello, selezionare la casella nella colonna sinistra.  
  
        -   Se si desidera usare l'attributo solo per l'analisi, selezionare **Input**.  
  
        -   Se si desidera includere la colonna come uno degli attributi stimabili per il modello, selezionare **Stima**.  
  
        -   Qualsiasi elemento incluso nella struttura, ma non specificato come un input o attributo stimabile viene aggiunto alla struttura con il flag **Ignora**. Ciò significa che i dati vengono elaborati quando si compila il modello, ma non vengono usati nell'analisi e sono disponibili solo per il drill-through. Ciò può essere utile se si desidera includere dettagli quali i nomi dei clienti, ma non si desidera utilizzarli nell'analisi.  
  
     Fare clic su **Fine** per chiudere la parte della procedura guidata correlata alle tabelle annidate. È possibile ripetere il processo per aggiungere più colonne nidificate.  
  
10. Nella pagina **Impostazione tipo di contenuto e dati delle colonne** , in **Struttura modello di data mining**, impostare il tipo di contenuto e il tipo di dati per ogni colonna.  
  
    > [!NOTE]  
    >  I modelli di data mining OLAP non supportano l'uso della caratteristica **Rileva** per rilevare automaticamente se una colonna contiene dati continui o discreti.  
  
     Scegliere **Avanti**.  
  
11. Nella pagina **Sezionamento cubo di origine** è possibile filtrare i dati usati per creare la struttura di data mining.  
  
     Sezionando il cubo si limitano i dati utilizzati per la compilazione del modello. È ad esempio possibile compilare modelli separati per ogni area sezionando in base alla gerarchia Geography e  
  
    -   **Dimensione**: Scegliere una dimensione correlata dall'elenco a discesa.  
  
    -   **Gerarchia**:  Selezionare il livello della gerarchia della dimensione in corrispondenza del quale si desidera applicare il filtro. Ad esempio, se si seziona in base alla dimensione [Geography], è necessario scegliere un livello di gerarchia come [Region Country Name].  
  
    -   **Operatore**: Scegliere un operatore dall'elenco.  
  
    -   **Espressione filtro**: Digitare un valore o un'espressione da utilizzare come condizione di filtro oppure usare l'elenco a discesa per selezionare un valore dall'elenco dei membri al livello specificato della gerarchia.  
  
         Ad esempio, se si è selezionato [Geography] come dimensione e [Region Country Name] come livello della gerarchia, l'elenco a discesa contiene tutti i paesi validi che è possibile usare come condizione di filtro. È possibile effettuare più selezioni. Di conseguenza, i dati nella struttura di data mining saranno limitati ai dati del cubo da queste aree geografiche.  
  
    -   **Parametri**: Ignorare questa casella di controllo. Questa finestra di dialogo supporta più scenari di applicazione filtri del cubo e questa opzione non è attinente alla compilazione di una struttura di data mining.  
  
     Scegliere **Avanti**.  
  
12. Nella pagina **Divisione dei dati in set di training e in set di testing** specificare la percentuale di dati della struttura di data mining da riservare al test oppure specificare il numero massimo di test case. Scegliere **Avanti**.  
  
     Se si specificano entrambi valori, i limiti vengono combinati per utilizzare quello più basso.  
  
13. Nella pagina **Completamento procedura guidata** specificare un nome per la nuova struttura di data mining OLAP e per il modello di data mining iniziale.  
  
14. Scegliere **Fine**.  
  
15. Nella pagina **Completamento procedura guidata** è anche disponibile l'opzione per creare una dimensione del modello di data mining e/o un cubo usando la dimensione del modello di data mining. Queste opzioni sono supportate solo per i modelli compilati utilizzando gli algoritmi seguenti:  
  
    -   Algoritmo Microsoft Clustering  
  
    -   Algoritmo Microsoft Decision Trees  
  
    -   Algoritmo Microsoft Association Rules  
  
     **Crea dimensione del modello di data mining**: Selezionare questa casella di controllo e specificare un nome di tipo per la dimensione del modello di data mining. Quando si utilizza questa opzione, viene creata una nuova dimensione all'interno del cubo originale utilizzato per compilare la struttura di data mining. È possibile utilizzare questa dimensione per eseguire il drill-down ed effettuare ulteriori analisi. Poiché si trova all'interno del cubo, viene automaticamente eseguito il mapping della dimensione alla dimensione dei dati del case.  
  
     **Crea il cubo utilizzando la dimensione del modello di data mining**: Selezionare questa casella di controllo e specificare un nome per il nuovo cubo. Quando si utilizza questa opzione, viene creato un nuovo cubo contenente sia le dimensioni esistenti utilizzate nella compilazione della struttura sia la nuova dimensione di data mining contenente i risultati del modello.  
  
## <a name="see-also"></a>Vedere anche  
 [Attività e procedure relative alla struttura di data mining](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
  
