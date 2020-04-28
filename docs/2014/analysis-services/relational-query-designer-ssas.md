---
title: Progettazione query relazionale (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.bidtoolset.relquerydesginer.f1
ms.assetid: 9399b1d1-1ad2-44df-bd11-bef60fbf01ec
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d9d3ea17d614a9c5cff48c35ae1864f1672bf8bc
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "72251214"
---
# <a name="relational-query-designer-ssas"></a>Progettazione query relazionale (SSAS)
  La finestra Progettazione query relazionale consente di creare una query che specifica i dati da recuperare [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] dai [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../includes/sssdsfull-md.md)] database relazionali di [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssDWfull](../includes/ssdwfull-md.md)]e e da. Utilizzare Progettazione query con interfaccia grafica per esplorare i metadati, compilare in modo interattivo la query e visualizzarne i risultati.  Utilizzare Progettazione query basata su testo per visualizzare la query compilata nella finestra Progettazione query con interfaccia grafica o per modificare una query. È inoltre possibile importare una query esistente da un file o un report.  
  
 Se si preferisce, è possibile scrivere la query nel linguaggio SQL tramite l'editor basato su testo. Per passare alla finestra Progettazione query basata su testo, fare clic su **Modifica come testo**sulla barra degli strumenti. Una volta modificata una query in Progettazione query basata su testo, non è più possibile utilizzare finestra Progettazione query con interfaccia grafica.  
  
> [!NOTE]  
>  per specificare una query per i tipi di origine dati Oracle, OLE DB, ODBC e Teradata, è necessario utilizzare Progettazione query basata su testo.  
  
> [!IMPORTANT]  
>  Gli utenti accedono alle origini dati quando creano ed eseguono query. È necessario concedere autorizzazioni minime per le origini dati, ad esempio autorizzazioni di sola lettura.  
>   
>  Le credenziali dell'utente corrente, non quelle specificate nella pagina Impostazioni di rappresentazione, vengono utilizzate per la connessione all'origine dati quando viene eseguita una query.  
  
## <a name="graphical-query-designer"></a>Finestra Progettazione query con interfaccia grafica  
 Nella finestra Progettazione query con interfaccia grafica è possibile esplorare le tabelle e le viste dei database e compilare in modo interattivo l'istruzione SQL SELECT che consente di specificare le tabelle e le colonne del database da cui recuperare i dati per un set di dati. È possibile scegliere i campi da includere nel set di dati e, facoltativamente, specificare filtri che limitano i dati nel set di dati. È possibile specificare che i filtri vengono utilizzati come parametri e forniscono il valore del filtro in fase di esecuzione. Se si scelgono più tabelle, la finestra Progettazione query descrive la relazione tra set di due tabelle.  
  
 La finestra Progettazione query con interfaccia grafica è suddivisa in tre aree. A seconda che la query utilizzi tabelle/viste o stored procedure/funzioni con valori di tabella il layout di Progettazione query cambia.  
  
> [!NOTE]  
>  [!INCLUDE[ssDWfull](../includes/ssdwfull-md.md)] non supporta stored procedure o funzioni con valori di tabella.  
  
 Nella figura seguente è illustrata la finestra Progettazione query con interfaccia grafica nell'utilizzo con tabelle o viste.  
  
 ![Progettazione query con interfaccia grafica](media/rsqd-relational-graphical.gif "Progettazione query con interfaccia grafica")  
  
 Nella figura seguente viene illustrata la finestra Progettazione query con interfaccia grafica quando viene utilizzata con stored procedure o funzioni con valori di tabella.  
  
 ![Stored procedure nella finestra Progettazione query con interfaccia grafica](media/rs-relational-graphical-sp.gif "Stored procedure nella finestra Progettazione query con interfaccia grafica")  
  
 Nella tabella seguente viene descritta la funzione di ogni riquadro.  
  
