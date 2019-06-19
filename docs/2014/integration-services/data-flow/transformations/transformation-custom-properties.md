---
title: Proprietà personalizzate delle trasformazioni | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- Aggregate transformation [Integration Services]
- Slowly Changing Dimension transformation
- Import Column transformation [Integration Services]
- Sort transformation
- Unpivot transformation
- Merge Join transformation
- Data Mining Query transformation
- Fuzzy Grouping transformation
- Data Conversion transformation
- Fuzzy Lookup transformation
- Term Extraction transformation
- Row Count transformation custom properties [Integration Services]
- transformations [Integration Services], properties
- Pivot transformation
- Lookup transformation
- Percentage Sampling transformation
- Export Column transformation [Integration Services]
- Row Sampling transformation
- Conditional Split transformation custom properties [Integration Services]
- custom properties [Integration Services]
- Audit transformation
- Term Lookup transformation
- Script Component transformation custom properties [Integration Services]
- Derived Column transformation
- OLE DB Command transformation
- Copy Column transformation custom properties [Integration Services]
- Character Map transformation custom properties [Integration Services]
ms.assetid: 56f5df6a-56f6-43df-bca9-08476a3bd931
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1a3e999975f13654a5f3c2f34a2325324c5a36ac
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62770734"
---
# <a name="transformation-custom-properties"></a>proprietà personalizzate della trasformazione
  Oltre alle proprietà comuni alla maggior parte degli oggetti del flusso di dati nel modello a oggetti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] , molti oggetti del flusso di dati hanno proprietà personalizzate specifiche dell'oggetto. Tali proprietà personalizzate sono disponibili solo in fase di esecuzione e non sono trattate nella documentazione di riferimento relativa alla programmazione gestita in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] .  
  
 In questo argomento vengono elencate e descritte le proprietà personalizzate delle diverse trasformazioni del flusso di dati. Per informazioni sulle proprietà comuni alla maggior parte degli oggetti del flusso di dati, vedere [Proprietà comuni](../../common-properties.md).  
  
 È possibile impostare alcune proprietà delle trasformazioni utilizzando espressioni di proprietà. Per altre informazioni, vedere [Proprietà del flusso di dati che è possibile impostare tramite espressioni](../../data-flow-properties-that-can-be-set-by-using-expressions.md).  
  
## <a name="transformations-with-custom-properties"></a>Trasformazioni con proprietà personalizzate  
  
