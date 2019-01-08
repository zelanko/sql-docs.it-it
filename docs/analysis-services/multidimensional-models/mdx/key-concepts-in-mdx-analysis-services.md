---
title: Concetti chiave per MDX (Analysis Services) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bb527f78b886154372092c128e2c2a33e1eac75c
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52527816"
---
# <a name="key-concepts-in-mdx-analysis-services"></a>Concetti chiave di MDX (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Prima di usare MDX (Multidimensional Expressions) per eseguire query su dati multidimensionali o creare espressioni MDX in un cubo, è utile comprendere i concetti e i termini relativi ai dati multidimensionali.  
  
 È consigliabile iniziare da un esempio di riepilogo dei dati già noto e quindi verificare le correlazioni tra MDX e l'esempio. Ecco una tabella pivot creata in Excel, popolata con dati da un cubo di esempio Analysis Services.  
  
 ![Tabella pivot con misure e dimensioni indicate](../../../analysis-services/multidimensional-models/media/ssas-keyconcepts-pivot1-measures-dimensions.png "tabella pivot con misure e dimensioni indicate")  
  
## <a name="measures-and-dimensions"></a>Dimensioni e misure  
 Un cubo Analysis Services è costituito da misure, dimensioni e attributi di dimensione. Tutti questi elementi sono evidenti nell'esempio di tabella pivot.  
  
 Le**misure** sono valori di dati numerici trovati nelle celle, aggregati come somma, conteggio, percentuale, valore min, valore max o media. I valori di misura sono dinamici, calcolati in tempo reale, in risposta allo spostamento e all'interazione dell'utente con la tabella pivot. In questo esempio, le celle mostrano importi Reseller Sales Amounts che aumentano o diminuiscono in base all'espansione o alla compressione degli assi. Per qualsiasi combinazione di Date (espressa in anno, trimestre, mese o data) e Sales Territory (Country group, Country, Region) sarà possibile ottenere un valore Reseller Sales Amount, sommato per quel contesto specifico. Altri termini sinonimi di misure sono fatti (in data warehouse) e campi calcolati (in modelli di dati tabulari ed Excel).  
  
 Le**dimensioni** si trovano sugli assi di colonna e riga di una tabella pivot e offrono il significato delle misure. Le dimensioni sono analoghe alle tabelle in un modello di dati relazionali. Esempi comuni di dimensione includono Time, Geography, Products, Customers, Employees e così via. Questo esempio ha due dimensioni, Sales Territory sulle righe e Date nella parte superiore, ma è possibile trascinare con facilità e rilasciare altre dimensioni associate a Reseller Sales, ad esempio Promotions o Products, per visualizzare le prestazioni di vendita in base a queste dimensioni. La capacità di esplorare i dati in modi interessanti dipende dalle dimensioni create e dall'eventuale correlazione tra le dimensioni e le tabelle di fatti nell'origine dati.  
  
 Gli**attributi di dimensione** sono elementi denominati in una dimensione, analoghi alle colonne in una tabella. In questo esempio, gli attributi di dimensione Sales Territory sono costituiti da Country Group (Europe, North America, Pacific), Country (Canada, United States) e Region (Central, Northeast, Northwest, Southeast, Southwest).  
  
 A ogni attributo è associata una raccolta di valori di dati o membri. Nell'esempio i membri dell'attributo Country Group sono Europe, North America e Pacific. Il termine**membri** fa riferimento ai valori di dati effettivi appartenenti a un attributo.  
  
> [!NOTE]  
>  Un aspetto della modellazione dati consiste nel formalizzare gli schemi e le relazioni già esistenti tra i dati stessi. Quando si usano dati che rientrano in una gerarchia naturale, ad esempio dati relativi ad aree geografiche-paesi-città, è possibile formalizzare la relazione creando una **relazione tra attributi**. Una relazione tra attributi è una relazione uno-a-molti tra attributi, ad esempio una relazione tra una città e uno stato: uno stato include infatti molte città ma una città appartiene a un solo stato. Creazione di relazioni tra attributi nel modello velocizza le prestazioni delle query, pertanto è consigliabile crearle, se i dati le supportano. È possibile creare una relazione tra attributi in Progettazione dimensioni in SQL Server Data Tools. Vedere [Define Attribute Relationships](../../../analysis-services/multidimensional-models/attribute-relationships-define.md).  
  
 In Excel i metadati del modello sono visualizzati nell'elenco di campi della tabella pivot.  Confrontare la tabella pivot riportata sopra con i campi elencati sotto. Si noti che l'elenco di campi include Sales Territory, Group, Country, Region (metadati), mentre la tabella pivot include solo i membri (valori di dati). Se si conosce l'aspetto delle icone, sarà possibile correlare con maggiore facilità le parti di un modello multidimensionale a una tabella pivot in Excel.  
  
 ![Elenco campi tabella pivot](../../../analysis-services/multidimensional-models/mdx/media/ssas-keyconcepts-ptfieldlist.png "elenco campi tabella pivot")  
  
