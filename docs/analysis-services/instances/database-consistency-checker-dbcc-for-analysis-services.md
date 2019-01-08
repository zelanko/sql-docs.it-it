---
title: Database Consistency Checker (DBCC) per Analysis Services | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bc158c0c5ba35da95fe3bf1af688e12a7b162045
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52413088"
---
# <a name="database-consistency-checker-dbcc-for-analysis-services"></a>Database Consistency Checker (DBCC) per Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  DBCC fornisce la convalida su richiesta dei database multidimensionali e tabulari in un'istanza di Analysis Services. È possibile eseguire DBCC in una finestra di query MDX o XMLA in SQL Server Management Studio (SSMS) e tracciare l'output di DBCC in SQL Server Profiler o in sessioni xEvent di SSMS.  
Il comando accetta una definizione di oggetto e restituisce un set di risultati vuoto o informazioni dettagliate sull'errore se l'oggetto è danneggiato.   In questo articolo, si sarà informazioni su come eseguire il comando, interpretare i risultati e risolvere eventuali problemi.  
  
 Per i database tabulari, le verifiche di coerenza eseguite da DBCC equivalgono alla convalida predefinita eseguita automaticamente ogni volta che si ricarica, si sincronizza o si ripristina un database.  Al contrario, le verifiche di coerenza per i database multidimensionali si verificano solo quando si esegue DBCC su richiesta.  
  
 La gamma di controlli di convalida varia in base alla modalità. I database tabulari sono infatti soggetti a una gamma più ampia di controlli.  
 Anche le caratteristiche di un carico di lavoro DBCC variano in base alla modalità del server. Il controllo delle operazioni sui database multidimensionali comporta la lettura dei dati dal disco e la creazione di indici temporanei per il confronto con gli indici effettivi, richiedendo tempi di completamento più lunghi.  
  
 La sintassi del comando per DBCC usa metadati degli oggetti specifici del tipo di database da verificare:  
  
-   I database multidimensionali e quelli tabulari precedenti a SQL Server 2016 con livello di compatibilità 1100 o 1103 sono descritti nei costrutti di modellazione multidimensionali come **cubeID**, **measuregroupID**e **partitionID**.  
  
-   I metadati per i nuovi database modello tabulare con livello di compatibilità 1200 e superiore sono costituiti da descrittori come **NomeTabella** e **PartitionName**.  
  
 DBCC per Analysis Services viene eseguito su qualsiasi database di Analysis Services con qualsiasi livello di compatibilità, purché il database venga eseguito in un'istanza di SQL Server 2016. Assicurarsi di usare la sintassi del comando corretto per ogni tipo di database.  
  
> [!NOTE]  
>  Se si ha familiarità con [DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md), si noterà subito che l'ambito di DBCC in Analysis Services è molto più ristretto. DBCC in Analysis Services è un comando singolo che segnala esclusivamente il danneggiamento dei dati nel database o in singoli oggetti. Se si considerano altre attività, ad esempio la raccolta di informazioni, provare a usare invece script XMLA o PowerShell per AMO.
  