||||  
|-|-|-|  
|[Aggregate](#aggregate)|[Esportazione colonna](#extract)|[Conteggio righe](#rowcount)|  
|[Controllo](#audit)|[Raggruppamento fuzzy](#fgroup)|[Campionamento righe](#rowsamp)|  
|[Trasformazione Cache](#cachetransform)|[Ricerca fuzzy](#flookup)|[Componente script](#script)|  
|[Mappa caratteri](#charmap)|[Importa colonna](#insert)|[Dimensione a modifica lenta](#scd)|  
|[Suddivisione condizionale](#condsplit)|[Ricerca](#lookup)|[Sort](#sort)|  
|[Copia colonna](#copymap)|[Merge Join](#mjoin)|[Estrazione termini](#textract)|  
|[Conversione dati](#dataconv)|[Comando OLE DB](#oledbcmd)|[Ricerca termini](#tlookup)|  
|[Query di data mining](#dmquery)|[Campionamento percentuale](#percent)|[UnPivot](#unpivot)|  
|[Colonna derivata](#derived)|[Pivot](#pivot)||  
  
### <a name="transformations-without-custom-properties"></a>Trasformazioni senza proprietà personalizzate  
 Le trasformazioni seguenti non includono proprietà personalizzate a livello di componente, di input o di output: [Trasformazione Unione](merge-transformation.md), [Trasformazione Multicast](multicast-transformation.md) e [Trasformazione Unione input multipli](union-all-transformation.md). Tali trasformazioni utilizzano solo le proprietà comuni a tutti i componenti del flusso di dati.  
  
##  <a name="aggregate"></a> Proprietà personalizzate della trasformazione Aggregazione  
 La trasformazione Aggregazione include proprietà personalizzate e le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate della trasformazione Aggregazione. Tutte le proprietà sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|AutoExtendFactor|Valore intero|Valore compreso tra 1 e 100 che specifica la possibile percentuale di estensione della memoria durante l'aggregazione. Il valore predefinito di questa proprietà è **25**.|  
|CountDistinctKeys|Valore intero|Valore che specifica il numero esatto di misure Distinct Count che possono essere scritte dall'aggregazione. Se viene specificato un valore CountDistinctScale, il valore in CountDistinctKeys ha la precedenza.|  
|CountDistinctScale|Integer (enumerazione)|Valore che descrive il numero approssimativo di valori distinct in una colonna che possono essere conteggiati dall'aggregazione. Di seguito vengono indicati i possibili valori della proprietà.<br /><br /> **Bassa** (1): indica fino a 500.000 valori di chiave.<br /><br /> **Media** (2): indica fino a 5 milioni di valori di chiave.<br /><br /> **Alta** (3): indica più di 25 milioni di valori di chiave.<br /><br /> **Non specificata** (0): indica che non viene usato alcun valore CountDistinctScale. L'uso dell'opzione **Non specificata** (0) può influire sulle prestazioni nei set di dati di grandi dimensioni.|  
|Chiavi|Valore intero|Valore che specifica il numero esatto di chiavi Group By scritte dall'aggregazione. Se si specifica un valore KeyScale, il valore in Keys ha la precedenza.|  
|KeyScale|Integer (enumerazione)|Valore che descrive approssimativamente il numero di valori di chiave Group By che possono essere scritti dall'aggregazione. Di seguito vengono indicati i possibili valori della proprietà.<br /><br /> **Bassa** (1): indica fino a 500.000 valori di chiave.<br /><br /> **Media** (2): indica fino a 5 milioni di valori di chiave.<br /><br /> **Alta** (3): indica più di 25 milioni di valori di chiave.<br /><br /> **Non specificata** (0): indica che non viene usato alcun valore KeyScale.|  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate dell'output della trasformazione Aggregazione. Tutte le proprietà sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|Chiavi|Valore intero|Valore che specifica il numero esatto di chiavi Group By che possono essere scritte dall'aggregazione. Se si specifica un valore KeyScale, il valore in Keys ha la precedenza.|  
|KeyScale|Integer (enumerazione)|Valore che descrive approssimativamente il numero di valori di chiave Group By che possono essere scritti dall'aggregazione. Di seguito vengono indicati i possibili valori della proprietà.<br /><br /> **Bassa** (1): indica fino a 500.000 valori di chiave.<br /><br /> **Media** (2): indica fino a 5 milioni di valori di chiave.<br /><br /> **Alta** (3): indica più di 25 milioni di valori di chiave.<br /><br /> **Non specificata** (0): indica che non viene usato alcun valore KeyScale.|  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate delle colonne di output della trasformazione Aggregazione. Tutte le proprietà sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|AggregationColumnId|Valore intero|`LineageID` di una colonna inclusa in una clausola GROUP BY o in funzioni di aggregazione.|  
|AggregationComparisonFlags|Valore intero|Valore che specifica il modo in cui la trasformazione Aggregazione confronta i dati di tipo stringa in una colonna. Per altre informazioni, vedere [Comparing String Data](../comparing-string-data.md).|  
|AggregationType|Integer (enumerazione)|Valore che specifica l'operazione di aggregazione da eseguire sulla colonna. Di seguito vengono indicati i possibili valori della proprietà.<br /><br /> **Count** (1)<br /><br /> **Count all** (2)<br /><br /> **Countdistinct** (3)<br /><br /> **Sum** (4)<br /><br /> **Average** (5)<br /><br /> **Maximum** (7)<br /><br /> **Minimum** (6)<br /><br /> **Group by** (0)|  
|CountDistinctKeys|Valore intero|Quando il tipo di aggregazione è **Count Distinct**, valore che specifica il numero esatto di chiavi che possono essere scritte dall'aggregazione. Se viene specificato un valore CountDistinctScale, il valore in CountDistinctKeys ha la precedenza.|  
|CountDistinctScale|Integer (enumerazione)|Quando il tipo di aggregazione è **Count Distinct**, valore che descrive approssimativamente il numero di valori di chiave che possono essere scritti dall'aggregazione. Di seguito vengono indicati i possibili valori della proprietà.<br /><br /> **Bassa** (1): indica fino a 500.000 valori di chiave.<br /><br /> **Media** (2): indica fino a 5 milioni di valori di chiave.<br /><br /> **Alta** (3): indica più di 25 milioni di valori di chiave.<br /><br /> **Non specificata** (0): indica che non viene usato alcun valore CountDistinctScale.|  
|IsBig|Boolean|Valore che indica se la colonna contiene un valore maggiore di 4 miliardi o un valore con una precisione maggiore di un valore a virgola mobile a precisione doppia. Il valore può essere 0 o 1. 0 indica che IsBig è `False` e la colonna non contiene un valore di grandi dimensioni o un valore preciso. Il valore predefinito di questa proprietà è 1.|  
  
 L'input e le colonne di input della trasformazione Aggregazione non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Trasformazione Aggregazione](aggregate-transformation.md).  
  
##  <a name="audit"></a> Proprietà personalizzate della trasformazione Controllo  
 La trasformazione Aggregazione include solo le proprietà comuni a tutti i componenti del flusso di dati a livello di componente.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate delle colonne di output della trasformazione Controllo. Tutte le proprietà sono di lettura/scrittura.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|LineageItemSelected|Integer (enumerazione)|Elemento di controllo selezionato per l'output. Di seguito vengono indicati i possibili valori della proprietà.<br /><br /> **GUID istanza esecuzione** (0)<br /><br /> **Ora di inizio esecuzione** (4)<br /><br /> **Nome computer** (5)<br /><br /> **ID pacchetto** (1)<br /><br /> **Nome pacchetto** (2)<br /><br /> **ID attività** (8)<br /><br /> **Nome attività** (7)<br /><br /> **Nome utente** (6)<br /><br /> **ID versione** (3)|  
  
 L'input, le colonne di input e l'output della trasformazione Controllo non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Trasformazione Controllo](audit-transformation.md).  
  
##  <a name="cachetransform"></a> Proprietà personalizzate della trasformazione Trasformazione cache  
 La trasformazione Trasformazione cache include proprietà personalizzate e le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà della trasformazione Trasformazione cache. Tutte le proprietà sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|Connectionmanager|String|Specifica il nome della gestione connessione.|  
|ValidateExternalMetadata|Boolean|Indica se la trasformazione Trasformazione cache viene convalidata utilizzando origini dati esterne in fase di progettazione. Se la proprietà è impostata su `False`, in fase di esecuzione viene eseguita la convalida rispetto a origini dati esterne.<br /><br /> Il valore predefinito è `True`.|  
|AvailableInputColumns|String|Elenco delle colonne di input disponibili.|  
|InputColumns|String|Elenco delle colonne di input selezionate.|  
|CacheColumnName|String|Specifica il nome della colonna a cui viene eseguito il mapping a una colonna di input selezionata.<br /><br /> Il nome della colonna nella proprietà CacheColumnName deve corrispondere al nome della colonna corrispondente indicato nella pagina **Colonne** di **Editor gestione connessione della cache**.<br /><br /> Per altre informazioni, vedere [Editor gestione connessione cache](../../cache-connection-manager-editor.md)|  
  
##  <a name="charmap"></a> Proprietà personalizzate della trasformazione Mappa caratteri  
 La trasformazione Mappa caratteri include solo le proprietà comuni a tutti i componenti del flusso di dati a livello di componente.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate delle colonne di output della trasformazione Mappa caratteri. Tutte le proprietà sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|InputColumnLineageId|Valore intero|Valore che specifica la proprietà `LineageID` della colonna di input che costituisce l'origine della colonna di output.|  
|MapFlags|Integer (enumerazione)|Valore che specifica le operazioni di stringa eseguite dalla trasformazione Mappa caratteri nella colonna. Di seguito vengono indicati i possibili valori della proprietà.<br /><br /> **Inversione byte** (2)<br /><br /> **Larghezza intera** (6)<br /><br /> **Metà larghezza** (5)<br /><br /> **Hiragana** (3)<br /><br /> **Katakana** (4)<br /><br /> **Conversione da maiuscole a minuscole (e viceversa) basata sulla lingua** (7)<br /><br /> **Minuscolo** (0)<br /><br /> **Cinese semplificato** (8)<br /><br /> **Cinese tradizionale**(9)<br /><br /> **Maiuscolo** (1)|  
  
 L'input, le colonne di input e l'output della trasformazione Mappa caratteri non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Trasformazione Mappa caratteri](character-map-transformation.md).  
  
##  <a name="condsplit"></a> Proprietà personalizzate della trasformazione Suddivisione condizionale  
 La trasformazione Suddivisione condizionale include solo le proprietà comuni a tutti i componenti del flusso di dati a livello di componente.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate dell'output della trasformazione Suddivisione condizionale. Tutte le proprietà sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|EvaluationOrder|Valore intero|Valore che specifica la posizione di una condizione, associata a un output, nell'elenco delle condizioni valutate dalla trasformazione Suddivisione condizionale. Le condizioni vengono valutate in ordine dal valore minimo al valore massimo.|  
|Espressione|String|Espressione che rappresenta la condizione valutata dalla trasformazione Suddivisione condizionale. Le colonne sono rappresentate da identificatori di derivazione.|  
|FriendlyExpression|String|Espressione che rappresenta la condizione valutata dalla trasformazione Suddivisione condizionale. Le colonne sono rappresentate dai relativi nomi.<br /><br /> È possibile specificare il valore di questa proprietà tramite un'espressione di proprietà.|  
|IsDefaultOut|Boolean|Valore che indica se l'output rappresenta l'output predefinito.|  
  
 L'input, le colonne di input e le colonne di output della trasformazione Suddivisione condizionale non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Trasformazione Suddivisione condizionale](conditional-split-transformation.md).  
  
##  <a name="copymap"></a> Proprietà personalizzate della trasformazione Copia colonna  
 La trasformazione Copia colonna include solo le proprietà comuni a tutti i componenti del flusso di dati a livello di componente.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate delle colonne di output della trasformazione Copia colonna. Tutte le proprietà sono di lettura/scrittura.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|copyColumnId|Valore intero|`LineageID` della colonna di input da cui viene copiata la colonna di output.|  
  
 L'input, le colonne di input e l'output della trasformazione Copia colonna non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Trasformazione Copia colonna](copy-column-transformation.md).  
  
##  <a name="dataconv"></a> Proprietà personalizzate della trasformazione Conversione dati  
 La trasformazione Conversione dati include solo le proprietà comuni a tutti i componenti del flusso di dati a livello di componente.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate delle colonne di output della trasformazione Conversione dati. Tutte le proprietà sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|FastParse|Boolean|Valore che indica se la colonna utilizza le routine di analisi più veloci ma indipendenti dalle impostazioni locali disponibili in [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] oppure le routine di analisi standard dipendenti dalle impostazioni locali. Il valore predefinito di questa proprietà è `False`. Per altre informazioni, vedere [Analisi veloce](../../fast-parse.md) e [Analisi standard](../../standard-parse.md). .<br /><br /> Nota: Questa proprietà non è disponibile in **Editor trasformazione Conversione dati**, ma può essere impostata in **Editor avanzato**.|  
|SourceInputColumnLineageId|Valore intero|`LineageID` della colonna di input che costituisce l'origine della colonna di output.|  
  
 L'input, le colonne di input e l'output della trasformazione Conversione dati non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Trasformazione Conversione dati](data-conversion-transformation.md).  
  
##  <a name="dmquery"></a> Proprietà personalizzate della trasformazione Query di data mining  
 La trasformazione Query di data mining include proprietà personalizzate e le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate della trasformazione Query di data mining. Tutte le proprietà sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|ASConnectionId|String|Identificatore univoco dell'oggetto Connection.|  
|ASConnectionString|String|Stringa di connessione a un progetto di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] o a un database di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .|  
|CatalogName|String|Nome di un database di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] .|  
|ModelName|String|Nome del modello di data mining.|  
|ModelStructureName|String|Nome della struttura di data mining.|  
|ObjectRef|String|Tag XML che identifica la struttura di data mining utilizzata dalla trasformazione.|  
|QueryText|String|Istruzione della query di stima utilizzata dalla trasformazione.|  
  
 L'input, le colonne di input, l'output e le colonne di output della trasformazione Query di data mining non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Trasformazione Query di data mining](data-mining-query-transformation.md).  
  
##  <a name="derived"></a> Proprietà personalizzate della trasformazione Colonna derivata  
 La trasformazione Colonna derivata include solo le proprietà comuni a tutti i componenti del flusso di dati a livello di componente.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate delle colonne di input e delle colonne di output della trasformazione Colonna derivata. Quando si sceglie di aggiungere la colonna derivata come nuova colonna, le proprietà personalizzate seguenti vengono applicate alla nuova colonna di output. Quando si sceglie di sostituire il contenuto di una colonna di input esistente con i risultati derivati, le proprietà personalizzate vengono applicate alla colonna di input esistente. Tutte le proprietà sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|Espressione|String|Espressione che rappresenta la condizione valutata dalla trasformazione Suddivisione condizionale. Le colonne sono rappresentate dalla proprietà `LineageID` per la colonna.|  
|FriendlyExpression|String|Espressione che rappresenta la condizione valutata dalla trasformazione Suddivisione condizionale. Le colonne sono rappresentate dai relativi nomi.<br /><br /> È possibile specificare il valore di questa proprietà tramite un'espressione di proprietà.|  
  
 L'input e l'output della trasformazione Colonna derivata non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Trasformazione Colonna derivata](derived-column-transformation.md).  
  
##  <a name="extract"></a> Proprietà personalizzate della trasformazione Esporta colonna  
 La trasformazione Esporta colonna include solo le proprietà comuni a tutti i componenti del flusso di dati a livello di componente.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate delle colonne di input della trasformazione Esporta colonna. Tutte le proprietà sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|AllowAppend|Boolean|Valore che specifica se la trasformazione aggiunge dati a un file esistente. Il valore predefinito di questa proprietà è `False`.|  
|ForceTruncate|Boolean|Valore che specifica se la trasformazione tronca un file esistente prima di scrivere i dati. Il valore predefinito di questa proprietà è `False`.|  
|FileDataColumnID|Valore intero|Valore che identifica la colonna contenente i dati inseriti in un file dalla trasformazione. In colonna estrazione questa proprietà ha un valore pari **0**; nella colonna Percorso File, questa proprietà contiene il `LineageID` di colonna estrazione.|  
|WriteBOM|Boolean|Valore che specifica se nel file viene scritto un indicatore per l'ordine dei byte.|  
  
 L'input, l'output e le colonne di output della trasformazione Esporta colonna non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Trasformazione Esporta colonna](export-column-transformation.md).  
  