## <a name="attribute-hierarchies"></a>Gerarchie di attributi  
 La disposizione dei valori in una tabella pivot è molto intuitiva. I valori si spostano verso l'alto o verso il basso quando si espandono e comprimono i livelli in ogni asse. Questo comportamento è dovuto alle gerarchie di attributi.  
  
 Comprimere tutti i livelli e verificare i totali complessivi per ogni Country Group e Calendar Year. Questo valore è derivato da un **membro (Totale)** in una gerarchia. Il membro (Totale) è il valore calcolato di tutti i membri in una gerarchia dell'attributo.  
  
-   Il membro (Totale) per tutti i Country Groups e Dates combinati è $80.450.596,98.  
  
-   Il membro (Totale) per CY2008 è $16.038.062,60.  
  
-   Il membro (Totale) Pacific è $1.594.335,38.  
  
 Aggregazioni come questa sono precalcolate e archiviate in anticipo e contribuiscono alla velocità delle prestazioni di query di Analysis Services.  
  
 ![Tabella pivot con tutti i membri indicate](../../../analysis-services/multidimensional-models/mdx/media/ssas-keyconcepts-pivot2-allmember.png "tabella pivot con tutti i membri indicate")  
  
 Espandere la gerarchia fino ad arrivare al livello più basso. Si tratta del **membro foglia**. Un membro foglia è un membro senza figli di una gerarchia. In questo esempio Australia membro foglia.  
  
 ![Tabella pivot con callout membro foglia](../../../analysis-services/multidimensional-models/mdx/media/ssas-keyconcepts-pivot3-leafparent.PNG "tabella pivot con callout membro foglia")  
  
 Qualsiasi membro superiore è definito **membro padre**. Pacific è padre di Australia.  
  
 **Componenti di una gerarchia dell'attributo**  
  
 Tutti questi concetti contribuiscono a illustrare il concetto di **gerarchia dell'attributo**. Una gerarchia dell'attributo è un albero di membri dell'attributo che contiene i livelli seguenti:  
  
-   Un livello foglia contenente ogni singolo membro dell'attributo, con ogni membro del livello foglia noto anche come **membro foglia**.  
  
-   Livelli intermedi, se la gerarchia dell'attributo è una gerarchia padre-figlio, come illustrato in seguito.  
  
-   Un membro (Totale) che include il valore aggregato di tutti gli attributi figlio. Facoltativamente, è possibile nascondere o disattivare il livello (totale) quando non ha senso per i dati. Ad esempio, anche se il codice prodotto è numerico, non avrebbe senso somma o Media o in caso contrario, l'aggregazione di tutti i valori Product Codes.  
  
> [!NOTE]  
>  Gli sviluppatori BI impostano spesso proprietà sulla gerarchia dell'attributo per ottenere determinati comportamenti nelle applicazioni client o per ottenere alcuni vantaggi a livello di prestazioni. Ad esempio, è necessario impostare AttributeHierarchyEnabled = False su attributi per il quale il membro (totale) non ha senso. In alternativa, è possibile che si voglia semplicemente nascondere il membro (Totale). In questo caso, impostare AttributeHierarchyVisible=False. Per altri dettagli sulle proprietà, vedere [Dimension Attribute Properties Reference](../../../analysis-services/multidimensional-models/dimension-attribute-properties-reference.md) .  
  
## <a name="navigation-hierarchies"></a>Gerarchie di navigazione  
 In una tabella pivot, almeno in questo esempio, gli assi di riga e di colonna si espandono per mostrare livelli inferiori di attributi. È possibile ottenere un albero espandibile tramite gerarchie di navigazione create in un modello.  Nel modello di esempio AdventureWorks la dimensione Sales Territory include una gerarchia con più livelli che inizia con Country Group, quindi prosegue con Country e infine Region.  
  
 Come si può notare, le gerarchie permettono di specificare un percorso di navigazione in una tabella pivot o in altri oggetti di riepilogo dei dati. Sono disponibili due tipi di base: bilanciata e non bilanciata.  
  
 **Gerarchie bilanciate**  
  