## <a name="permission-requirements"></a>Requisiti relativi alle autorizzazioni  
 Per eseguire il comando, è necessario essere un amministratore del server o del database di Analysis Services, ovvero un membro del ruolo del server. Per istruzioni, vedere [Concedere le autorizzazioni per il database &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/grant-database-permissions-analysis-services.md) o [Concedere i diritti di amministratore del server a un'istanza di Analysis Services](../../analysis-services/instances/grant-server-admin-rights-to-an-analysis-services-instance.md).  
  
## <a name="command-syntax"></a>Sintassi del comando 
 I livelli di compatibilità superiore e i database tabulari a 1200 usano metadati tabulari per le definizioni degli oggetti. L'esempio seguente illustra la sintassi completa di DBCC per un database tabulare creato a un livello funzionale di SQL Server 2016.  
  
 Le principali differenze tra le due sintassi includono uno spazio dei nomi XMLA più recente, non \<oggetto > elemento e nessun \<modello > elemento (ne è ancora disponibile un solo modello per ogni database).  
  
```  
<DBCC xmlns="http://schemas.microsoft.com/analysisservices/2014/engine">  
     <DatabaseID>MyTabular1200DB_7811b5d8-c407-4203-8793-12e16c3d1b9b</DatabaseID>  
     <TableName>FactSales</TableName>  
     <PartitionName>FactSales 4</PartitionName>  
</DBCC>  
```  
  
 Per controllare l'intero schema, è possibile omettere gli oggetti di livello inferiore, ad esempio nomi di tabella o partizione.  
  
 È possibile ottenere i nomi degli oggetti e DatabaseID da Management Studio tramite la pagina delle proprietà di ogni oggetto.  
  
## <a name="command-syntax-for-multidimensional-and-tabular-110x-databases"></a>Sintassi del comando per database multidimensionali e tabulari 110x  
 DBCC usa la stessa sintassi sia per i database multidimensionali che per quelli tabulari 1100 e 1103. È possibile eseguire DBCC su oggetti di database specifici, incluso l'intero database. Per altre informazioni sulla definizione di oggetti, vedere [Elemento Object &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla).  
  
```  
<DBCC xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
     <Object>  
          <DatabaseID>AdventureWorksDW2014Multidimensional-EE</DatabaseID>  
          <CubeID>Adventure Works</CubeID>  
          <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
          <PartitionID>Internet_Sales_2006</PartitionID>  
     </Object>  
</DBCC>  
  
```  
  
 Per eseguire DBCC su oggetti superiori nella catena di oggetti, eliminare tutti gli elementi ID oggetto di livello inferiore che non è necessario:  
  
```  
<DBCC xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
     <Object>  
          <DatabaseID>AdventureWorksDW2014Multidimensional-EE</DatabaseID>  
          <CubeID>Adventure Works</CubeID>  
     </Object>  
</DBCC>  
  
```  
  
 Per i database tabulari 110x la sintassi di definizione degli oggetti viene modellata in base alla sintassi del comando Process, in particolare in base al modo in cui viene eseguito il mapping delle tabelle alle dimensioni e ai gruppi di misure.  
  
-   Per**CubeID** viene eseguito il mapping all'ID modello, ovvero **Model**.  
  
-   Per**MeasureGroupID** viene eseguito il mapping a un ID tabella.  
  
-   Per**PartitionID** viene eseguito il mapping a un ID partizione.  
  
## <a name="usage"></a>Uso  
 In SQL Server Management Studio è possibile richiamare DBCC tramite una finestra di query MDX o XMLA. Per visualizzare l'output di DBCC, è anche possibile usare [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Profiler o xEvent di Analysis Services. Si noti che i messaggi di DBCC SSAS non vengono segnalati nel registro eventi applicazioni di Windows o nel file msmdsrv.log.  
  
 DBCC verifica l'eventuale danneggiamento dei dati fisici, nonché il danneggiamento dei dati logici che si verificano quando un segmento include membri orfani. Prima di poter eseguire DBCC, il database deve essere elaborato, perché le partizioni remote, vuote o non elaborate vengono ignorate.  
  
 Il comando viene eseguito in una transazione di lettura e può quindi essere interrotto da timeout con commit forzato. Le verifiche delle partizioni vengono eseguite in parallelo.  
  
 Per rilevare gli eventuali errori di danneggiamento che si sono verificati dopo l'ultimo riavvio del servizio, potrebbe essere necessario un nuovo riavvio. La riconnessione al server non è sufficiente per rendere effettive le modifiche.  
  
### <a name="run-dbcc-commands-in-management-studio"></a>Eseguire i comandi DBCC in Management Studio  
 Per le query ad hoc, aprire una finestra di query MDX o XMLA in SQL Server Management Studio. A questo scopo, fare clic con il pulsante destro del mouse sul database | **Nuova query** | **XMLA**) per eseguire il comando e leggere l'output.  
  
 ![Comando DBCC XML in Management Studio](../../analysis-services/instances/media/ssas-dbcc-ssms.gif "comando XML di DBCC in Management Studio")  
  
 Se non sono stati rilevati problemi, la scheda Risultati visualizza un set di risultati vuoto, come illustrato nella schermata.  
  
 La scheda Messaggi fornisce informazioni dettagliate, ma non è sempre affidabile per i database più piccoli. I messaggi di stato vengono a volte rimossi, a indicare che il comando è stato completato, ma senza messaggi di verifica dello stato per ogni oggetto. Un tipico report del messaggio può essere simile al seguente.  
  
 **Messaggi segnalati da DBCC per il controllo di convalida del cubo**  
  