##  <a name="insert"></a> Proprietà personalizzate della trasformazione Importa colonna  
 La trasformazione Importa colonna include solo le proprietà comuni a tutti i componenti del flusso di dati a livello di componente.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate delle colonne di input della trasformazione Importa colonna. Tutte le proprietà sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|ExpectBOM|Boolean|Valore che specifica se nella trasformazione Importa colonna è previsto un indicatore per l'ordine dei byte. È previsto un indicatore dell'ordine dei byte solo se i dati sono di tipo DT_NTEXT.|  
|FileDataColumnID|Valore intero|Valore che identifica la colonna contenente i dati inseriti in un flusso di dati dalla trasformazione. Nella colonna di dati da inserire questa proprietà ha un valore pari a 0, mentre nella colonna contenente i percorsi dei file di origine questa proprietà contiene la proprietà `LineageID` della colonna di dati da inserire.|  
  
 L'input, l'output e le colonne di output della trasformazione Importa colonna non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Trasformazione Importa colonna](import-column-transformation.md).  
  
##  <a name="fgroup"></a> Proprietà personalizzate della trasformazione Raggruppamento fuzzy  
 La trasformazione Raggruppamento fuzzy include proprietà personalizzate e le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate della trasformazione Raggruppamento fuzzy. Tutte le proprietà sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|Delimiters|String|Delimitatori di token utilizzati dalla trasformazione. I delimitatori predefiniti includono i caratteri seguenti: spazio ( ), virgola (,), punto (.), punto e virgola (;), due punti (:), trattino (-), virgolette diritte doppie ("), virgolette diritte singole ('), e commerciale (&), barra (/), barra rovesciata (\\), chiocciola (@), punto esclamativo (!), punto interrogativo (?), parentesi di apertura ((), parentesi di chiusura ()), segno di minore (\<), segno di maggiore (>), parentesi quadra di apertura ([), parentesi quadra di chiusura (]), parentesi graffa di apertura ({), parentesi graffa di chiusura (}), barra verticale (&#124;), cancelletto (#), asterisco (*), accento circonflesso (^) e segno di percentuale (%).|  
|Exhaustive|Boolean|Valore che specifica se ogni record di input viene confrontato con tutti gli altri record di input. Il valore `True` è destinato per lo più al debug. Il valore predefinito di questa proprietà è `False`.<br /><br /> Nota: Questa proprietà non è disponibile in **Editor trasformazione Raggruppamento fuzzy**, ma può essere impostata in **Editor avanzato**.|  
|MaxMemoryUsage|Valore intero|Quantità di memoria massima che può essere utilizzata dalla trasformazione. Il valore predefinito di questa proprietà è **0**, che consente l'uso della memoria dinamica.<br /><br /> È possibile specificare il valore di questa proprietà tramite un'espressione di proprietà.<br /><br /> Nota: Questa proprietà non è disponibile in **Editor trasformazione Raggruppamento fuzzy**, ma può essere impostata in **Editor avanzato**.|  
|MinSimilarity|Double|Soglia di somiglianza utilizzata dalla trasformazione per identificare duplicati, espressa come valore compreso tra 0 e 1.  Il valore predefinito di questa proprietà è 0.8.|  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate delle colonne di input della trasformazione Raggruppamento fuzzy. Tutte le proprietà sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|ExactFuzzy|Integer (enumerazione)|Valore che specifica se la trasformazione esegue una corrispondenza fuzzy o una corrispondenza esatta. I valori validi sono **Exact** e **Fuzzy**. Il valore predefinito di questa proprietà è **Fuzzy**.|  
|FuzzyComparisonFlags|Integer (enumerazione)|Valore che specifica il modo in cui la trasformazione confronta i dati di tipo stringa in una colonna. Di seguito vengono indicati i possibili valori della proprietà.<br /><br /> **FullySensitive**<br /><br /> **IgnoreCase**<br /><br /> **IgnoreKanaType**<br /><br /> **IgnoreNonSpace**<br /><br /> **IgnoreSymbols**<br /><br /> **IgnoreWidth**<br /><br /> <br /><br /> Per altre informazioni, vedere [Comparing String Data](../comparing-string-data.md).|  
|LeadingTrailingNumeralsSignificant|Integer (enumerazione)|Valore che specifica l'importanza dei numerali. Di seguito vengono indicati i possibili valori della proprietà.<br /><br /> **LeadingNumeralsSignificant** (1): usare se i numerali iniziali sono significativi.<br /><br /> **TrailingNumeralsSignificant** (2): usare se i numerali finali sono significativi.<br /><br /> **LeadingAndTrailingNumeralsSignificant** (3): usare se sia i numerali iniziali che i numerali finali sono significativi.<br /><br /> **NumeralsNotSpecial** (0): usare se i numerali non sono significativi.|  
|MinSimilarity|Double|Soglia di somiglianza utilizzata per il join sulla colonna, specificata come valore compreso tra 0 e 1. Solo le righe che superano tale soglia vengono considerate corrispondenze.|  
|ToBeCleaned|Boolean|Valore che specifica se la colonna viene utilizzata per identificare duplicati, ovvero se si tratta di una colonna su cui si esegue il raggruppamento. Il valore predefinito di questa proprietà è `False`.|  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate delle colonne di output della trasformazione Raggruppamento fuzzy. Tutte le proprietà sono di lettura/scrittura.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|ColumnType|Integer (enumerazione)|Valore che identifica il tipo di colonna di output. Di seguito vengono indicati i possibili valori della proprietà.<br /><br /> **KeyIn** (1)<br /><br /> **KeyOut** (2)<br /><br /> **Somiglianza** (3)<br /><br /> **ColumnSimilarity** (4)<br /><br /> **PassThru** (5)<br /><br /> **Canonica**l (6)<br /><br /> **Non definito** (0)|  
|InputID|Valore intero|`LineageID` della colonna di input corrispondente.|  
  
 L'input e l'output della trasformazione Raggruppamento fuzzy non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Trasformazione Raggruppamento fuzzy](fuzzy-grouping-transformation.md).  
  