|||  
|-|-|  
|![Tabella pivot con callout gerarchia bilanciata indicata](../../../analysis-services/multidimensional-models/mdx/media/ssas-keyconcepts-pivot4-balancedhierarchy.PNG "tabella pivot con callout gerarchia bilanciata indicata")|Una **gerarchia bilanciata** è una gerarchia in cui tra il livello principale e qualsiasi membro foglia esiste lo stesso numero di livelli.<br /><br /> Una **gerarchia naturale** è una gerarchia che emerge naturalmente dai dati sottostanti. Un esempio comune è costituito da Country-Region-State o Year-Month-Date o Category-Subcategory-Model, in cui ogni livello subordinato emerge in modo prevedibile dal padre.<br /><br /> In un modello multidimensionale, la maggior parte delle gerarchie è costituita da gerarchie bilanciate e molte di esse sono anche gerarchie naturali.<br /><br /> Un altro termine di modellazione correlato è **gerarchia definita dall'utente**, usato spesso in contrapposizione alle gerarchie di attributi. Indica semplicemente una gerarchia creata dallo sviluppatore BI, in contrapposizione con le gerarchie di attributi generate automaticamente da Analysis Services quando si definisce un attributo.|  
  
 **Gerarchie sbilanciate**  
  
|||  
|-|-|  
|![Tabella pivot con gerarchia incompleta indicata](../../../analysis-services/multidimensional-models/mdx/media/ssas-keyconcepts-pivot15-raggedhierarchy.PNG "tabella pivot con gerarchia incompleta indicata")|Una **gerarchia incompleta** o **gerarchia sbilanciata** è una gerarchia in cui tra il livello principale e i membri foglia esistono numeri di livelli diversi. Anche in questo caso si tratta di una gerarchia creata dallo sviluppatore BI, ma in questo caso sono presenti gap nei dati.<br /><br /> Nel modello di esempio AdventureWorks Sales Territory illustra una gerarchia incompleta, perché United States ha un livello aggiuntivo (Regions) che non esiste per altri paesi in questo esempio.<br /><br /> Le gerarchie incomplete costituiscono un problema per gli sviluppatori BI se l'applicazione client non le gestisce in modo appropriato. Nel modello di Analysis Services è possibile creare una **gerarchia padre-figlio** che definisce in modo esplicito una relazione tra dati multilivello, eliminando qualsiasi ambiguità in merito alle relazioni tra un livello e il livello successivo. Per altri dettagli, vedere [Dimensioni padre-figlio](../../../analysis-services/multidimensional-models/parent-child-dimension.md) .|  
  