```  
Executing the query ...  
READS, 0  
READ_KB, 0  
WRITES, 0  
WRITE_KB, 0  
CPU_TIME_MS, 0  
ROWS_SCANNED, 0  
ROWS_RETURNED, 0  
  
<DBCC xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
<Object>  
<DatabaseID>AdventureWorksDW2014Multidimensional-EE</DatabaseID>  
<CubeID>Adventure Works</CubeID>  
</Object>  
</DBCC>  
Started checking segment indexes for the 'Internet_Sales_2011' partition.  
Started checking segment indexes for the 'Internet_Sales_2012' partition.  
Finished checking segment indexes for the 'Internet_Sales_2011' partition.  
Started checking segment indexes for the 'Internet_Sales_2013' partition.  
Finished checking segment indexes for the 'Internet_Sales_2012' partition.  
Started checking segment indexes for the 'Internet_Sales_2014' partition.  
Started checking segment indexes for the 'Internet_Orders_2011' partition.  
Finished checking segment indexes for the 'Internet_Sales_2014' partition.  
Started checking segment indexes for the 'Internet_Orders_2012' partition.  
Started checking segment indexes for the 'Internet_Orders_2013' partition.  
Finished checking segment indexes for the 'Internet_Orders_2012' partition.  
...   
Run complete  
  
```  
  
 **Output generato dall'esecuzione di DBCC in una versione precedente di Analysis Services**  
  
 DBCC è supportato solo su database eseguiti in un'istanza di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] . L'esecuzione del comando in sistemi precedenti restituirà questo errore.  
  
```  
Executing the query ...  
The DBCC element at line 7, column 87 (namespace http://schemas.microsoft.com/analysisservices/2003/engine) cannot appear under Envelope/Body/Execute/Command.  
Execution complete  
  
```  
  
### <a name="trace-dbcc-output-in-sql-server-profiler-2016"></a>Traccia dell'output di DBCC in SQL Server Profiler 2016  
 È possibile visualizzare l'output di DBCC in una traccia di Profiler che include gli eventi Progress Report, ovvero Progress Report Begin, Progress Report Current, Progress Report End e Progress Report Error.  
  
1.  Avviare una traccia. Per informazioni su come usare SQL Server Profiler con Analysis Services, vedere [Use SQL Server Profiler to Monitor Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md) .  
  
2.  Scegliere **Command Begin** e **Command End** più alcuni o tutti gli eventi **Progress Report** .  
  
3.  Eseguire il comando DBCC in Management Studio in una finestra di query XMLA o MDX usando la sintassi fornita nella sezione precedente.  
  
4.  In SQL Server Profiler l'attività di DBCC è indicata tramite gli eventi **Command** che hanno una sottoclasse di evento DBCC:  
  
     ![ssas-dbcc-profiler-eventsubclass](../../analysis-services/instances/media/ssas-dbcc-profiler-eventsubclass.PNG "ssas-dbcc-profiler-eventsubclass")  
  
     Il codice evento 32 indica l'esecuzione di DBCC.  
  
     Il codice evento 64 è un report di stato di DBCC per singoli oggetti.  
  
     Il codice evento 63 indica un controllo di segmento per gli oggetti multidimensionali.  
  
     Per entrambe le sottoclassi di evento esaminare i valori **TextData** per i messaggi restituiti da DBCC.  
  
     I messaggi di stato iniziano con "verifica della coerenza della \<oggetto >", "avviata verifica \<oggetto >", o "terminato il controllo \<oggetto >".  
  
    > [!NOTE]  
    >  Nella versione CTP 3.0 gli oggetti vengono identificati da nomi interni. Ad esempio, una gerarchia di categorie è articolata come H$ Categories -\<IDOggetto >. In una futura versione di CTP i nomi interni verranno sostituiti da nomi descrittivi.  
  
     I messaggi di errore sono elencati di seguito.  
  
### <a name="trace-dbcc-output-in-an-xevent-session-in-ssms"></a>Tracciare l'output di DBCC in una sessione xEvent in SSMS  
 Le sessioni di eventi estesi possono usare sia eventi del profiler che XEvent. Vedere la sezione precedente per istruzioni sull'aggiunta degli eventi **Command** e **Progress Report** .  
  
1.  Avviare una sessione facendo clic con il pulsante destro del mouse su un database > **Gestione** >**Eventi estesi** >   **Sessioni** > **Nuova sessione**. Per altre informazioni, vedere  [Monitor Analysis Services with SQL Server Extended Events](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md) .  
  
2.  Scegliere uno o tutti gli eventi **Progress Report** per la categoria di eventi del profiler o eventi **RequestProgress** per la categoria PureXevent.  
  