##  <a name="flookup"></a> Proprietà personalizzate della trasformazione Ricerca fuzzy  
 La trasformazione Ricerca fuzzy include proprietà personalizzate e le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate della trasformazione Ricerca fuzzy. Tutte le proprietà, ad eccezione di `ReferenceMetadataXML`, sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|CopyReferenceTable|Boolean|Specifica se è necessario creare una copia della tabella di riferimento per la creazione dell'indice di ricerca fuzzy e le ricerche successive. Il valore predefinito di questa proprietà è `True`.|  
|Delimiters|String|Delimitatori utilizzati dalla trasformazione per suddividere in token i valori di colonna. I delimitatori predefiniti includono i caratteri seguenti: spazio ( ), virgola (,), punto (.), punto e virgola (;), due punti (:), trattino (-), virgolette diritte doppie ("), virgolette diritte singole ('), e commerciale (&), barra (/), barra rovesciata (\\), chiocciola (@), punto esclamativo (!), punto interrogativo (?), parentesi di apertura ((), parentesi di chiusura ()), segno di minore (\<), segno di maggiore (>), parentesi quadra di apertura ([), parentesi quadra di chiusura (]), parentesi graffa di apertura ({), parentesi graffa di chiusura (}), barra verticale (&#124;), cancelletto (#), asterisco (*), accento circonflesso (^) e segno di percentuale (%).|  
|DropExistingMatchIndex|Boolean|Un valore che specifica se l'indice delle corrispondenze specificato in MatchIndexName viene eliminato quando MatchIndexOptions non è impostata su ReuseExistingIndex. Il valore predefinito di questa proprietà è `True`.|  
|Exhaustive|Boolean|Valore che specifica se ogni record di input viene confrontato con tutti gli altri record di input. Il valore `True` è destinato per lo più al debug. Il valore predefinito di questa proprietà è `False`.<br /><br /> Nota: Questa proprietà non è disponibile in **Editor trasformazione Ricerca fuzzy**, ma può essere impostata in **Editor avanzato**.|  
|MatchIndexName|String|Nome dell'indice delle corrispondenze. L'indice delle corrispondenze è la tabella in cui la trasformazione crea e salva l'indice utilizzato. Se viene riusato l'indice delle corrispondenze, MatchIndexName specifica l'indice da riusare. MatchIndexName deve essere un nome di identificatore di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] valido. Se il nome contiene spazi, ad esempio, deve essere racchiuso tra parentesi.|  
|MatchIndexOptions|Integer (enumerazione)|Valore che specifica il modo in cui l'indice delle corrispondenze viene gestito dalla trasformazione. Di seguito vengono indicati i possibili valori della proprietà.<br /><br /> `ReuseExistingIndex` (0)<br /><br /> **GenerateNewIndex** (1)<br /><br /> **GenerateAndPersistNewIndex** (2)<br /><br /> **GenerateAndMaintainNewIndex** (3)|  
|MaxMemoryUsage|Valore intero|Dimensione massima della cache per la tabella di ricerca. Il valore predefinito di questa proprietà è **0**, che indica l'assenza di limiti per le dimensioni della cache.<br /><br /> È possibile specificare il valore di questa proprietà tramite un'espressione di proprietà.<br /><br /> Nota: Questa proprietà non è disponibile in **Editor trasformazione Ricerca fuzzy**, ma può essere impostata in **Editor avanzato**.|  
|MaxOutputMatchesPerInput|Valore intero|Numero massimo di corrispondenze restituite dalla trasformazione per ogni riga di input. Il valore predefinito di questa proprietà è **1**.<br /><br /> Nota: È possibile specificare valori maggiori di 100 solo in **Editor avanzato**.|  
|MinSimilarity|Valore intero|Soglia di somiglianza utilizzata dalla trasformazione a livello di componente, specificata come valore compreso tra 0 e 1. Solo le righe che superano tale soglia vengono considerate corrispondenze.|  
|ReferenceMetadataXML|String|[!INCLUDE[ssInternalOnly](../../../includes/ssinternalonly-md.md)]|  
|ReferenceTableName|String|Nome della tabella di ricerca. Il nome deve essere un nome di identificatore di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] valido. Se il nome contiene spazi, ad esempio, deve essere racchiuso tra parentesi.|  
|WarmCaches|Boolean|Se il valore è True, la ricerca carica parzialmente l'indice e la tabella di riferimento nella memoria prima dell'inizio dell'esecuzione. Ciò può determinare un miglioramento delle prestazioni.|  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate delle colonne di input della trasformazione Ricerca fuzzy. Tutte le proprietà sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|FuzzyComparisonFlags|Valore intero|Valore che specifica il modo in cui la trasformazione confronta i dati di tipo stringa in una colonna. Per altre informazioni, vedere [Comparing String Data](../comparing-string-data.md).|  
|FuzzyComparisonFlagsEx|Integer (enumerazione)|Valore che specifica i flag di confronto estesi utilizzati dalla trasformazione. I valori possono includere **MapExpandLigatures, MapFoldCZone**, **MapFoldDigits**, **MapPrecomposed**e **NoMapping**. Non è possibile usare il flag**NoMapping** con altri flag.|  
|JoinToReferenceColumn|String|Valore che specifica il nome della colonna della tabella di riferimento a cui è unita in join la colonna.|  
|JoinType|Valore intero|Valore che specifica se la trasformazione esegue una corrispondenza fuzzy o una corrispondenza esatta. Il valore predefinito di questa proprietà è **Fuzzy**. L'integer per il tipo di join esatto è **1** , quello per il tipo di join fuzzy è **2**.|  
|MinSimilarity|Double|Soglia di somiglianza utilizzata dalla trasformazione a livello di colonna, specificata come valore compreso tra 0 e 1. Solo le righe che superano tale soglia vengono considerate corrispondenze.|  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate delle colonne di output della trasformazione Ricerca fuzzy. Tutte le proprietà sono di lettura/scrittura.  
  