|Riquadro|Funzione|  
|----------|--------------|  
|[Vista di database](#DatabaseView)|Consente di visualizzare gerarchicamente tabelle, viste, stored procedure e funzioni con valori di tabella organizzate in base allo schema del database.|  
|[Campi selezionati](#SelectedFields)|Visualizza l'elenco dei nomi di campo del database dagli elementi selezionati nel riquadro Vista di database. Questi campi diventano la raccolta dei campi per il set di dati.|  
|[Parametri di funzione](#FunctionParameters)|Visualizza l'elenco dei parametri di input per stored procedure o funzioni con valori di tabella presenti nel riquadro Vista di database.|  
|[Relazioni](#Relationships)|Visualizza un elenco delle relazioni derivate dai campi selezionati per tabelle o viste nel riquadro Vista di database o delle relazioni create manualmente.|  
|[Filtri applicati](#AppliedFilters)|Visualizza l'elenco dei campi e i criteri di filtro per tabelle o viste presenti nella Vista di database.|  
|[Risultati query](#QueryResults)|Visualizza i dati di esempio per il set di risultati per la query generata automaticamente.|  
  
###  <a name="database-view-pane"></a><a name="DatabaseView"></a> Riquadro Vista di database  
 Nel riquadro Vista di database vengono visualizzati i metadati per gli oggetti di database per cui si dispone delle autorizzazioni per la visualizzazione, determinate dalla connessione all'origine dati e dalle credenziali. Nella visualizzazione gerarchica, gli oggetti di database sono organizzati in base allo schema del database. Espandere il nodo di ogni schema per visualizzare tabelle, viste, stored procedure e funzioni con valori di tabella. Espandere la tabella o la vista per visualizzare le colonne.  
  
###  <a name="selected-fields-pane"></a><a name="SelectedFields"></a>Riquadro campi selezionati  
 Nel riquadro Campi selezionati sono visualizzati i campi del set di dati e i gruppi e le aggregazioni da includere nella query.  
  
 Vengono visualizzate le opzioni seguenti:  
  
-   **Campi selezionati** Visualizza i campi del database selezionati per tabelle o viste oppure i parametri di input per stored procedure o funzioni con valori di tabella. I campi visualizzati in questo riquadro diventano la raccolta dei campi per il set di dati.  
  
     Utilizzare il riquadro dei dati del report per visualizzare la raccolta di campi di un set di dati.  
  
-   **Raggruppa e aggrega** Attiva e disattiva l'uso del raggruppamento e delle aggregazioni nella query. Se la funzionalità in questione viene disabilitata dopo avere aggiunto raggruppamento e aggregazioni, questi vengono rimossi. Il testo **(nessuno)** indica che non vengono usati raggruppamenti e aggregazioni. Se questa funzionalità viene riattivata, il raggruppamento e le aggregazioni precedenti vengono ripristinati.  
  
-   **Elimina campo** Elimina il campo selezionato.  
  
#### <a name="group-and-aggregate"></a>Raggruppa e aggrega  
 Le query a database con tabelle di grandi dimensioni potrebbero restituire un numero di righe di dati eccessivo per essere utile e influenzano le prestazioni della rete in cui viene trasportata la grande quantità di dati. Per limitare il numero delle righe di dati, la query può includere aggregazioni SQL in cui sono riepilogati i dati sul server di database.  
  
 Le aggregazioni forniscono un riepilogo dei dati. Per supportare l'aggregazione che recapita i dati di riepilogo, i dati vengono raggruppati. Quando si utilizza un'aggregazione nella query, gli altri campi restituiti dalla query vengono raggruppati automaticamente e la query include la clausola SQL GROUP BY. È possibile riepilogare i dati senza aggiungere un'aggregazione semplicemente usando l'opzione **Raggruppato per** nell'elenco **Raggruppa e aggrega** . In gran parte delle aggregazioni è inclusa una versione che utilizza la parola chiave DISTINCT. L'inclusione di DISTINCT consente di eliminare i valori duplicati.  
  
 [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] USA [!INCLUDE[tsql](../includes/tsql-md.md)] [!INCLUDE[msCoName](../includes/msconame-md.md)] e [!INCLUDE[ssDWfull](../includes/ssdwfull-md.md)] USA [!INCLUDE[DWsql](../includes/dwsql-md.md)]. Entrambi i dialetti del linguaggio SQL supportano la clausola, la parola chiave e le aggregazioni fornite dalla finestra Progettazione query.  
  
 Per altre informazioni su [!INCLUDE[tsql](../includes/tsql-md.md)], vedere la [Guida di riferimento a Transact-SQL &#40;Motore di database& #41;](/sql/t-sql/language-reference) nella [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [Documentazione online](https://go.microsoft.com/fwlink/?LinkId=141687) di  sul sito msdn.microsoft.com.  
  
 Nella tabella seguente sono elencate le aggregazioni per le quali vengono fornite brevi descrizioni.  
  
|Aggregate|Descrizione|  
|---------------|-----------------|  
|Avg|Restituisce la media dei valori di un gruppo. Implementa l'aggregazione SQL AVG.|  
|Conteggio|Restituisce il numero degli elementi contenuti in un gruppo. Implementa l'aggregazione SQL COUNT.|  
|Count Big|Consente di restituire il numero di elementi di un gruppo. Si tratta dell'aggregazione SQL COUNT_BIG. La differenza tra COUNT e COUNT_BIG è che la prima restituisce sempre un valore del tipo di dati `bigint`.|  
|Min|Restituisce il valore minimo in un gruppo. Implementa l'aggregazione SQL MIN.|  
|Max|Restituisce il valore massimo in un gruppo. Implementa l'aggregazione SQL MAX.|  
|StDev|Restituisce la deviazione statistica standard di tutti i valori di un gruppo. Implementa l'aggregazione SQL STDEV.|  
|StDevP|Restituisce la deviazione statistica standard relativa al popolamento di tutti i valori nell'espressione specificata di un gruppo. Implementa l'aggregazione SQL STDEVP.|  
|SUM|Restituisce la somma di tutti i valori del gruppo. Implementa l'aggregazione SQL SUM.|  
|Var|Restituisce la varianza statistica di tutti i valori del gruppo. Implementa l'aggregazione SQL VAR.|  
|VarP|Restituisce la varianza statistica del popolamento per tutti i valori del gruppo. Implementa l'aggregazione SQL VARP.|  
|Avg Distinct|Restituisce medie univoche. Implementa una combinazione dell'aggregazione AVG e della parola chiave DISTINCT.|  
|Count Distinct|Restituisce conteggi univoci. Implementa una combinazione dell'aggregazione COUNT e della parola chiave DISTINCT.|  
|Count Big Distinct|Restituisce il conteggio univoco degli elementi contenuti in un gruppo. Implementa una combinazione dell'aggregazione COUNT_BIG e della parola chiave DISTINCT.|  
|StDev Distinct|Restituisce deviazioni statistiche standard univoche. Implementa una combinazione dell'aggregazione STDEV e della parola chiave DISTINCT.|  
|StDevP Distinct|Restituisce deviazioni statistiche standard univoche. Implementa una combinazione dell'aggregazione STDEVP e della parola chiave DISTINCT.|  
|Sum Distinct|Restituisce somme univoche. Implementa una combinazione dell'aggregazione SUM e della parola chiave DISTINCT.|  
|Var Distinct|Restituisce varianze statistiche univoche. Implementa una combinazione dell'aggregazione VAR e della parola chiave DISTINCT.|  
|VarP Distinct|Restituisce varianze statistiche univoche. Implementa una combinazione dell'aggregazione VARP e della parola chiave DISTINCT.|  
  
###  <a name="function-parameters-pane"></a><a name="FunctionParameters"></a> Riquadro Parametri di funzione  
 Nel riquadro Parametri di funzione vengono visualizzati i parametri per una stored procedure o una funzione con valori di tabella. Vengono visualizzate le colonne seguenti:  
  
-   **Nome parametro** Visualizza il nome del parametro definito dalla stored procedure o dalla funzione con valori di tabella.  
  
-   **Valore** Valore da usare per il parametro quando la query viene eseguita per recuperare dati da visualizzare nel riquadro Risultati query in fase di progettazione. Questo valore non è utilizzato in fase di esecuzione.  
  
###  <a name="relationships-pane"></a><a name="Relationships"></a> Riquadro Relazioni  
 Il riquadro Relazioni visualizza le relazioni di join. Le relazioni possono essere rilevate automaticamente dalle relazioni di chiave esterna recuperate dai metadati del database o possono essere create manualmente.  
  
 Vengono visualizzate le opzioni seguenti:  
  
-   **Rilevamento automatico** Attiva e disattiva la funzionalità di rilevamento automatico che crea automaticamente le relazioni tra tabelle. Se il rilevamento automatico è abilitato, Progettazione query crea relazioni dalle chiavi esterne delle tabelle. In caso contrario, è necessario creare le relazioni manualmente. Quando si selezionano tabelle nel riquadro **Vista di database** , la funzione di rilevamento automatico tenta di creare relazioni. Se si abilita il rilevamento automatico dopo avere creato manualmente join, tali join verranno rimossi.  
  
    > [!IMPORTANT]  
    >  Se vengono usati con [!INCLUDE[ssDWfull](../includes/ssdwfull-md.md)] , i metadati necessari a creare join non vengono forniti e non è possibile rilevare le relazioni automaticamente. Se la query recupera dati da [!INCLUDE[ssDWfull](../includes/ssdwfull-md.md)], è necessario creare tutti i join della tabella manualmente.  
  
-   **Aggiungi relazione** Aggiunge una relazione all'elenco **Relazione** .  
  
     Se il rilevamento automatico è abilitato, le tabelle, le cui colonne vengono usate nella query, vengono aggiunte automaticamente all'elenco **Relazione** . Quando il rilevamento automatico identifica la relazione tra due tabelle, una tabella viene aggiunta alla colonna **Tabella a sinistra** , l'altra alla colonna **Tabella a destra** e viene creato un inner join tra di esse. Ogni relazione genera una clausola JOIN nella query. Se le tabelle non sono correlate, vengono tutte elencate nella colonna **Tabella a sinistra** e la colonna **Tipo di join** indica che non sono correlate ad altre tabelle. Quando il rilevamento automatico è abilitato, non è possibile aggiungere manualmente relazioni tra le tabelle identificate da tale funzionalità come non correlate.  
  
     Se il rilevamento automatico è disabilitato, è possibile aggiungere e modificare le relazioni tra tabelle. Fare clic su **Modifica campi** per specificare i campi da usare per il join delle due tabelle.  
  
     L'ordine di visualizzazione delle relazioni nell'elenco **Relazione** coincide con quello di esecuzione dei join nella query. È possibile modificare l'ordine delle relazioni spostandole verso l'alto e il basso nell'elenco.  
  
     Quando si utilizzano più relazioni in una query, è necessario che a una delle tabelle di ogni relazione, ad eccezione della prima, venga fatto riferimento nelle relazioni precedenti.  
  
     Se a entrambe le tabelle di una relazione viene fatto riferimento da una relazione precedente, la relazione non genera una clausola join separata. Viene invece aggiunta una condizione di join alla clausola join generata per la relazione precedente. Il tipo di join viene derivato dalla relazione precedente che faceva riferimento alle stesse tabelle.  
  
-   **Modifica campi** Apre la finestra di dialogo **Modifica campi correlati** in cui è possibile aggiungere e modificare le relazioni tra tabelle. È possibile scegliere i campi di cui creare un join nelle tabelle a destra e a sinistra. È possibile creare un join di più campi delle tabelle a sinistra e a destra per specificare più condizioni di join in una relazione. I due campi che uniscono in join le tabelle a sinistra e a destra non devono presentare lo stesso nome. I campi di join devono presentare tipi di dati compatibili.  
  
-   **Elimina relazione**  Elimina la relazione selezionata **.**  
  
-   **Sposta su** e **Sposta giù** Consentono di spostare le relazioni verso l'alto o il basso nell'elenco **Relazione** . La sequenza di inserimento delle relazioni nella query può avere un impatto sui risultati della query. Le relazioni vengono aggiunte alla query nell'ordine in cui sono visualizzate nell'elenco **Relazione** .  
  
 Vengono visualizzate le colonne seguenti:  
  
-   **Tabella a sinistra** Visualizza il nome della prima tabella che fa parte di una relazione di join.  
  
-   **Tipo di join** Visualizza il tipo di istruzione SQL JOIN usata nella query generata automaticamente. Per impostazione predefinita, se viene rilevato un vincolo di chiave esterna, viene utilizzato INNER JOIN. Altri tipi di join possono essere LEFT JOIN o RIGHT JOIN. Se nessuno di questi tipi di join è applicabile, nella colonna **Tipo di join** viene visualizzato **Nessuna relazione**. Non vengono creati join CROSS JOIN per le tabelle non correlate. È invece necessario creare manualmente relazioni mediante la creazione di un join delle colonne presenti nelle tabelle a sinistra e a destra. Per altre informazioni su tipi di JOIN, vedere "Nozioni fondamentali sui join" nella [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [Books Online](https://go.microsoft.com/fwlink/?LinkId=141687) on msdn.microsoft.com.  
  
-   **Tabella a destra** Visualizza il nome della seconda tabella nella relazione di join.  
  
-   **Campi di join** Elenca le coppie di campi di join. Se una relazione presenta più condizioni di join, le coppie di campi di join sono separate da virgole (,).  
  
###  <a name="applied-filters-pane"></a><a name="AppliedFilters"></a> Riquadro Filtri applicati  
 Nel riquadro Filtri applicati vengono visualizzati i criteri utilizzati per limitare il numero delle righe di dati recuperate in fase di esecuzione. I criteri specificati in questo riquadro vengono utilizzati per generare una clausola SQL WHERE. Quando si seleziona l'opzione del parametro, viene creato automaticamente un parametro.  
  
 Vengono visualizzate le colonne seguenti:  
  
-   **Nome campo** Visualizza il nome del campo al quale applicare i criteri.  
  
-   **Operatore** Visualizza l'operazione da usare nell'espressione di filtro.  
  
-   **Valore** Visualizza il valore da usare nell'espressione di filtro.  
  
-   **Parametro** Visualizza l'opzione per aggiungere un parametro di query alla query.  
  
###  <a name="query-results-pane"></a><a name="QueryResults"></a> Riquadro Risultati query  
 Nel riquadro Risultati query vengono visualizzati i risultati della query generata automaticamente in base alle selezioni negli altri riquadri. Le colonne nel set di risultati sono costituite dai campi che si specificano nel riquadro Campi selezionati e i dati di riga sono limitati dai filtri che si specificano nel riquadro Filtri applicati.  
  
 Questi dati rappresentano i valori dell'origine dati al momento dell'esecuzione della query.  
  
 L'ordinamento nel set dei risultati è determinato dall'ordine in base al quale i dati vengono recuperati dall'origine dati. È possibile modificare il tipo di ordinamento modificando direttamente il testo della query. Per altre informazioni su come usare la clausola GROUP BY in una query, vedere "GROUP BY (Transact-SQL)" nella [documentazione online di SQL Server](https://go.microsoft.com/fwlink/?linkid=98335).  
  
### <a name="graphical-query-designer-toolbar"></a>Barra degli strumenti della finestra Progettazione query con interfaccia grafica  
 La barra degli strumenti della finestra Progettazione query con interfaccia grafica dispone dei pulsanti seguenti per specificare o visualizzare i risultati di una query.  
  
|Button|Descrizione|  
|------------|-----------------|  
|**Modifica come testo**|Consente di passare alla finestra Progettazione query basata su testo per visualizzare la query generata automaticamente o per modificare la query.|  
|**Importa**|Consente di importare una query esistente da un file o un report. Sono supportati i tipi di file con estensione sql e rdl.|  
|**Esegui query**|Consente di eseguire la query. Il set di risultati viene visualizzato nel riquadro Risultati query.|  
  
## <a name="understanding-automatically-generated-queries"></a>Informazioni sulle query generate automaticamente  
 Quando nel riquadro Vista di database si selezionano tabelle e colonne o stored procedure e viste, Progettazione query recupera le relazioni di chiave esterna e di chiave primaria sottostanti dallo schema del database. Grazie all'analisi di queste relazioni, Progettazione query rileva le relazioni tra due tabelle e aggiunge join alla query. È quindi possibile modificare la query aggiungendo gruppi e aggregazioni, aggiungendo o modificando relazioni e aggiungendo filtri. Per visualizzare il testo della query che mostra le colonne dalle quali recuperare i dati, i join tra tabelle e i gruppi o le aggregazioni, fare clic su **Modifica come testo**.  
  
## <a name="text-based-query-designer"></a>Finestra Progettazione query basata su testo  
 Progettazione query basata su testo consente di specificare una query utilizzando il linguaggio di query supportato dall'origine dati, eseguire la query e visualizzare i risultati in fase di progettazione. È possibile specificare più istruzioni SQL, la sintassi della query o dei comandi per estensioni per l'elaborazione dati personalizzata e query che vengono fornite come espressioni.  
  
 Poiché la finestra Progettazione query basata su testo non esegue la pre-elaborazione della query, può gestire qualsiasi tipo di sintassi della query. Rappresenta lo strumento di Progettazione query predefinito per molti tipi di origine dati.  
  
 Nella finestra Progettazione query basata su testo vengono visualizzati una barra degli strumenti e i due riquadri seguenti:  
  
-   **Query** Mostra il testo della query e il nome della tabella o della stored procedure, a seconda del tipo di query. Non tutti i tipi di query sono disponibili per tutti i tipi di origine dati. Il nome tabella, ad esempio, è supportato solo per le origini dati di tipo OLE DB.  
  
-   **Risultato** Consente di visualizzare i risultati della query eseguita in fase di progettazione.  
  
### <a name="text-based-query-designer-toolbar"></a>Barra degli strumenti di Progettazione query basata su testo  
 La finestra Progettazione query basata su testo include una sola barra degli strumenti per tutti i tipi di comandi. Nella tabella seguente sono elencati tutti i pulsanti contenuti nella barra degli strumenti con la rispettiva funzione.  
  
|Button|Descrizione|  
|------------|-----------------|  
|**Modifica come testo**|Consente di passare dalla finestra Progettazione query basata su testo alla finestra Progettazione query con interfaccia grafica e viceversa. Le finestre Progettazione query con interfaccia grafica non sono supportate da tutti i tipi di origine dati.|  
|**Importa**|Consente di importare una query esistente da un file o un report. Sono supportati solo i tipi di file con estensione sql e rdl.|  
|![Eseguire la query](media/rsqdicon-run.gif "Eseguire la query")|Consente di eseguire la query e di visualizzare il set di risultati nel riquadro Risultati.|  
|**Tipo di comando**|Selezionare **Text**, **StoredProcedure**o **TableDirect**. Se una stored procedure dispone di parametri, facendo clic su **Esegui** sulla barra degli strumenti viene visualizzata la finestra di dialogo **Definisci parametri query** ed è possibile inserire i valori desiderati.<br /><br /> Si noti che se un stored procedure restituisce più di un set di risultati, per popolare il set di dati viene utilizzato solo il primo set di risultati. Si noti anche che <br />                      **TableDirect** è disponibile solo per il tipo di origine dati OLE DB.|  
  
#### <a name="command-type-text"></a>Tipo di comando Text  
 Quando si crea un set di dati di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , per impostazione predefinita viene visualizzata la finestra Progettazione query relazionale. Per passare alla finestra Progettazione query basata su testo, fare clic sul pulsante **Modifica come testo** sulla barra degli strumenti. La finestra Progettazione query basata su testo include due riquadri, il riquadro Query e il riquadro Risultati. Nella figura seguente vengono etichettati tutti i riquadri.  
  
 ![Finestra Progettazione query standard per query di dati relazionali](media/rsqd-dsaw-sql-generic.gif "Finestra Progettazione query standard per query di dati relazionali")  
  
 Nella tabella seguente viene descritta la funzione di ogni riquadro.  
  
|Riquadro|Funzione|  
|----------|--------------|  
|Query|Consente di visualizzare il testo della query SQL. Utilizzare questo riquadro per scrivere o modificare una query SQL.|  
|Risultato|Consente di visualizzare i risultati della query. Per eseguire la query, fare clic con il pulsante destro del mouse su un riquadro qualsiasi e scegliere **Esegui**oppure fare clic sul pulsante **Esegui** sulla barra degli strumenti.|  
  
#### <a name="example"></a>Esempio  
 La query seguente restituisce l'elenco di nomi da una tabella denominata `ContactType`.  
  
```  
SELECT Name FROM ContactType  
```  
  
 Quando si fa clic su **Esegui** sulla barra degli strumenti, viene eseguito il comando nel riquadro **Query** e i risultati, un elenco di nomi, vengono visualizzati nel riquadro **Risultati** .  
  
#### <a name="command-type-storedprocedure"></a>Tipo di comando StoredProcedure  
 Quando si seleziona **Tipo di comando StoredProcedure**, la finestra Progettazione query basata su testo mostra due riquadri, il riquadro Query e il riquadro Risultati. Immettere il nome della stored procedure nel riquadro Query e fare clic su **Esegui** sulla barra degli strumenti. Se la stored procedure usa parametri, verrà visualizzata la finestra di dialogo **Definisci parametri query** . Immettere i valori dei parametri per la stored procedure.  
  
 Nella figura seguente vengono illustrati i riquadri Query e Risultati quando si esegue una stored procedure. In questo caso, i parametri di input sono costanti.  
  
 ![Stored procedure in Progettazione query basata su testo](media/rs-relational-text-sp.gif "Stored procedure in Progettazione query basata su testo")  
  
 Nella tabella seguente viene descritta la funzione di ogni riquadro.  
  
|Riquadro|Funzione|  
|----------|--------------|  
|Query|Visualizza il nome della stored procedure e di qualsiasi parametro di input.|  
|Risultato|Consente di visualizzare i risultati della query. Per eseguire la query, fare clic con il pulsante destro del mouse su un riquadro qualsiasi e scegliere **Esegui**oppure fare clic sul pulsante **Esegui** sulla barra degli strumenti.|  
  
#### <a name="example"></a>Esempio  
 La query seguente chiama la stored procedure denominata `uspGetWhereUsedProductID`. Quando la stored procedure dispone di parametri di input è necessario fornire dei valori di parametro quando si esegue la query.  
  
```  
uspGetWhereUsedProductID  
```  
  
 Fare clic sul pulsante **Esegui** (**!**). Nella tabella seguente viene fornito un esempio `uspGetWhereUsedProductID` di parametri per i quali vengono forniti valori nella finestra di dialogo **Definisci parametri query** .  
  
|||  
|-|-|  
|*\@StartProductID*|820|  
|*\@CheckDate*|20010115|  
  
#### <a name="command-type-tabledirect"></a>Tipo di comando TableDirect  
 Quando si seleziona **Tipo di comando TableDirect**, la finestra Progettazione query basata su testo mostra due riquadri, il riquadro Query e il riquadro Risultati. Quando si immette una tabella e si fa clic sul pulsante **Esegui** , vengono restituite tutte le colonne della tabella.  
  
#### <a name="example"></a>Esempio  
 Per un'origine dati di tipo OLE DB, la query del set di dati riportata di seguito restituisce un set di risultati per tutti i tipi di contatto nella tabella `ContactType`.  
  
 `ContactType`  
  
 L'immissione del nome della tabella `ContactType` è equivalente alla creazione dell'istruzione SQL `SELECT * FROM ContactType`.  
  
  
