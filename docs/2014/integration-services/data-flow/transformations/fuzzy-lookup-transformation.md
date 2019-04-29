---
title: Trasformazione Ricerca fuzzy | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.fuzzylookuptrans.f1
helpviewer_keywords:
- cleaning data
- comparing data
- token delimiters [Integration Services]
- temporary indexes [Integration Services]
- temporary tables [Integration Services]
- Fuzzy Lookup transformation
- reference tables [Integration Services]
- match similar data [Integration Services]
- replacing missing values
- correcting data [Integration Services]
- cache [Integration Services]
- standardizing data [Integration Services]
- lookups [Integration Services]
- confidence scores [Integration Services]
- fuzzy matches
- missing values replaced [Integration Services]
- similarity thresholds [Integration Services]
ms.assetid: 019db426-3de2-4ca9-8667-79fd9a47a068
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d0b77d45ca55adaa85e4e37e9da817f325ce0fc7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62900317"
---
# <a name="fuzzy-lookup-transformation"></a>Ricerca fuzzy - trasformazione
  La trasformazione Ricerca fuzzy esegue attività di pulitura dei dati, ad esempio standardizzazione, correzione e inserimento di valori mancanti.  
  
> [!NOTE]  
>  Per informazioni dettagliate sulla trasformazione Ricerca fuzzy, inclusi i limiti di memoria e le prestazioni, vedere il white paper [Fuzzy Lookup and Fuzzy Grouping in SQL Server Integration Services 2005](https://go.microsoft.com/fwlink/?LinkId=96604)(Ricerca fuzzy e Raggruppamento fuzzy in SQL Server Integration Services 2005).  
  
 La differenza tra la trasformazione Ricerca fuzzy e la trasformazione Ricerca è l'utilizzo della corrispondenza fuzzy. La trasformazione Ricerca individua i record corrispondenti nella tabella di riferimento tramite un equijoin Restituisce record con almeno un record corrispondente e record senza alcuna corrispondenza. La trasformazione Ricerca fuzzy invece restituisce anche corrispondenze fuzzy.  
  
 La trasformazione Ricerca fuzzy viene spesso eseguita dopo la trasformazione Ricerca nel flusso di dati di un pacchetto. La trasformazione Ricerca individua innanzitutto eventuali corrispondenze esatte. Se non esiste alcuna corrispondenza esatta, la trasformazione Ricerca fuzzy individua le corrispondenze fuzzy nella tabella di riferimento.  
  
 È necessario che la trasformazione possa accedere a un'origine dei dati di riferimento contenente i valori utilizzati per la pulitura e l'estensione dei dati di input. Tale origine deve essere una tabella di un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . La corrispondenza tra il valore di una colonna di input e il valore della tabella di riferimento può essere una corrispondenza esatta o fuzzy. La trasformazione richiede tuttavia che almeno una corrispondenza di colonna sia configurata per la corrispondenza fuzzy. Se si desidera individuare solo corrispondenze esatte, utilizzare la trasformazione Ricerca.  
  
 Questa trasformazione include un input e un output.  
  
 Nella corrispondenza fuzzy è possibile utilizzare solo colonne di input con tipi di dati `DT_WSTR` e `DT_STR`. Per la corrispondenza esatta è possibile utilizzare qualsiasi tipo di dati DTS ad eccezione di `DT_TEXT`, `DT_NTEXT` e `DT_IMAGE`. Per altre informazioni, vedere [Tipi di dati di Integration Services](../integration-services-data-types.md). I tipi di dati delle colonne che partecipano al join tra l'input e la tabella di riferimento devono essere compatibili. È ad esempio corretto unire in join una colonna con tipo di dati DTS `DT_WSTR` e una colonna con tipo di dati di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] `nvarchar`, ma non una colonna con tipo di dati `DT_WSTR` e una colonna con tipo di dati `int`.  
  
 È possibile personalizzare questa trasformazione specificando la quantità di memoria massima, l'algoritmo di confronto tra righe, nonché la memorizzazione nella cache delle tabelle di riferimento e degli indici utilizzati dalla trasformazione.  
  
 La quantità di memoria usata dalla trasformazione Ricerca fuzzy può essere configurata impostando la proprietà personalizzata MaxMemoryUsage. È possibile specificare il numero di megabyte (MB) oppure il valore 0, che consente alla trasformazione di utilizzare una quantità dinamica di memoria, a seconda delle esigenze e della quantità di memoria fisica disponibile. La proprietà personalizzata MaxMemoryUsage può essere aggiornata da un'espressione di proprietà al caricamento del pacchetto. Per altre informazioni, vedere [Espressioni di Integration Services &#40;SSIS&#41;](../../expressions/integration-services-ssis-expressions.md), [Utilizzo delle espressioni di proprietà nei pacchetti](../../expressions/use-property-expressions-in-packages.md) e [Proprietà personalizzate delle trasformazioni](transformation-custom-properties.md).  
  
## <a name="controlling-fuzzy-matching-behavior"></a>Controllo del funzionamento della corrispondenza fuzzy  
 La trasformazione Ricerca fuzzy include tre caratteristiche per la personalizzazione del tipo di ricerca eseguito, ovvero numero massimo di corrispondenze da restituire per ogni riga di input, delimitatori token e soglie di somiglianza.  
  
 La trasformazione restituisce zero o più corrispondenze fino al numero massimo specificato. L'impostazione di un numero massimo di corrispondenze non garantisce la restituzione di tale numero di corrispondenze. Viene semplicemente limitato il numero di corrispondenze da restituire. Se come numero massimo di corrispondenze si imposta un valore maggiore di 1, l'output della trasformazione potrebbe includere più di una riga per ogni ricerca e alcune righe potrebbero essere duplicate.  
  
 La trasformazione utilizza un numero di delimitatori predefinito per la suddivisione in token dei dati. È tuttavia possibile aggiungere delimitatori in base alle specifiche esigenze. Il numero di delimitatori predefinito è specificato nella proprietà Delimitatori. La suddivisione in token è un'operazione importante in quanto definisce le unità all'interno dei dati che vengono confrontate tra di loro.  
  
 Le soglie di somiglianza possono essere impostate a livello di componente e di join. La soglia di somiglianza a livello di join è disponibile solo quando la trasformazione esegue una corrispondenza fuzzy tra le colonne dell'input e quelle della tabella di riferimento. L'intervallo di somiglianza è compreso tra 0 e 1. Più la soglia è vicina a 1 e più simili devono essere le righe e le colonne per essere qualificate come duplicati. Per impostare la soglia di somiglianza, è necessario impostare la proprietà MinSimilarity a livello di componente e di join. Per soddisfare la soglia di somiglianza specificata a livello di componente, è necessario che la somiglianza di tutte le righe in tutte le corrispondenze sia maggiore o uguale alla soglia di somiglianza specificata a livello di componente. Ciò significa che è possibile specificare una corrispondenza elevata a livello di componente solo se anche le corrispondenze a livello di riga o di join sono elevate.  
  
 Ogni corrispondenza include un punteggio di somiglianza e un punteggio di confidenza. Il punteggio di somiglianza è una misura matematica della somiglianza testuale tra il record di input e il record della tabella di riferimento restituito dalla trasformazione Ricerca fuzzy. Il punteggio di confidenza indica la probabilità con cui un valore specifico risulta essere la corrispondenza migliore tra le corrispondenze individuate nella tabella di riferimento. Il punteggio di confidenza assegnato a un record dipende dagli altri record corrispondenti restituiti. Ad esempio, la corrispondenza tra *Sig.* e *Signor* restituisce un punteggio di somiglianza basso indipendentemente dalle altre corrispondenze. Se *Signor* è l'unica corrispondenza restituita, il punteggio di confidenza è alto. Se la tabella di riferimento include sia *Signor* che *Sig.* , per *Sig.* la confidenza risulta elevata, mentre per *Signor* risulta bassa. A una somiglianza elevata tuttavia non corrisponde necessariamente una confidenza elevata. Se, ad esempio, si esegue la ricerca del valore *Capitolo 4*, i risultati *Capitolo 1*, *Capitolo 2*e *Capitolo 3* avranno un punteggio di somiglianza elevato, ma un punteggio di confidenza basso in quanto non è chiaro quale dei risultati sia la corrispondenza migliore.  
  
 Il punteggio di somiglianza è rappresentato da un valore decimale compreso tra 0 e 1, dove 1 indica una corrispondenza esatta tra il valore della colonna di input e il valore della tabella di riferimento. Il punteggio di confidenza, rappresentato da un valore decimale compreso tra 0 e 1, indica la confidenza della corrispondenza. Se non viene individuata alcuna corrispondenza utilizzabile, alla riga viene assegnato un punteggio di somiglianza e di confidenza pari a 0 e le colonne di output copiate dalla tabella di riferimento includeranno valori Null.  
  
 In alcuni casi la ricerca fuzzy non restituisce corrispondenze appropriate nella tabella di riferimento. Ciò si verifica se il valore di input utilizzato per la ricerca è una singola parola breve. Ad esempio, *teto* non viene restituito come corrispondenza del valore *tetto* in una tabella di riferimento che non include altri token nelle colonne della riga.  
  
 Le colonne di output della trasformazione corrispondono alle colonne di input contrassegnate come colonne pass-through, alle colonne selezionate nella tabelle di ricerca e alle colonne seguenti:  
  
-   **_Similarity**, colonna che descrive la somiglianza tra i valori delle colonne di input e di riferimento.  
  
-   **_Confidence**, colonna che descrive la probabilità della corrispondenza.  
  
 Sfruttando la connessione al database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , la trasformazione crea le tabelle temporanee utilizzate dall'algoritmo per individuare le corrispondenze fuzzy.  
  
## <a name="running-the-fuzzy-lookup-transformation"></a>Esecuzione della trasformazione Ricerca fuzzy  
 All'avvio della trasformazione nel pacchetto, viene innanzitutto copiata la tabella di riferimento, viene aggiunta una chiave con tipo di dati integer nella nuova tabella e viene compilato un indice nella colonna chiave. Quindi, nella copia della tabella di riferimento, viene compilato un indice, denominato indice delle corrispondenze. In questo indice vengono archiviati i risultati della suddivisione in token dei valori delle colonne di input della trasformazione. I token vengono quindi utilizzati dalla trasformazione durante l'operazione di ricerca. L'indice delle corrispondenze è una tabella di un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Alla successiva esecuzione del pacchetto, la trasformazione utilizza un indice delle corrispondenze esistente oppure ne crea uno nuovo. Se la tabella di riferimento è statica, il pacchetto può evitare la ricompilazione dell'indice per le sessioni di pulitura dei dati successive, operazione potenzialmente costosa in termini di risorse. Se si sceglie di utilizzare un indice esistente, l'indice viene creato alla prima esecuzione del pacchetto. Se si eseguono più trasformazioni Ricerca fuzzy basate sulla stessa tabella di riferimento, viene utilizzato lo stesso indice in tutte le trasformazioni. Per poter riutilizzare l'indice, è necessario che le operazioni di ricerca siano identiche e che nella ricerca vengano utilizzate le stesse colonne. È possibile assegnare un nome all'indice e selezionare la connessione al database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in cui viene salvato l'indice.  
  
 Se la trasformazione salva l'indice delle corrispondenze, l'indice può essere mantenuto in modo automatico. Ciò significa che in corrispondenza di ogni aggiornamento di un record della tabella di riferimento viene aggiornato anche l'indice delle corrispondenze. La manutenzione dell'indice delle corrispondenze consente di ridurre i tempi di elaborazione, in quanto non è necessario ricompilare l'indice quando il pacchetto viene eseguito. È possibile impostare la modalità con cui la trasformazione gestisce l'indice delle corrispondenze.  
  
 Nella tabella seguente vengono descritte le opzioni per l'indice delle corrispondenze.  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|**GenerateAndMaintainNewIndex**|Crea un nuovo indice, lo salva e ne esegue la manutenzione. Nella tabella di riferimento la trasformazione installa trigger per la sincronizzazione tra la tabella di riferimento e la tabella dell'indice.|  
|**GenerateAndPersistNewIndex**|Crea un nuovo indice e lo salva, ma non ne esegue la manutenzione.|  
|**GenerateNewIndex**|Crea un nuovo indice, ma non lo salva.|  
|**ReuseExistingIndex**|Riutilizza un indice esistente.|  
  
### <a name="maintenance-of-the-match-index-table"></a>Manutenzione della tabella dell'indice delle corrispondenze  
 L'opzione **GenerateAndMaintainNewIndex** consente di installare i trigger nella tabella di riferimento per mantenere la sincronizzazione tra la tabella dell'indice delle corrispondenze e la tabella di riferimento. Prima di rimuovere il trigger installato, è necessario eseguire la stored procedure **sp_FuzzyLookupTableMaintenanceUnInstall** e specificare come valore del parametro di input il nome riportato nella proprietà MatchIndexName.  
  
 È opportuno inoltre non eliminare la tabella dell'indice delle corrispondenze prima di eseguire la stored procedure **sp_FuzzyLookupTableMaintenanceUnInstall** . Se si esegue questa operazione, i trigger della tabella di riferimento non verranno eseguiti correttamente. I successivi aggiornamenti della tabella di riferimento avranno esito negativo fino a quando i trigger della tabella non vengono eliminati in modo manuale.  
  
 Il comando SQL TRUNCATE TABLE non richiama trigger DELETE. Se si esegue il comando TRUNCATE TABLE sulla tabella di riferimento, la tabella e l'indice delle corrispondenze non saranno più sincronizzati e la trasformazione Ricerca fuzzy avrà esito negativo. Mentre i trigger per la manutenzione della tabella dell'indice delle corrispondenze sono installati nella tabella di riferimento, è necessario eseguire il comando SQL DELETE anziché TRUNCATE TABLE.  
  
> [!NOTE]  
>  Se si seleziona **Manutenzione indice archiviato** nella scheda **Tabella di riferimento** di **Editor trasformazione Ricerca fuzzy**, la trasformazione utilizza stored procedure gestite per gestire l'indice. Queste stored procedure gestite usano la funzionalità di integrazione con Common Language Runtime (CLR) presente in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Per impostazione predefinita, l'integrazione con CLR non è abilitata in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Per utilizzare la funzionalità **Manutenzione indice archiviato** è necessario abilitare l'integrazione con CLR. Per altre informazioni, vedere [Enabling CLR Integration](../../../relational-databases/clr-integration/clr-integration-enabling.md).  
>   
>  Considerato che l'opzione **Manutenzione indice archiviato** richiede l'integrazione con CLR, questa funzionalità può essere usata solo se si seleziona una tabella di riferimento in un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in cui è abilitata l'integrazione con CLR.  
  
## <a name="row-comparison"></a>Confronto tra righe  
 Quando si configura la trasformazione Ricerca fuzzy è possibile specificare l'algoritmo di confronto utilizzato per individuare i record corrispondenti nella tabella di riferimento. Se si imposta la proprietà Exhaustive su `True`, la trasformazione confronta ogni riga dell'input per ogni riga nella tabella di riferimento. Questo algoritmo di confronto restituisce in genere risultati più precisi, ma la trasformazione viene eseguita più lentamente, a meno che la tabella di riferimento non includa un numero di righe ridotto. Se la proprietà Exhaustive è impostata su `True`, l'intera tabella di riferimento viene caricata in memoria. Per evitare problemi di prestazioni, è consigliabile impostare la proprietà Exhaustive su `True` pacchetto solo durante lo sviluppo.  
  
 Se la proprietà Exhaustive è impostata su `False`, la trasformazione Ricerca Fuzzy restituirà solo le corrispondenze che hanno almeno una sottostringa o un token indicizzato (la sottostringa viene chiamata un *q-gramma*) in comune con il record di input. Per ottimizzare l'efficienza delle ricerche, viene indicizzato solo un subset dei token in ogni riga della tabella nella struttura con indice invertito utilizzata dalla trasformazione Ricerca fuzzy per individuare le corrispondenze. Se il set di dati di input è ridotto, è possibile impostare la proprietà Exhaustive su `True` per evitare di ignorare le corrispondenze per cui non esistono token comuni nella tabella dell'indice.  
  
## <a name="caching-of-indexes-and-reference-tables"></a>Memorizzazione nella cache di indici e tabelle di riferimento  
 Quando si configura la trasformazione Ricerca fuzzy, è possibile specificare se l'indice e la tabella di riferimento devono prima essere inseriti parzialmente nella memoria cache. Se si imposta la proprietà WarmCaches su `True`, la tabella dell'indice e di riferimento vengono caricati in memoria. Se l'input include molte righe, l'impostazione della proprietà WarmCaches su `True` può migliorare le prestazioni della trasformazione. Se il numero di righe di input è ridotto, impostare la proprietà WarmCaches su `False` può rendere più veloce il riutilizzo di un indice di grandi dimensioni.  
  
## <a name="temporary-tables-and-indexes"></a>Tabelle e indici temporanei  
 In fase di esecuzione la trasformazione Ricerca fuzzy crea oggetti temporanei, ad esempio tabelle e indici, nel database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a cui la trasformazione si connette. Le dimensioni delle tabelle e degli indici temporanei sono proporzionali al numero di righe e token della tabella di riferimento e al numero di token creati dalla trasformazione Ricerca fuzzy. Questi oggetti temporanei pertanto possono utilizzare potenzialmente una quantità di spazio su disco considerevole. La trasformazione esegue inoltre query sulle tabelle temporanee. È pertanto consigliabile connettere la trasformazione Ricerca fuzzy a un'istanza di un database di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non di produzione, soprattutto se lo spazio su disco disponibile nel server di produzione è ridotto.  
  
 Le prestazioni della trasformazione possono risultare migliori se le tabelle e gli indici utilizzati si trovano sullo stesso computer locale. Se la tabella di riferimento utilizzata dalla trasformazione Ricerca fuzzy si trova nel server di produzione, è consigliabile copiarla in un server non di produzione e configurare la trasformazione per l'accesso alla copia della tabella. In tal modo le risorse del server di produzione non vengono utilizzate dalle query di ricerca. La trasformazione Ricerca fuzzy, inoltre, esegue la manutenzione dell'indice delle corrispondenze. In caso di impostazione di MatchIndexOptions su **GenerateAndMaintainNewIndex**, quindi, la trasformazione potrebbe bloccare la tabella di riferimento per la durata dell'operazione di pulizia dei dati e impedirne l'accesso da parte di altri utenti e applicazioni.  
  
## <a name="configuring-the-fuzzy-lookup-transformation"></a>Configurazione della trasformazione Ricerca fuzzy  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor trasformazione Ricerca fuzzy** , fare clic su uno degli argomenti seguenti:  
  
-   [Editor trasformazione Ricerca fuzzy &#40;scheda Tabella di riferimento&#41;](../../fuzzy-lookup-transformation-editor-reference-table-tab.md)  
  
-   [Editor trasformazione Ricerca fuzzy &#40;scheda Colonne&#41;](../../fuzzy-lookup-transformation-editor-columns-tab.md)  
  
-   [Editor trasformazione Ricerca fuzzy &#40;scheda Avanzate&#41;](../../fuzzy-lookup-transformation-editor-advanced-tab.md)  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](../../common-properties.md)  
  
-   [Proprietà personalizzate delle trasformazioni](transformation-custom-properties.md)  
  
## <a name="related-tasks"></a>Attività correlate  
 Per informazioni su come impostare le proprietà di un componente del flusso di dati, vedere [Impostare le proprietà di un componente del flusso di dati](../set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Trasformazione Ricerca](lookup-transformation.md)   
 [Trasformazione Raggruppamento fuzzy](fuzzy-grouping-transformation.md)   
 [Trasformazioni di Integration Services](integration-services-transformations.md)  
  
  