> [!NOTE]  
>  Per le colonne di output che contengono valori pass-through dalle colonne di input corrispondenti, CopyFromReferenceColumn è vuoto e SourceInputColumnLineageID contiene la `LineageID` della colonna di input corrispondente. Per le colonne di output che contengono risultati di ricerca, CopyFromReferenceColumn contiene il nome della colonna di ricerca, mentre SourceInputColumnLineageID è vuoto.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|ColumnType|Integer (enumerazione)|Valore che identifica il tipo di colonna di output per le colonne aggiunte all'output dalla trasformazione. Di seguito vengono indicati i possibili valori della proprietà.<br /><br /> **Somiglianza** (1)<br /><br /> **Confidenza** (2)<br /><br /> **ColumnSimilarity** (3)<br /><br /> **Non definito** (0)|  
|CopyFromReferenceColumn|String|Valore che specifica il nome della colonna nella tabella di riferimento che fornisce il valore in una colonna di output.|  
|SourceInputColumnLineageId|Valore intero|Valore che identifica la colonna di input che fornisce valori a questa colonna di output.|  
  
 L'input e l'output della trasformazione Ricerca fuzzy non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Trasformazione Ricerca fuzzy](lookup-transformation.md).  
  
##  <a name="lookup"></a> Proprietà personalizzate della trasformazione Ricerca  
 La trasformazione Ricerca include proprietà personalizzate e le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate della trasformazione Ricerca. Tutte le proprietà, ad eccezione di `ReferenceMetadataXML`, sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|CacheType|Integer (enumerazione)|Tipo di cache per la tabella di ricerca. I valori validi sono **Completa** (0), **Parziale** (1) e **Nessuna** (2). Il valore predefinito di questa proprietà è **Completa**.|  