3.  Eseguire il comando DBCC in Management Studio in una finestra di query XMLA o MDX usando la sintassi fornita nella sezione precedente.  
  
4.  In SSMS aggiornare la cartella Sessioni. Fare clic con il pulsante destro del mouse sul nome della sessione > **Controlla dati dinamici**.  
  
5.  Esaminare i valori TextData per i messaggi restituiti da DBCC.  TextData è una proprietà di un campo evento e mostra i messaggi di errore e di stato restituiti dall'evento.  
  
     I messaggi di stato iniziano con "verifica della coerenza della \<oggetto >", "avviata verifica \<oggetto >", o "terminato il controllo \<oggetto >".  
  
     I messaggi di errore sono elencati di seguito.  
  
## <a name="reference-consistency-checks-and-errors-for-multidimensional-databases"></a>Informazioni di riferimento: Verifiche di coerenza ed errori per i database multidimensionali  
 Per i database multidimensionali vengono convalidati solo gli indici partizione.  Durante l'esecuzione DBCC crea un indice temporaneo per ogni partizione e lo confronta con l'indice persistente su disco.  La creazione di un indice temporaneo richiede la lettura di tutti i dati dalle partizioni su disco e quindi il mantenimento dell'indice temporaneo in memoria per il confronto. Dato il carico di lavoro aggiuntivo, nel server potrebbe verificarsi una quantità di I/O su disco e un consumo di memoria significativi durante un'esecuzione di DBCC.  
  
 Il rilevamento del danneggiamento dell'indice multidimensionale include i controlli seguenti. Gli errori in questa tabella sono visualizzati nelle tracce xEvent o di Profiler per gli errori a livello di oggetto.  
  
||||  
|-|-|-|  
|**Oggetto**|**Descrizione del controllo DBCC**|**Errore di operazione non riuscita**|  
|Indice partizione|Controlla gli indici e le statistiche dei segmenti.<br /><br /> Confronta l'ID di ogni membro nell'indice partizione temporaneo con le statistiche della partizione archiviate su disco.  Se nell'indice temporaneo viene trovato un membro con un valore dell'ID dati non compreso nell'intervallo archiviato per le statistiche dell'indice partizione sul disco, le statistiche per l'indice vengono considerate danneggiate.|Le statistiche dei segmenti della partizione sono danneggiate.|  
|Indice partizione|Convalida i metadati.<br /><br /> Verifica che ogni membro nell'indice temporaneo possa essere trovato nel file di intestazione dell'indice per il segmento su disco.|Il segmento della partizione è danneggiato.|  
|Indice partizione|Analizza i segmenti per cercare eventuali danneggiamenti fisici.<br /><br /> Legge il file di indice su disco per ogni membro nell'indice temporaneo e verifica che le dimensioni dei record di indice corrispondano e che le stesse pagine di dati siano contrassegnate come pagine contenenti record per il membro corrente.|Il segmento della partizione è danneggiato.|  
  
## <a name="reference-consistency-checks-and-errors-for-tabular-databases"></a>Informazioni di riferimento: Verifiche di coerenza ed errori per i database tabulari  
 La tabella seguente contiene l'elenco di tutte le verifiche di coerenza eseguite sugli oggetti tabulari, insieme agli errori generati se la verifica indica un danneggiamento. Gli errori in questa tabella sono visualizzati nelle tracce xEvent o di Profiler per gli errori a livello di oggetto.  
  
