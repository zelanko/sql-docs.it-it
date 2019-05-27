---
title: Creare una struttura di Data Mining OLAP | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 21cbdc9d-d33c-4026-b9ef-1be2bd92b3b1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: adf29f6f73020ddc265072b3b9f3f67042200506
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66085245"
---
# <a name="create-an-olap-mining-structure"></a>Create an OLAP Mining Structure
  La creazione di un modello di data mining basato su un cubo OLAP o un altro archivio dati multidimensionale presenta numerosi vantaggi. Una soluzione OLAP contiene già enormi quantità di dati ben organizzati, puliti e formattati correttamente; tuttavia, la complessità dei dati è tale che difficilmente gli utenti possono trovare modelli significativi tramite l'esplorazione ad hoc. Il data mining consente di individuare nuove correlazioni e fornire informazioni su cui è possibile eseguire azioni.  
  
 In questo argomento viene descritto come creare una struttura di data mining OLAP, basata su una dimensione e misure correlate in una soluzione multidimensionale esistente.  
  
 [Requisiti](#bkmk_Reqs)  
  
 [Cenni preliminari sul processo di data mining OLAP](#bkmk_Overview)  
  
 [Scenari per l'utilizzo del data mining nelle soluzioni OLAP](#bkmk_OLAP_Scenarios)  
  
 [Filtri](#bkmk_Filters)  
  
 [Utilizzo di tabelle nidificate](#bkmk_Nested)  
  
 [Dimensioni di data mining](#bkmk_DMDimension)  
  
##  <a name="bkmk_Reqs"></a> Requisiti per la struttura e i modelli di data mining OLAP  
 Se si progetta un modello di data mining OLAP, l'origine dati esiste già nel database utilizzato per compilare il cubo. Non è possibile connettersi a un cubo remoto e compilare oggetti di data mining; gli oggetti del cubo devono essere disponibili all'interno della stessa soluzione di database della struttura di data mining che viene compilata.  
  
 Se non si dispone dei file di progetto originali o non si vuole modificarli, è possibile usare l'opzione di Visual Studio **Importa da server (multidimensionale o data mining)** per ottenere una copia dei metadati e degli oggetti della soluzione. È quindi possibile modificare la destinazione di distribuzione e le origini dati e utilizzare gli oggetti del cubo senza influire sugli oggetti esistenti.  
  
 Per altre informazioni, vedere [Importare un progetto di data mining usando l'Importazione guidata di Analysis Services](import-a-data-mining-project-using-the-analysis-services-import-wizard.md).  
  
##  <a name="bkmk_Overview"></a> Cenni preliminari sul processo di data mining OLAP  
 Avviare la Creazione guidata modello di data mining facendo clic con il pulsante destro del mouse sul nodo **Strutture di data mining** in Esplora soluzioni e scegliendo  **Nuova struttura di data mining**. La procedura guidata consente di eseguire in modo semplificato i passaggi indicati di seguito per la creazione di una nuova struttura e un nuovo modello:  
  
1.  **Selezione metodo di definizione**: Consente di selezionare una data tipo di origine e scegliere **da cubo esistente**.  
  
    > [!NOTE]  
    >  Il cubo OLAP utilizzato come origine deve esistere all'interno dello stesso database della struttura di data mining, come descritto sopra. Inoltre, non è possibile utilizzare un cubo creato dal componente aggiuntivo PowerPivot per Excel come origine per il data mining.  
  
2.  **Creare la struttura di Data Mining**: Determinare se verrà compilata solo una struttura o una struttura con un modello di data mining.  
  
     È inoltre necessario scegliere un algoritmo appropriato per l'analisi dei dati. Per informazioni aggiuntive sull'algoritmo migliore per determinate attività, vedere HYPERLINK "ms-help://SQL111033/as_1devconc/html/ed1fc83b-b98c-437e-bf53-4ff001b92d64.htm" Algoritmi di data mining (Analysis Services - Data mining).  
  
3.  **Selezione dimensione cubo di origine**: Questo passaggio è quello utilizzato per la selezione di un'origine dati. È necessario scegliere la singola dimensione che contiene i dati più importanti utilizzati per il training del modello. È possibile aggiungere dati da altre dimensioni in un secondo momento oppure filtrare la dimensione.  
  
4.  **Selezione chiave del Case**: All'interno della dimensione appena selezionata, scegliere un attributo (colonna) da usare come identificatore univoco per i dati del case.  
  
     Una colonna sarà in genere preselezionata, ma è possibile modificarla se sono presenti più chiavi.  
  
5.  **Selezione colonne livello Case**: Qui si scelgono gli attributi dalla dimensione selezionata e le misure correlate, rilevanti per l'analisi. Questo passaggio equivale alla selezione di colonne da una tabella.  
  
     Nella creazione guidata sono automaticamente incluse per la revisione e la selezione eventuali misure create utilizzando gli attributi dalla dimensione selezionata.  
  
     Ad esempio, se il cubo contiene una misura che calcola il costo di spedizione in base alla posizione geografica del cliente e si sceglie la dimensione Customer come origine dati principale per la modellazione, la misura sarà proposta come candidato per l'aggiunta al modello. Prestare attenzione ad aggiungere troppe misure già basate direttamente sugli attributi, poiché esiste già una relazione implicita tra le colonne, come definito nella formula della misura, e la forza di questa correlazione (prevista) può nascondere altre relazioni che diversamente si potrebbero individuare.  
  
6.  **Specificare l'utilizzo colonne modello di Data Mining**: Per ogni attributo o misura aggiunta alla struttura, è necessario specificare se l'attributo deve essere utilizzato per la stima o utilizzato come input. Se non si seleziona una di queste opzioni, i dati verranno elaborati ma non saranno utilizzati per l'analisi; tuttavia, saranno disponibili come dati in background nel caso successivamente si abiliti il drill-through.  
  
7.  **Aggiungi tabelle nidificate**: Fare clic per aggiungere tabelle correlate. Nella finestra di dialogo **Selezione dimensione gruppo di misure** è possibile scegliere una singola dimensione tra quelle correlate alla dimensione corrente.  
  
     Successivamente, utilizzare la finestra di dialogo **Seleziona colonna chiave tabella nidificata** per definire la modalità di correlazione della nuova dimensione alla dimensione che contiene i dati del case.  
  
     Utilizzare la finestra di dialogo **Selezione colonne tabella nidificata** per scegliere gli attributi e le misure dalla nuova dimensione che si intende utilizzare nell'analisi. È inoltre necessario specificare se l'attributo nidificato sarà utilizzato per la stima.  
  
     Dopo avere aggiunto tutti gli attributi nidificati che potrebbero essere necessari, tornare alla pagina **Impostazione utilizzo colonne modello di data mining**e fare clic su **Avanti**.  
  
8.  **Specificare il contenuto delle colonne e tipo di dati**: A questo punto, sono stati aggiunti tutti i dati che verranno utilizzati per l'analisi e devono specificare il *tipo di dati* e *tipo di contenuto* per ogni attributo.  
  
     In un modello OLAP non è possibile rilevare automaticamente i tipi di dati, perché il tipo di dati è già definito dalla soluzione multidimensionale e non può essere modificato. Anche le chiavi vengono identificate automaticamente. Per altre informazioni, vedere [Tipi di dati &#40;data mining&#41;](data-types-data-mining.md).  
  
     Il *tipo di contenuto* scelto per ogni colonna utilizzata nel modello indica all'algoritmo in che modo devono essere elaborati i dati. Per altre informazioni, vedere [Tipi di contenuto &#40;Data mining&#41;](content-types-data-mining.md).  
  
9. **Sezionamento cubo di origine**: Qui è possibile definire filtri in un cubo per selezionare solo un subset di dati e il training dei modelli più interessati.  
  
     Per filtrare un cubo scegliere la dimensione in base a cui filtrare, selezionare il livello della gerarchia che contiene i criteri da utilizzare, quindi digitare una condizione da utilizzare come filtro.  
  
10. **Creare Set di Testing**: In questa pagina, è possibile definire nella procedura guidata la quantità di dati da mettere da utilizzare nel test del modello. Se i dati supporteranno più modelli, è consigliabile creare un set di dati di controllo, in modo da poter eseguire il test di tutti i modelli sugli stessi dati.  
  
     Per altre informazioni, vedere [Test e convalida &#40;Data mining&#41;](testing-and-validation-data-mining.md).  
  
11. **Completamento procedura guidata**: In questa pagina, si assegna un nome alla nuova struttura di data mining e il modello di data mining associato e salvano struttura e modello.  
  
     In questa pagina è inoltre possibile impostare le opzioni seguenti:  
  
    -   **Consenti drill-through**  
  
    -   **Crea dimensione del modello di data mining**  
  
    -   **Crea il cubo utilizzando la dimensione del modello di data mining**  
  
     Per ulteriori informazioni su queste opzioni, vedere la sezione [Informazioni sulle dimensioni di data mining e sul drill-through](#bkmk_DMDimension)più avanti in questo argomento.  
  
 In questa fase la struttura di data mining e il modello sono esclusivamente metadati; sarà necessario elaborarli entrambi per ottenere risultati.  
  
##  <a name="bkmk_OLAP_Scenarios"></a> Scenari per l'utilizzo del data mining con dati OLAP  
 I cubi OLAP contengono spesso un numero talmente elevato di membri e dimensioni da rendere difficile la comprensione del punto di inizio del data mining. Per identificare i modelli inclusi nei cubi, in genere è necessario identificare una sola dimensione desiderata, quindi iniziare a esplorare i modelli correlati alla dimensione. Nella tabella seguente sono elencate diverse attività comuni di data mining OLAP e vengono descritti gli scenari di esempio in cui è possibile applicare ogni attività identificando l'algoritmo di data mining corrispondente da utilizzare.  
  
|Attività|Scenario di esempio|Algoritmo|  
|----------|---------------------|---------------|  
|Raggruppamento di membri in cluster|Segmentare una dimensione relativa ai clienti in base alle proprietà del membro corrispondente, ai prodotti acquistati dai clienti e alla quantità di denaro spesa dai clienti.|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Clustering|  
|Ricerca di membri interessanti o anomali|Identificare membri interessanti o anomali in una dimensione relativa ai negozi in base a vendite, profitti, ubicazione e dimensioni del punto vendita.|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Decision Trees|  
|Ricerca di celle interessanti o anomale|Identificare le vendite dei negozi che risultano controcorrente rispetto alle tendenze tipiche registrate nel tempo.|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Time Series|  
|Trovare le correlazioni|Identificare i fattori correlati al tempo di inattività del server, tra cui area, tipo di computer, sistema operativo o data di acquisto.|[!INCLUDE[msCoName](../../includes/msconame-md.md)] Naive Bayes|  
  
##  <a name="bkmk_Filters"></a> Un cubo e di sezionamento. applicazione di filtri ai modelli  
 Il sezionamento del cubo mentre si compila un modello equivale alla creazione di un filtro su un modello di data mining relazionale. In un modello relazionale il filtro sull'origine dati è definito come clausola WHERE su un'istruzione SQL; in un cubo si usa l'editor per creare istruzioni di filtro mediante MDX.  
  
 Ad esempio, un cubo potrebbe contenere informazioni sugli acquisti di prodotti in tutto il mondo, ma per una campagna di marketing si desidera creare un modello basato sull'analisi dei clienti di sesso femminile oltre i 30 anni che vivono nel Regno Unito.  
  
 In questo scenario si creerebbero due filtri:  
  
-   Per il primo filtro, potrebbe scegliere la dimensione Geography, scegliere la gerarchia per Region e quindi usare il **espressione di filtro** elenco per scegliere "United Kingdom" tra i valori possibili.  
  
-   Per il secondo filtro scegliere la dimensione Customer, selezionare l'attributo Gender e quindi "Female" dall'elenco di valori di attributo.  
  
 Dopo avere creato la struttura di data mining, è possibile modificare sia la definizione dei dati del cubo sia i criteri di filtro. Per altre informazioni, vedere [filtrare il cubo di origine per una struttura di Data Mining](../filter-the-source-cube-for-a-mining-structure.md).  
  
 Sia la scheda **Struttura di data mining** che la scheda **Modello di data mining** contengono un'opzione per l'aggiunta di un filtro a una struttura di data mining esistente, facendo clic su **Definisci una sezione del cubo**. Nella finestra di dialogo **Seziona cubo** è possibile compilare un'espressione di filtro MDX valida scegliendo un valore dagli elenchi a discesa.  
  
> [!WARNING]  
>  Si noti che l'interfaccia per la progettazione e l'esplorazione dei cubi è stata modificata in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Per altre informazioni, vedere [Esplorare dati e metadati in un cubo](../multidimensional-models/browse-data-and-metadata-in-cube.md).  
  
 Nel cubo è possibile aggiungere il numero di filtri necessari per restituire i dati desiderati per il modello di data mining. È inoltre possibile definire sezioni di singole sezioni del cubo. Se, ad esempio, la struttura contiene due tabelle nidificate basate sui prodotti, è possibile sezionare una tabella in corrispondenza del mese di marzo 2004 e l'altra tabella in corrispondenza del mese di aprile 2004. È quindi possibile utilizzare il modello risultante per stimare gli acquisti effettuati ad aprile in base agli acquisti effettuati a marzo.  
  
##  <a name="bkmk_Nested"></a> Utilizzo di tabelle nidificate in un modello di data mining OLAP  
 Quando si utilizza Creazione guidata modello di data mining per compilare un modello basato su dati del cubo, è possibile aggiungere tabelle nidificate specificando i nomi delle dimensioni correlate e scegliendo gli attributi o le misure da aggiungere al modello.  
  
 Ad esempio, se la dimensione principale usata per i dati del case è Customer, è possibile aggiungere come dimensione correlata la dimensione Products, poiché si prevede che un cliente possa avere acquistato più prodotti nel tempo e nel cubo ogni cliente è già collegato ai diversi prodotti tramite le tabelle dei fatti degli ordini.  
  
 Le tabelle nidificate vengono aggiunte nella pagina **Impostazione utilizzo colonne modello di data mining** della procedura guidata, facendo clic su **Aggiungi tabelle nidificate**. Verrà visualizzata una finestra di dialogo che agevola il processo di scelta di una dimensione correlata e di eventuali misure. Il case e le dimensioni nidificate devono essere correlati da una chiave esterna e le misure devono utilizzare uno degli attributi già inclusi nel case o nelle tabelle nidificate. Sfortunatamente, queste restrizioni in realtà non molto per restringere l'ambito, pertanto è necessario prestare attenzione a selezionare solo gli attributi che sono utili per la modellazione.  
  
 Per ogni attributo o misura che si aggiunge alla tabella nidificata, è necessario specificare se l'attributo nidificato sarà utilizzato o meno per la stima, selezionando **Stimabile** o **Input** nella finestra di dialogo **Selezione colonne tabella nidificata** . Se non si seleziona una di queste opzioni, i dati verranno aggiunti alla struttura di data mining senza essere utilizzati per l'analisi.  
  
 Per ogni attributo e misura, è inoltre necessario specificare se l'attributo è discreto, discretizzato o continuo. Nella procedura guidata verrà preselezionato un valore predefinito in base al tipo di dati dell'attributo, ma potrebbe essere necessario modificare questa selezione, a seconda dei requisiti dell'algoritmo. Se si sceglie un tipo di contenuto che non è compatibile con l'algoritmo scelto (ad esempio, si utilizza un tipo numerico continuo con un modello Naïve Bayes), si otterranno un messaggio di errore fino a quando non si tenta di elaborare il modello.  
  
 Al termine dell'importazione di queste opzioni, la tabella nidificata verrà aggiunta alla tabella del case tramite la procedura guidata. Il nome predefinito della tabella nidificata corrisponde al nome della dimensione nidificata. È tuttavia possibile rinominare sia la tabella nidificata che le colonne corrispondenti. È possibile ripetere il processo per aggiungere più tabelle nidificate alla struttura di data mining.  
  
 La possibilità di utilizzare dati delle tabelle nidificate in questo modo è una funzionalità particolarmente efficace del data mining di SQL Server e in un cubo ci sono possibilità praticamente illimitate di utilizzare i subset di dati correlati.  
  
##  <a name="bkmk_DMDimension"></a> Informazioni sulle dimensioni di data mining e sul drill-through  
 L'opzione **Consenti drill-through**consente di eseguire query nei dati del cubo sottostante durante l'esplorazione del modello. I dati non sono contenuti nella nuova dimensione di data mining, ma nel database [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è possibile utilizzare le associazioni dati per recuperare le informazioni dal cubo di origine.  
  
 L'opzione **Crea dimensione del modello di data mining**consente di generare una nuova dimensione all'interno del cubo esistente che contiene i modelli individuati dall'algoritmo. La gerarchia all'interno della nuova dimensione è determinata in gran parte dal tipo di modello. Ad esempio, la rappresentazione di un modello di clustering è piuttosto lineare, con il nodo (Tutto) in cima alla gerarchia e ogni cluster al livello successivo. Al contrario, la dimensione creata per un modello ad albero delle decisioni può avere una gerarchia molto profonda, che rappresenta le diramazioni dell'albero.  
  
 L'opzione **Crea il cubo utilizzando la dimensione del modello di data mining**consente di esportare la nuova dimensione di data mining in un nuovo cubo. Qualsiasi oggetto necessario per il drill-through sulla dimensione di data mining verrà incluso automaticamente.  
  
> [!WARNING]  
>  Solo questi tipi di modelli supportano la creazione di dimensioni di data mining: modelli basati sull'algoritmo Microsoft Clustering, Microsoft Decision Trees o Microsoft Association.  
  
## <a name="see-also"></a>Vedere anche  
 [Algoritmi di data mining &#40;Analysis Services - Data mining&#41;](data-mining-algorithms-analysis-services-data-mining.md)   
 [Colonne della struttura di data mining](mining-structure-columns.md)   
 [Colonne del modello di data mining](mining-model-columns.md)   
 [Proprietà dei modelli di data mining](mining-model-properties.md)   
 [Proprietà delle strutture di data mining e delle colonne delle strutture di data mining](properties-for-mining-structure-and-structure-columns.md)  
  
  