|DefaultCodePage|Valore intero|Tabella codici predefinita da utilizzare quando le informazioni sulla tabella codici non sono disponibili dall'origine dati.|  
|MaxMemoryUsage|Valore intero|Dimensione massima della cache per la tabella di ricerca. Il valore predefinito di questa proprietà è **25**, che indica l'assenza di limiti per la dimensione della cache.|  
|MaxMemoryUsage64|Valore intero|Dimensioni massime della cache per la tabella di ricerca in un computer a 64 bit.|  
|NoMatchBehavior|Integer (enumerazione)|Valore che specifica se le righe prive di voci corrispondenti nel set di dati di riferimento devono essere considerate errori.<br /><br /> Quando la proprietà è impostata su `Treat rows with no matching entries as errors` (0), le righe prive di voci corrispondenti vengono considerate errori. È possibile specificare l'azione necessaria quando viene restituito questo tipo di errore usando la pagina **Output degli errori** della finestra di dialogo **Editor trasformazione Ricerca** . Per altre informazioni, vedere [Editor trasformazione Ricerca &#40;pagina Output degli errori&#41;](../../lookup-transformation-editor-error-output-page.md).<br /><br /> Quando la proprietà è impostata su `Send rows with no matching entries to the no match output` (1), le righe non vengono considerate errori.<br /><br /> Il valore predefinito è `Treat rows with no matching entries as errors` (0).|  
|ParameterMap|String|Elenco con valori delimitati da punti e virgola di ID di derivazione con mapping ai parametri utilizzati nell'istruzione `SqlCommand`.|  
|ReferenceMetadataXML|String|Metadati per le colonne nella tabella di ricerca copiati nell'output dalla trasformazione.|  
|SqlCommand|String|Istruzione SELECT che popola la tabella di ricerca.|  
|SqlCommandParam|String|Istruzione SQL con parametri che popola la tabella di ricerca.|  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate delle colonne di input della trasformazione Ricerca. Tutte le proprietà sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|CopyFromReferenceColumn|String|Nome della colonna nella tabella di riferimento da cui viene copiata una colonna.|  
|JoinToReferenceColumns|String|Nome della colonna nella tabella di riferimento a cui è unita in join una colonna di origine.|  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate delle colonne di output della trasformazione Ricerca. Tutte le proprietà sono di lettura/scrittura.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|CopyFromReferenceColumn|String|Nome della colonna nella tabella di riferimento da cui viene copiata una colonna.|  
  
 L'input e l'output della trasformazione Ricerca non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Trasformazione Ricerca](lookup-transformation.md).  
  
##  <a name="mjoin"></a> Proprietà personalizzate della trasformazione Merge Join  
 La trasformazione Merge Join include proprietà personalizzate e le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate della trasformazione Merge Join.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|JoinType|Integer (enumerazione)|Specifica se il join è un inner join (2), un left outer join (1) o un full join (0).|  
|MaxBuffersPerInput|Valore intero|Non è più necessario configurare il valore della proprietà `MaxBuffersPerInput`, in quanto Microsoft ha apportato modifiche che riducono il rischio di uso di una quantità eccessiva di memoria da parte della trasformazione Merge join. Questo problema si verificava in genere quando tramite i diversi input della trasformazione Merge Join venivano prodotti dati con frequenze irregolari.|  
|NumKeyColumns|Valore intero|Numero di colonne utilizzate nel join.|  
|TreatNullsAsEqual|Boolean|Valore che specifica se la trasformazione considera i valori Null come valori uguali. Il valore predefinito di questa proprietà è `True`. Se il valore della proprietà è `False`, la trasformazione gestisce i valori Null come in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate delle colonne di output della trasformazione Merge Join. Tutte le proprietà sono di lettura/scrittura.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|InputColumnID|Valore intero|`LineageID` della colonna di input da cui vengono copiati dati in questa colonna di output.|  
  
 L'input, le colonne di input e l'output della trasformazione Merge Join non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Trasformazione Merge join](merge-join-transformation.md).  
  
##  <a name="oledbcmd"></a> Proprietà personalizzate della trasformazione Comando OLE DB  
 La trasformazione Comando OLE DB include proprietà personalizzate e le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate della trasformazione Comando OLE DB.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|CommandTimeout|Valore intero|Numero massimo di secondi durante i quali è possibile eseguire il comando SQL prima del timeout. Il valore **0** corrisponde a un intervallo infinito. Il valore predefinito di questa proprietà è **0**.|  
|DefaultCodePage|Valore intero|Tabella codici da utilizzare quando le informazioni sulla tabella codici non sono disponibili dall'origine dati.|  
|SqlCommand|String|Istruzione Transact-SQL eseguita dalla trasformazione per ogni riga nel flusso di dati.<br /><br /> È possibile specificare il valore di questa proprietà tramite un'espressione di proprietà.|  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate delle colonne esterne della trasformazione Comando OLE DB. Tutte le proprietà sono di lettura/scrittura.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|DBParamInfoFlag|Integer (maschera di bit)|Set di flag che descrivono le caratteristiche dei parametri. Per ulteriori informazioni, vedere DBPARAMFLAGSENUM nella documentazione relativa a OLE DB in MSDN Library.|  
  
 L'input, le colonne di input, l'output e le colonne di output della trasformazione Comando OLE DB non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Trasformazione Comando OLE DB](ole-db-command-transformation.md).  
  
##  <a name="percent"></a> Proprietà personalizzate della trasformazione Campionamento percentuale  
 La trasformazione Campionamento percentuale include proprietà personalizzate e le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate della trasformazione Campionamento percentuale.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|SamplingSeed|Valore intero|Valore di inizializzazione utilizzato dal generatore di numeri casuali. Il valore predefinito di questa proprietà è **0**, che indica che la trasformazione usa un conteggio di tick.|  
|SamplingValue|Valore intero|Dimensione del campione come percentuale dell'origine.<br /><br /> È possibile specificare il valore di questa proprietà tramite un'espressione di proprietà.|  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate degli output della trasformazione Campionamento percentuale. Tutte le proprietà sono di lettura/scrittura.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|Selezionato|Boolean|Definisce l'output a cui vengono indirizzate le righe campionate. Nell'output selezionato, selezionato è impostata su `True`, e nella finestra di output non selezionato è impostata su `False`.|  
  
 L'input, le colonne di input e le colonne di output della trasformazione Campionamento percentuale non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Trasformazione Campionamento percentuale](percentage-sampling-transformation.md).  
  
##  <a name="pivot"></a> Proprietà personalizzate della trasformazione tramite Pivot  
 Nella tabella seguente si descrivono le proprietà di componenti personalizzati della trasformazione Pivot.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|**PassThroughUnmatchedPivotKeyts**|Boolean|Impostare su `True` per configurare la trasformazione Pivot in modo da ignorare le righe contenenti valori non riconosciuti nella colonna Chiave pivot e restituire tutti i valori di chiave pivot in un messaggio di log, quando viene eseguito il pacchetto.|  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate delle colonne di input della trasformazione tramite Pivot. Tutte le proprietà sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|PivotUsage|Integer (enumerazione)|Uno dei seguenti valori che specificano il ruolo di una colonna quando viene trasformata tramite pivot il set di dati:<br /><br /> **0**: La colonna non viene trasformata tramite Pivot e i valori di colonna vengono passati all'output della trasformazione.<br /><br /> **1**: La colonna fa parte della chiave del set che identifica una o più righe come parte di un set specifico. Tutte le righe di input con la stessa chiave del set vengono combinate in una singola riga di output.<br /><br /> **2**: La colonna è una colonna pivot. Da ogni valore di colonna viene creata almeno una colonna.<br /><br /> **3**: I valori di questa colonna vengono inseriti in colonne create come risultato della trasformazione tramite Pivot.|  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate delle colonne di output della trasformazione tramite Pivot. Tutte le proprietà sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|PivotKeyValue|String|Uno dei possibili valori della colonna contrassegnata come chiave pivot dal valore della relativa proprietà PivotUsage.<br /><br /> È possibile specificare il valore di questa proprietà tramite un'espressione di proprietà.|  