||||  
|-|-|-|  
|**Oggetto**|**Descrizione del controllo DBCC**|**Errore di operazione non riuscita**|  
|Database|Controlla il numero di tabelle nel database.  Un valore minore di zero indica un danneggiamento.|È stato rilevato un danneggiamento nel livello di archiviazione: la raccolta di tabelle nel database '%{parent/}' è danneggiata.|  
|Database|Controlla la struttura interna usata per rilevare l'integrità referenziale e genera un errore se le dimensioni non sono corrette.|Verifiche di coerenza non superate dai file di database.|  
|Tabella|Controlla il valore interno usato per determinare se si tratta di una tabella delle dimensioni o dei fatti.  Un valore che non rientra nell'intervallo noto indica un danneggiamento.|Le verifiche di coerenza del database (DBCC) non sono riuscite durante il controllo delle statistiche della tabella.|  
|Tabella|Controlla che il numero di partizioni nella mappa di segmenti per la tabella corrisponda al numero di partizioni definito per la tabella.|È stato rilevato un danneggiamento nel livello di archiviazione: la raccolta di partizioni nella tabella '%{parent/}' è danneggiata.|  
|Tabella|Se un database tabulare è stato creato o importato da PowerPivot per Excel 2010 e include un numero di partizioni maggiore di uno, verrà generato un errore, perché il supporto delle partizioni è stato aggiunto in versioni successive e ciò indica un danneggiamento.|Le verifiche di coerenza del database (DBCC) non sono riuscite durante il controllo della mappa di segmenti.|  
|Partition|Verifica che per ogni partizione il numero di segmenti di dati e il numero di record per ogni segmento di dati nel segmento corrisponda ai valori archiviati nell'indice per il segmento.|Le verifiche di coerenza del database (DBCC) non sono riuscite durante il controllo della mappa di segmenti.|  
|Partition|Genera un errore se il numero totale di record, segmenti o record per ogni segmento non è valido (minore di zero) o il numero di segmenti non corrisponde al numero di segmenti necessari calcolato in base al numero totale di record.|Le verifiche di coerenza del database (DBCC) non sono riuscite durante il controllo della mappa di segmenti.|  
|Relazione|Genera un errore se la struttura usata per archiviare i dati relativi alla relazione non contiene record o se il nome della tabella usata nella relazione è vuoto.|Le verifiche di coerenza del database (DBCC) non sono riuscite durante il controllo delle relazioni.|  
|Relazione|Verifica che i nomi della tabella primaria, della colonna primaria, della tabella della chiave esterna e della colonna esterna siano impostati e che le colonne e le tabelle coinvolte nella relazione siano accessibili.<br /><br /> Verifica che i tipi di colonne coinvolti siano validi e che i valori di chiave esterna-chiave primaria dell'indice generino una struttura di ricerca valida.|Le verifiche di coerenza del database (DBCC) non sono riuscite durante il controllo delle relazioni.|  
|Gerarchia|Genera un errore se l'ordinamento per la gerarchia non è un valore riconosciuto.|Le verifiche di coerenza del database (DBCC) non sono riuscite durante il controllo della gerarchia '%{hier/}'.|  
|Gerarchia|I controlli eseguiti sulla gerarchia dipendono dal tipo interno dello schema di mapping della gerarchia usato.<br /><br /> Tutte le gerarchie vengono controllate per verificare che lo stato di elaborazione sia corretto, che l'archivio della gerarchia sia presente e che, ove applicabile, le strutture dei dati usate per una conversione da ID dati a posizione della gerarchia siano disponibili.<br /><br /> Presupponendo che vengano superati tutti questi controlli, la struttura della gerarchia viene esaminata per verificare che ogni posizione nella gerarchia punti al membro corretto.<br />Se uno di questi test non riesce, viene generato un errore.|Le verifiche di coerenza del database (DBCC) non sono riuscite durante il controllo della gerarchia '%{hier/}'.|  
|Gerarchia definita dall'utente|Controlla se i nomi dei livelli della gerarchia sono impostati.<br /><br /> Se la gerarchia è stata elaborata, verifica che il formato dell'archivio dati di gerarchia interno sia corretto.  Verifica che l'archivio di gerarchia interno non contenga valori di dati non validi.<br /><br /> Se la gerarchia è contrassegnata come non elaborata, verifica che questo stato si applichi alle strutture dei dati precedenti e che tutti i livelli della gerarchia siano contrassegnati come vuoti.|Le verifiche di coerenza del database (DBCC) non sono riuscite durante il controllo della gerarchia '%{hier/}'.|  
|colonna|Genera un errore se la codifica usata per la colonna non è impostata su un valore noto.|Le verifiche di coerenza del database (DBCC) non sono riuscite durante il controllo delle statistiche della colonna.|  
|colonna|Controlla se la colonna è stata o meno compressa dal motore in memoria.|Le verifiche di coerenza del database (DBCC) non sono riuscite durante il controllo delle statistiche della colonna.|  
|colonna|Controlla se per il tipo di compressione nella colonna sono presenti valori noti.|Le verifiche di coerenza del database (DBCC) non sono riuscite durante il controllo delle statistiche della colonna.|  
|colonna|Quando la colonna "tokenizzazione" non è impostata su un valore noto, genera un errore.|Le verifiche di coerenza del database (DBCC) non sono riuscite durante il controllo delle statistiche della colonna.|  
|colonna|Se l'intervallo di ID archiviato per un dizionario dei dati delle colonne non corrisponde al numero di valori nel dizionario dei dati o non è compreso nell'intervallo consentito, genera un errore.|Le verifiche di coerenza del database (DBCC) non sono riuscite durante il controllo del dizionario dei dati.|  
|colonna|Controlla che il numero di segmenti di dati per una colonna corrisponda al numero di segmenti di dati per la tabella a cui appartiene.|È stato rilevato un danneggiamento nel livello di archiviazione: la raccolta di segmenti nella colonna '%{parent/}' è danneggiata.|  
|colonna|Controlla che il numero di partizioni nella colonna dati corrisponda al numero di partizioni della mappa di segmenti di dati per la colonna.|Le verifiche di coerenza del database (DBCC) non sono riuscite durante il controllo della mappa di segmenti.|  
|colonna|Verifica che il numero di record in un segmento di colonna corrisponda al conteggio di record archiviato nell'indice per tale segmento di colonna.|È stato rilevato un danneggiamento nel livello di archiviazione: la raccolta di segmenti nella colonna '%{parent/}' è danneggiata.|  
|colonna|Se per una colonna non sono presenti statistiche dei segmenti, genera un errore.|Le verifiche di coerenza del database (DBCC) non sono riuscite durante il controllo delle statistiche del segmento.|  
|colonna|Se una colonna non contiene informazioni sulla compressione o l'archiviazione di segmenti, genera un errore.|Verifiche di coerenza non superate dai file di database.|  
|colonna|Segnala un errore se le statistiche dei segmenti per una colonna non corrispondono ai valori di colonna effettivi per ID dati minimo, ID dati massimo, Numero di valori Distinct, Numero di righe o presenza di valori NULL.|Le verifiche di coerenza del database (DBCC) non sono riuscite durante il controllo delle statistiche del segmento.|  
|Segmento di colonna|Se ID dati minimo o ID dati massimo è minore del valore di sistema riservato per i valori NULL, contrassegna le informazioni sul segmento di colonna come danneggiate.|Le verifiche di coerenza del database (DBCC) non sono riuscite durante il controllo delle statistiche del segmento.|  
|Segmento di colonna|Se non sono presenti righe per questo segmento, i valori di dati minimo e massimo per la colonna devono essere impostati sul valore di sistema riservato per NULL.  Se il valore non è Null, genera un errore.|Le verifiche di coerenza del database (DBCC) non sono riuscite durante il controllo delle statistiche del segmento.|  
|Segmento di colonna|Se la colonna include righe e almeno un valore diverso da Null, verifica che l'ID dati minimo e massimo per la colonna sia maggiore del valore di sistema riservato per NULL.|Le verifiche di coerenza del database (DBCC) non sono riuscite durante il controllo delle statistiche del segmento.|  
|Interno|Verifica che sia impostato l'hint di tokenizzazione dell'archivio e che, se l'archivio viene elaborato, siano presenti puntatori validi per le tabelle interne.  Se l'archivio non viene elaborato, verifica che tutti i puntatori siano Null.<br />In caso contrario, restituisce un errore DBCC generico.|Verifiche di coerenza non superate dai file di database.|  
|Database DBCC|Genera un errore se lo schema del database non contiene tabelle o una o più tabelle non sono accessibili.|È stato rilevato un danneggiamento nel livello di archiviazione: la raccolta di tabelle nel database '%{parent/}' è danneggiata.|  
|Database DBCC|Genera un errore se una tabella è contrassegnata come temporanea o è di un tipo sconosciuto.|È stato rilevato un tipo di tabella non valido.|  
|Database DBCC|Genera un errore se il numero di relazioni per una tabella ha un valore negativo o se una tabella qualsiasi ha una relazione definita e non viene trovata una struttura di relazioni corrispondente.|È stato rilevato un danneggiamento nel livello di archiviazione: la raccolta di relazioni nella tabella '%{parent/}' è danneggiata.|  
|Database DBCC|Se il livello di compatibilità per il database è 1050 (SQL Server 2008 R2/PowerPivot v 1.0) e il numero di relazioni supera il numero di tabelle nel modello, contrassegna il database come danneggiato.|Verifiche di coerenza non superate dai file di database.|  
|Tabella DBCC|Per la tabella in fase di convalida, controlla se il numero di colonne è minore di zero e genera un errore se il valore è true.  Si verifica un errore anche se l'archivio colonne per una colonna nella tabella è NULL.|È stato rilevato un danneggiamento nel livello di archiviazione: la raccolta di colonne nella tabella '%{parent/}' è danneggiata.|  
|Partizione DBCC|Controlla la tabella a cui appartiene la partizione in fase di convalida e, se il numero di colonne per la tabella è minore di zero, significa che la raccolta Colonne della tabella è danneggiata. Si verifica un errore anche se l'archivio colonne per una colonna della tabella è NULL.|È stato rilevato un danneggiamento nel livello di archiviazione: la raccolta di colonne nella tabella '%{parent/}' è danneggiata.|  
|Partizione DBCC|Esegue il ciclo di ogni colonna della partizione selezionata e verifica che ogni segmento della partizione abbia un collegamento valido a una struttura di segmenti di colonna.  Se un segmento qualsiasi include un collegamento NULL, la partizione viene considerata danneggiata.|È stato rilevato un danneggiamento nel livello di archiviazione: la raccolta di segmenti nella colonna '%{parent/}' è danneggiata.|  
|colonna|Restituisce un errore se il tipo di colonna non è valido.|È stato rilevato un tipo di segmento non valido.|  
|colonna|Restituisce un errore se il conteggio del numero di segmenti in una colonna qualsiasi è negativo o se il puntatore alla struttura di segmenti di colonna per un segmento ha un collegamento NULL.|È stato rilevato un danneggiamento nel livello di archiviazione: la raccolta di segmenti nella colonna '%{parent/}' è danneggiata.|  
|Comando DBCC|Il comando DBCC segnala più messaggi di stato durante l'esecuzione dell'operazione DBCC.  Visualizza un messaggio di stato che include il nome del database, della tabella o della colonna dell'oggetto prima dell'avvio e un altro messaggio al termine del controllo di ogni oggetto.|Verifica della coerenza del \<objectname > \<objecttype >. Fase: verifica preliminare.<br /><br /> Verifica della coerenza del \<objectname > \<objecttype >. Fase: verifica finale.|  
  