## <a name="key-attributes"></a>Attributi chiave  
 I modelli sono una raccolta di oggetti correlati che si basano su chiavi e indici per creare le associazioni. I modelli Analysis Services non sono diversi. Per ogni dimensione, che è uguale a una tabella in un modello relazionale, è presente un attributo chiave. L' **attributo** chiave è usato nelle relazioni di chiave esterna con la tabella dei fatti (gruppo di misure). Tutti gli attributi non chiave della dimensione sono collegati, direttamente o indirettamente, all'attributo chiave.  
  
 Spesso, ma non sempre, l'attributo chiave è anche l' **attributo di granularità**. La granularità indica il livello di dettaglio o di precisione nei dati. Anche in questo caso un esempio semplifica la comprensione di questo concetto. Esaminare i valori relativi alle date. Per le vendite giornaliere sono necessari valori di dati specificati in modo giornaliero. Per le quote, potrebbero essere sufficienti valori di dati trimestrali, ma se i dati analitici sono costituiti dai risultati di una competizione sportiva, è possibile che la granularità corrisponda ai millisecondi. Il livello di precisione dei valori di dati corrisponde alla granularità.  
  
 Valuta è un altro esempio: un'applicazione finanziaria tenga traccia dei valori monetari con a molte cifre decimali, mentre raccolta fondi della tua scuola locali potrebbero essere sufficienti valori al dollaro più vicino. La comprensione della granularità è importante, perché è consigliabile evitare di archiviare dati non necessari. L'eliminazione di millisecondi da un timestamp o di centesimi da un importo di vendita può permettere di risparmiare tempo di archiviazione ed elaborazione quando un livello così specifico di dati non è rilevante ai fini dell'analisi.  
  
 Per impostare l'attributo di granularità, usare la tabella Utilizzo dimensioni in Progettazione cubi in SQL Server Data Tools. Nel modello di esempio AdventureWorks l'attributo chiave della dimensione Date è la chiave Date. Per Sales Orders l'attributo di granularità equivale all'attributo chiave. Per Sales Targets il livello di granularità è trimestrale, quindi l'attributo di granularità è impostato su Calendar Quarter.  
  
 ![Modello che mostra l'attributo di granularità](../../../analysis-services/multidimensional-models/mdx/media/ssas-keyconcepts-granularityattrib.png "modello che mostra l'attributo di granularità")  
  
> [!NOTE]  
>  Se l'attributo di granularità e l'attributo chiave sono diversi, tutti gli attributi non chiave devono essere collegati, direttamente o indirettamente, all'attributo di granularità. All'interno di un cubo l'attributo di granularità definisce la granularità di una dimensione.  
  
## <a name="query-scope-cube-space"></a>Ambito della query (spazio del cubo)  
 L'ambito di una query fa riferimento ai limiti entro cui i dati sono selezionati. Può includere l'intero cubo (un cubo è l'oggetto query più grande) o una sola cella.  
  
 Lo**spazio del cubo** è il prodotto dei membri delle gerarchie dell'attributo di un cubo per le misure del cubo.  
  
 Un**sottocubo** è un subset di un cubo che rappresenta una vista filtrata del cubo. I sottocubi possono essere definiti con un'istruzione Scope nello script di calcolo MDX o in una clausola di selezione secondaria (sub-SELECT) di una query MDX o come un cubo di sessione.  
  
 Con**cella** si intende lo spazio che si trova al punto di intersezione tra un membro della dimensione Measures e un membro di ogni gerarchia dell'attributo di un cubo.  
  
## <a name="other-modeling-terms"></a>Altri termini di modellazione  
 In questa sezione è una raccolta di concetti e termini che non rientrano nelle altre sezioni, ma è necessario conoscere.  
  
 Un**membro calcolato** è un membro della dimensione definito e calcolato in fase di query. È possibile definire un membro calcolato in una query dell'utente o nello script di calcolo MDX e archiviarlo sul server. Un membro calcolato corrisponde alle righe della tabella della dimensione nella dimensione in cui viene definito.  
  
 **Distinct Count** è un tipo speciale di misura ed è usato per elementi di dati da contare una sola volta. Il modello di esempio AdventureWorks incluse misure Distinct Count per Internet Orders, Reseller Orders e Sales Orders.  
  
 I**gruppi di misure** sono raccolte di una o più misure. Nella maggior parte dei casi sono definiti dagli utenti e sono usati per raggruppare misure correlate. Le misure Distinct Count costituiscono un'eccezione. Sono sempre incluse in un gruppo dedicato di misure, che contiene solo le misure Distinct Count. Non è possibile visualizzare il gruppo di misure nella figura di esempio di tabella pivot, ma viene visualizzato in un elenco di campi tabella pivot, come una raccolta denominata di misure.  
  
 Una**dimensione Measures** è la dimensione che contiene tutte le misure di un cubo. Non è esposta in un modello multidimensionale che si compila in SQL Server Data Tools, ma esistente nello stesso. Poiché contiene misure, tutti i membri di una dimensione Measures sono in genere aggregati, tramite somma o conteggio.  
  
 **Dimensioni del database e del cubo**. In un modello è possibile definire dimensioni autonome, che sono quindi incluse in alcuni cubi dello stesso modello. Quando si aggiunge una dimensione a un cubo, viene definito una dimensione del cubo. Trova da sola in un progetto, come elemento autonomo in Esplora oggetti viene definito una dimensione del database. Questa distinzione è importante perché le proprietà corrispondenti sono impostate in modo indipendente. Nella documentazione del prodotto, si noterà usati entrambi i termini è quindi utile per comprenderne il significato.  
  
## <a name="next-steps"></a>Passaggi successivi  
 Sono stati illustrati concetti essenziali e terminologia importante. É quindi possibile passare agli argomenti aggiuntivi che illustrano in modo più dettagliato i concetti fondamentali relativi ad Analysis Services:  
  
-   [Query MDX di base &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-the-basic-query.md)  
  
-   [Script MDX di base &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md)  
  
-   [Modellazione multidimensionale &#40;esercitazione di AdventureWorks&#41;](../../../analysis-services/multidimensional-modeling-adventure-works-tutorial.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Cube Space](../../../analysis-services/multidimensional-models/mdx/cube-space.md)   
 [Tuple](../../../analysis-services/multidimensional-models/mdx/tuples.md)   
 [Autoexists](../../../analysis-services/multidimensional-models/mdx/autoexists.md)   
 [Utilizzo di membri, tuple e set &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/working-with-members-tuples-and-sets-mdx.md)   
 [Totali visualizzati e non visualizzati](../../../analysis-services/multidimensional-models/mdx/visual-totals-and-non-visual-totals.md)   
 [Nozioni fondamentali sulle query MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)   
 [Nozioni fondamentali sullo scripting MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-scripting-fundamentals-analysis-services.md)   
 [Guida di riferimento al linguaggio MDX &#40;MDX&#41;](../../../mdx/mdx-language-reference-mdx.md)   
 [Guida di riferimento a MDX &#40;Multidimensional Expressions&#41;](../../../mdx/multidimensional-expressions-mdx-reference.md)  
  
  