|SourceColumn ID|Valore intero|`LineageID` di una colonna di input che contiene un valore trasformato tramite Pivot oppure -1. Il valore -1 indica che la colonna non viene utilizzata in un'operazione pivot.|  
  
 Per altre informazioni, vedere [Trasformazione pivot](pivot-transformation.md).  
  
##  <a name="rowcount"></a> Proprietà personalizzate della trasformazione Conteggio righe  
 La trasformazione Conteggio righe include proprietà personalizzate e le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate della trasformazione Conteggio righe. Tutte le proprietà sono di lettura/scrittura.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|VariableName|String|Nome della variabile che contiene il conteggio delle righe.|  
  
 L'input, le colonne di input, l'output e le colonne di output della trasformazione Conteggio righe non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Trasformazione Conteggio righe](row-count-transformation.md).  
  
##  <a name="rowsamp"></a> Proprietà personalizzate della trasformazione Campionamento righe  
 La trasformazione Campionamento righe include proprietà personalizzate e le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate della trasformazione Campionamento righe. Tutte le proprietà sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|SamplingSeed|Valore intero|Valore di inizializzazione utilizzato dal generatore di numeri casuali. Il valore predefinito di questa proprietà è **0**, che indica che la trasformazione usa un conteggio di tick.|  
|SamplingValue|Valore intero|Conteggio delle righe del campione.<br /><br /> È possibile specificare il valore di questa proprietà tramite un'espressione di proprietà.|  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate degli output della trasformazione Campionamento righe. Tutte le proprietà sono di lettura/scrittura.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|Selezionato|Boolean|Definisce l'output a cui vengono indirizzate le righe campionate. Nell'output selezionato, selezionato è impostata su `True`, e nella finestra di output non selezionato è impostata su `False`.|  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate delle colonne di output della trasformazione Campionamento righe. Tutte le proprietà sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|InputColumnLineageId|Valore intero|Valore che specifica la proprietà `LineageID` della colonna di input che costituisce l'origine della colonna di output.|  
  
 L'input e le colonne di input della trasformazione Campionamento righe non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Trasformazione Campionamento righe](row-sampling-transformation.md).  
  
##  <a name="script"></a> Proprietà personalizzate della trasformazione Componente script  
 La trasformazione Componente script include proprietà personalizzate e le proprietà comuni a tutti i componenti del flusso di dati. Le stesse proprietà personalizzate sono disponibili se la trasformazione Componente script funziona come origine, trasformazione o destinazione.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate della trasformazione Componente script. Tutte le proprietà sono di lettura/scrittura.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|ReadOnlyVariables|String|Elenco con valori delimitati da virgole delle variabili disponibili per il componente script per l'accesso in sola lettura.|  
|ReadWriteVariables|String|Elenco con valori delimitati da virgole delle variabili disponibili per la trasformazione Componente script per l'accesso in lettura/scrittura.|  
  
 L'input, le colonne di input, l'output e le colonne di output della trasformazione Componente script non includono proprietà personalizzate, a meno che non vengano create dallo sviluppatore dello script.  
  
 Per altre informazioni, vedere [Componente script](script-component.md).  
  
##  <a name="scd"></a> Proprietà personalizzate della trasformazione Dimensione a modifica lenta  
 La trasformazione Dimensione a modifica lenta include proprietà personalizzate e le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate della trasformazione Dimensione a modifica lenta. Tutte le proprietà sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|CurrentRowWhere|String|Clausola WHERE nell'istruzione SELECT che seleziona la riga corrente fra righe con la stessa chiave business.|  
|EnableInferredMember|Boolean|Valore che specifica se rilevare gli aggiornamenti del membro derivato. Il valore predefinito di questa proprietà è `True`.|  
|FailOnFixedAttributeChange|Boolean|Valore che specifica se la trasformazione ha esito negativo quando le colonne della riga con attributi fissi contengono modifiche o se la ricerca nella tabella delle dimensioni non riesce. Se si prevede che le righe in ingresso contengano nuovi record, impostare questo valore su `True` per fare in modo che la trasformazione continui dopo l'esito negativo della ricerca, in quanto la trasformazione utilizzerà l'errore per identificare nuovi record. Il valore predefinito di questa proprietà è `False`.|  
|FailOnLookupFailure|Boolean|Valore che specifica se la trasformazione ha esito negativo quando la ricerca di un record esistente non riesce. Il valore predefinito di questa proprietà è `False`.|  
|IncomingRowChangeType|Valore intero|Valore che specifica se tutte le righe in ingresso sono righe nuove o se la trasformazione deve rilevare il tipo di modifica.|  
|InferredMemberIndicator|String|Nome di colonna per il membro derivato.|  
|SqlCommand|String|Istruzione SQL utilizzata per creare un set di righe dello schema.|  
|UpdateChangingAttributeHistory|Boolean|Valore che indica se gli aggiornamenti dell'attributo cronologico vengono indirizzati all'output della trasformazione per gli aggiornamenti dell'attributo modificabile.|  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate delle colonne di input della trasformazione Dimensione a modifica lenta. Tutte le proprietà sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|ColumnType|Integer (enumerazione)|Tipo di aggiornamento della colonna. Le prestazioni possono risultare: **Attributo modificabile** (2), **Attributo fisso** (4), **Attributo cronologico** (3), **Chiave** (1) e **Altro** (0).|  
  
 L'input, gli output e le colonne di output della trasformazione Dimensione a modifica lenta non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Trasformazione Dimensione a modifica lenta](slowly-changing-dimension-transformation.md).  
  
##  <a name="sort"></a> Proprietà personalizzate della trasformazione Ordinamento  
 La trasformazione Ordinamento include proprietà personalizzate e le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate della trasformazione Ordinamento. Tutte le proprietà sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|EliminateDuplicates|Boolean|Specifica se la trasformazione rimuove righe duplicate dall'output della trasformazione. Il valore predefinito di questa proprietà è `False`.|  
|MaximumThreads|Valore intero|Contiene il numero massimo di thread che la trasformazione può utilizzare per l'ordinamento. Il valore **0** indica un numero infinito di thread. Il valore predefinito di questa proprietà è **0**.<br /><br /> È possibile specificare il valore di questa proprietà tramite un'espressione di proprietà.|  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate delle colonne di input della trasformazione Ordinamento. Tutte le proprietà sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|NewComparisonFlags|Integer (maschera di bit)|Valore che specifica il modo in cui la trasformazione confronta i dati di tipo stringa in una colonna. Per altre informazioni, vedere [Comparing String Data](../comparing-string-data.md).|  
|NewSortKeyPosition|Valore intero|Valore che specifica l'ordinamento della colonna. Il valore -0 indica che i dati non vengono ordinati nella colonna.|  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate delle colonne di output della trasformazione Ordinamento. Tutte le proprietà sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|SortColumnID|Valore intero|`LineageID` di una colonna di ordinamento.|  
  
 L'input e l'output della trasformazione Ordinamento non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Trasformazione Ordinamento](sort-transformation.md).  
  