## <a name="common-resolutions-for-error-conditions"></a>Risoluzioni comuni per le condizioni di errore  
 Gli errori seguenti vengono visualizzati in SQL Server Management Studio o nei file msmdsrv.log. Questi errori vengono visualizzati quando uno o più controlli non riescono. A seconda dell'errore, la soluzione consigliata consiste nel rielaborare un oggetto, eliminare e ridistribuire una soluzione o ripristinare il database.  
  
|Errore|Problema|Soluzione|  
|-----------|-----------|----------------|  
|**Errori nella gestione metadati**<br /><br /> Il riferimento all'oggetto '\<objectID >' non è valido. Non corrisponde alla struttura della gerarchia di classi dei metadati.|Comando non valido|Verificare la sintassi del comando. È probabile che sia stato incluso un oggetto di livello inferiore senza specificare uno o più dei relativi oggetti padre.|  
|**Errori nella gestione metadati**<br /><br /> Entrambi il \<oggetto > con l'ID di '\<objectID >' non esiste nel \<parentobject > con l'ID di '\<ID oggetto padre >', oppure l'utente non dispone delle autorizzazioni per accedere all'oggetto.|Danneggiamento dell'indice (multidimensionale)|Rielaborare l'oggetto e tutti gli eventuali oggetti dipendenti.|  
|**Errore durante la verifica di coerenza della partizione**<br /><br /> Si è verificato un errore durante la verifica della coerenza del \<-nome della partizione > partizione del \<misure-group-name > gruppo di misure per il \<nome-cubo > del cubo dal \<-nome del database > database. È possibile correggere l'errore elaborando di nuovo la partizione o gli indici.|Danneggiamento dell'indice (multidimensionale)|Rielaborare l'oggetto e tutti gli eventuali oggetti dipendenti.|  
|**Le statistiche dei segmenti della partizione sono danneggiate**|Danneggiamento dell'indice (multidimensionale)|Rielaborare l'oggetto e tutti gli eventuali oggetti dipendenti.|  
|**Il segmento della partizione è danneggiato**|Danneggiamento dei metadati (multidimensionali o tabulari)|Eliminare e ridistribuire il progetto o ripristinarlo da un backup e rielaborarlo.<br /><br /> Per istruzioni, vedere il blog [How to Deal with Corruption in Analysis Services](http://blogs.msdn.com/b/karang/archive/2010/08/11/how-to-deal-with-corruption-in-analysis-services.aspx) (Gestione dei danneggiamenti in Analysis Services).|  
|**Danneggiamento di metadati della tabella**<br /><br /> Tabella \<nome-tabella > file di metadati è danneggiato. Non è possibile trovare la tabella principale nel nodo DataFileList.|Danneggiamento dei metadati (solo tabulari)|Eliminare e ridistribuire il progetto o ripristinarlo da un backup e rielaborarlo.<br /><br /> Per istruzioni, vedere il blog [How to Deal with Corruption in Analysis Services](http://blogs.msdn.com/b/karang/archive/2010/08/11/how-to-deal-with-corruption-in-analysis-services.aspx) (Gestione dei danneggiamenti in Analysis Services).|  
|**Danneggiamento nel livello di archiviazione**<br /><br /> Danneggiamento nel livello di archiviazione: raccolta di \<-nome del tipo > in \<nome-padre > \<tipo-padre > è danneggiato.|Danneggiamento dei metadati (solo tabulari)|Eliminare e ridistribuire il progetto o ripristinarlo da un backup e rielaborarlo.<br /><br /> Per istruzioni, vedere il blog [How to Deal with Corruption in Analysis Services](http://blogs.msdn.com/b/karang/archive/2010/08/11/how-to-deal-with-corruption-in-analysis-services.aspx) (Gestione dei danneggiamenti in Analysis Services).|  
|**Tabella di sistema mancante**<br /><br /> Tabella di sistema \<nome-tabella > è mancante.|Danneggiamento di oggetti (solo tabulari)|Rielaborare l'oggetto e tutti gli eventuali oggetti dipendenti.|  
|**Le statistiche della tabella sono danneggiate**<br /><br /> Le statistiche della tabella di sistema \<nome-tabella > è mancante.|Danneggiamento dei metadati (solo tabulari)|Eliminare e ridistribuire il progetto o ripristinarlo da un backup e rielaborarlo.<br /><br /> Per istruzioni, vedere il blog [How to Deal with Corruption in Analysis Services](http://blogs.msdn.com/b/karang/archive/2010/08/11/how-to-deal-with-corruption-in-analysis-services.aspx) (Gestione dei danneggiamenti in Analysis Services).|  
  
## <a name="disable-automatic-consistency-checks-on-database-load-operations-through--the-msmdsrvini-configuration-file"></a>Disabilitare le verifiche di coerenza automatiche durante le operazioni di caricamento del database tramite il file di configurazione msmdsrv.ini  
 Anche se non è consigliabile, è possibile disabilitare le verifiche di coerenza del database predefinite eseguite automaticamente in presenza di eventi di caricamento del database (solo nei database tabulari). A questo scopo, è necessario modificare un'impostazione di configurazione nel file msmdsrv.ini:  
  
```  
<ConfigurationSettings>  
     <Vertipaq />  
          <DisableConsistencyChecks />  
```  
  
 Questa impostazione non è presente nel file di configurazione e deve essere aggiunta manualmente.  
  
 I valori validi sono i seguenti:  
  
-   **-2** (impostazione predefinita) DBCC è abilitato. Se il server è riesce a risolvere in modo logico l'errore con un livello di certezza elevato, viene applicata automaticamente una correzione. In caso contrario, verrà registrato un errore.  
  
-   **-1** DBCC è parzialmente abilitato. Viene abilitato per RESTORE e per le convalide pre-commit che controllano lo stato del database alla fine di una transazione.  
  
-   **0** DBCC è parzialmente abilitato. Vengono eseguite verifiche di coerenza del database durante le operazioni RESTORE, IMAGELOAD, LOCALCUBELOAD e  
         ATTACH.  
  
-   **1** DBCC è disabilitato. I controlli di integrità dei dati sono disabilitati, tuttavia continueranno a essere eseguiti i controlli di deserializzazione.  
  
> [!NOTE]  
>  Questa impostazione non ha alcun impatto su DBCC quando si esegue il comando su richiesta.  
  
## <a name="see-also"></a>Vedere anche  
 [Elaborare database, tabelle o partizioni &#40;Analysis Services&#41;](../../analysis-services/tabular-models/process-database-table-or-partition-analysis-services.md)   
 [Elaborazione di un modello multidimensionale &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Livello di compatibilità per i modelli tabulari in Analysis Services](../../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)   
 [proprietà server in Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)  
  
  