##  <a name="textract"></a> Proprietà personalizzate della trasformazione Estrazione termini  
 La trasformazione Estrazione termini include proprietà personalizzate e le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate della trasformazione Estrazione termini. Tutte le proprietà sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|--------------|-----------------|  
|FrequencyThreshold|Valore intero|Valore numerico che indica il numero necessario di occorrenze di un termine prima che questo venga estratto. Il valore predefinito di questa proprietà è **2**.|  
|IsCaseSensitive|Boolean|Valore che specifica se utilizzare la distinzione tra maiuscole e minuscole per l'estrazione di sostantivi e sintagmi nominali. Il valore predefinito di questa proprietà è `False`.|  
|MaxLengthOfTerm|Valore intero|Valore numerico che indica la lunghezza massima di un termine. Questa proprietà si applica solo alle frasi. Il valore predefinito di questa proprietà è **12**.|  
|NeedRefenceData|Boolean|Valore che specifica se la trasformazione utilizza un elenco di termini di esclusione archiviato in una tabella di riferimento. Il valore predefinito di questa proprietà è `False`.|  
|OutTermColumn|String|Nome della colonna contenente i termini di esclusione.|  
|OutTermTable|String|Nome della tabella contenente la colonna con i termini di esclusione.|  
|ScoreType|Valore intero|Valore che specifica il tipo di punteggio da associare al termine. I valori validi sono 0, che indica la frequenza, e 1, che indica un punteggio TFIDF. Il punteggio TFIDF è il prodotto tra la frequenza del termine (TF) e l'inverso della frequenza nei documenti (IDF) espresso dalla ponderazione seguente: TFIDF di un termine T = (frequenza di T) \* log( (numero di righe nell'input) / (numero di righe contenenti T) ). Il valore predefinito di questa proprietà è **0**.|  
|WordOrPhrase|Valore intero|Valore che specifica il tipo di termine. I valori validi sono 0 per indicare solo le parole, 1 per indicare solo i sintagmi nominali e 2 per indicare sia le parole sia i sintagmi nominali. Il valore predefinito di questa proprietà è **0**.|  
  
 L'input, le colonne di input, l'output e le colonne di output della trasformazione Estrazione termini non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Trasformazione Estrazione termini](term-extraction-transformation.md).  
  
##  <a name="tlookup"></a> Proprietà personalizzate della trasformazione Ricerca termini  
 La trasformazione Ricerca termini include proprietà personalizzate e le proprietà comuni a tutti i componenti del flusso di dati.  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate della trasformazione Ricerca termini. Tutte le proprietà sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|IsCaseSensitive|Boolean|Valore che specifica se applicare un confronto con distinzione tra maiuscole e minuscole alla corrispondenza tra il testo della colonna di input e il termine da cercare. Il valore predefinito di questa proprietà è `False`.|  
|RefTermColumn|String|Nome della colonna contenente i termini da cercare.|  
|RefTermTable|String|Nome della tabella contenente la colonna con i termini da cercare.|  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate delle colonne di input della trasformazione Ricerca termini. Tutte le proprietà sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|InputColumnType|Valore intero|Valore che specifica l'utilizzo della colonna. I valori validi sono 0 per una colonna pass-through, 1 per una colonna di ricerca e 2 per una colonna che sia insieme una colonna pass-through e una colonna di ricerca.|  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate delle colonne di output della trasformazione Ricerca termini. Tutte le proprietà sono di lettura/scrittura.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|CustomLineageID|Valore intero|`LineageID` della colonna di input corrispondente se l'oggetto `InputColumnType` di tale colonna è 0 o 2.|  
  
 L'input e l'output della trasformazione Ricerca termini non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Trasformazione Ricerca termini](term-lookup-transformation.md).  
  
##  <a name="unpivot"></a> Proprietà personalizzate delle trasformazioni tramite UnPivot  
 La trasformazione tramite UnPivot include solo le proprietà comuni a tutti i componenti del flusso di dati a livello di componente.  
  
> [!NOTE]  
>  Per illustrare l'uso delle opzioni descritte in questa sezione, viene usato lo scenario UnPivot descritto in [Trasformazione UnPivot](unpivot-transformation.md) .  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate delle colonne di input della trasformazione tramite UnPivot. Tutte le proprietà sono di lettura/scrittura.  
  
|Proprietà|Tipo di dati|Descrizione|  
|--------------|---------------|-----------------|  
|DestinationColumn|Valore intero|`LineageID` della colonna di output a cui viene eseguito il mapping della colonna di input. Il valore -1 indica che il mapping tra la colonna di input e una colonna di output non viene eseguito.|  
|PivotKeyValue|String|Valore copiato in una colonna di output della trasformazione.<br /><br /> È possibile specificare il valore di questa proprietà tramite un'espressione di proprietà.<br /><br /> Nello scenario UnPivot descritto in [Trasformazione UnPivot](unpivot-transformation.md)i valori pivot sono i valori di testo Ham, Coke, Milk, Beer e Chips. Tali valori verranno visualizzati come valori di testo nella nuova colonna Product definita dall'opzione **Nome colonna valore chiave pivot** .|  
  
 Nella tabella seguente vengono descritte le proprietà personalizzate delle colonne di output della trasformazione tramite UnPivot. Tutte le proprietà sono di lettura/scrittura.  
  
|Nome proprietà|Tipo di dati|Descrizione|  
|-------------------|---------------|-----------------|  
|PivotKey|Boolean|Indica se i valori della proprietà `PivotKeyValue` delle colonne di input vengono scritti in questa colonna di output.<br /><br /> Nello scenario UnPivot descritto in [Trasformazione UnPivot](unpivot-transformation.md), il Nome colonna valore chiave pivot è **Product** e designa la nuova colonna **Product** come la colonna in cui viene applicata la trasformazione tramite UnPivot alle colonne Ham, Coke, Milk, Beer e Chips.|  
  
 L'input e l'output della trasformazione tramite UnPivot non includono proprietà personalizzate.  
  
 Per altre informazioni, vedere [Trasformazione UnPivot](unpivot-transformation.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Trasformazioni di Integration Services](integration-services-transformations.md)   
 [Proprietà comuni](../../common-properties.md)   
 [Proprietà del percorso](../../path-properties.md)   
 [Proprietà del flusso di dati che è possibile impostare tramite espressioni](../../data-flow-properties-that-can-be-set-by-using-expressions.md)  
  
  
