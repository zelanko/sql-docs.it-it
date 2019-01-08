---
title: La modalità DirectQuery in Analysis Services | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a51b38dacf5a1ebaf67a19bf8b3761800425a347
ms.sourcegitcommit: 8a64c59c5d84150659a015e54f8937673cab87a0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/08/2018
ms.locfileid: "53072468"
---
# <a name="directquery-mode"></a>Modalità DirectQuery
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Questo articolo descrive *la modalità DirectQuery* per modelli tabulari di Analysis Services a livello di compatibilità 1200 e versioni successive. È possibile attivare la modalità DirectQuery per i modelli realizzati in SSDT o, per i modelli tabulari già distribuiti, è possibile passare alla modalità DirectQuery in SSMS. Prima di scegliere la modalità DirectQuery, è importante comprendere i vantaggi e restrizioni.
  
##  <a name="bkmk_Benefits"></a> Vantaggi
 Per impostazione predefinita, i modelli tabulari utilizzano una cache in memoria per l'archiviazione dei dati e l'esecuzione di query. Se i modelli tabulari eseguono query sui dati residenti in memoria, anche le query più complesse possono essere molto veloci. Esistono tuttavia alcune limitazioni legate all'uso dei dati memorizzati nella cache. In particolare, i set di dati di grandi dimensioni possono superare la memoria disponibile e i requisiti di aggiornamento dei dati possono essere difficili se non impossibili da soddisfare sulla base di una pianificazione di elaborazione regolare.  
  
 DirectQuery supera queste limitazioni sfruttando allo stesso tempo le funzionalità RDBMS che rendono più efficiente l'esecuzione di query. Con DirectQuery:  
  
-   I dati sono sempre aggiornati e non si verifica alcun overhead di gestione supplementare legato alla necessità di conservare una copia separata dei dati nella cache in memoria. Le modifiche ai dati di origine sottostanti possono essere immediatamente riflesse nelle query sul modello di dati.  
  
-   I set di dati possono avere dimensioni maggiori rispetto la capacità di memoria di un server Analysis Services.  
  
-   DirectQuery può trarre vantaggio dall'accelerazione delle query lato provider, ad esempio quella fornita dagli indici di colonna con ottimizzazione per la memoria delle.  
  
-   La sicurezza può essere applicata dal database back-end, tramite le funzionalità di sicurezza a livello di riga dal database. In alternativa, è possibile usare la sicurezza a livello di riga nel modello tramite DAX.  
  
-   Se il modello contiene formule complesse che potrebbero richiedere più query, Analysis Services consente di eseguire l'ottimizzazione per garantire che il piano relativo alla query eseguita sul database back-end sia il più efficiente possibile.  
  
##  <a name="bkmk_prereq"></a>Restrizioni
I modelli tabulari in modalità DirectQuery presentano alcune restrizioni. Prima di cambiare modalità, è importante stabilire se i vantaggi dell'esecuzione di query sul server back-end superano la riduzione della funzionalità.  
  
 Se viene cambiata la modalità di un modello esistente in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], la finestra di progettazione dei modelli segnala all'utente le funzionalità del modello non compatibili con la modalità DirectQuery.  
  
 L'elenco seguente riepiloga le principali restrizioni di funzionalità da tenere presente:  
  
|||  
|-|-|  
|**Area delle funzionalità**|**Restrizione**|  
|**Origini dei dati**|I modelli DirectQuery possono usare solo i dati da un solo database relazionale dei tipi seguenti: SQL Server, Database SQL di Azure, Oracle e Teradata.  Vedere le origini dati supportate per DirectQuery più avanti in questo articolo per informazioni su versione e provider.| 
|**Stored procedure per SQL**|Per i modelli DirectQuery, non è possibile specificare stored procedure in un'istruzione SQL per definire tabelle durante l'uso di Importazione guidata dati. |   
|**Tabelle calcolate**|Le tabelle calcolate non sono supportate nei modelli DirectQuery. Sono invece supportate le colonne calcolate. Se si tenta di convertire un modello tabulare che contiene una tabella calcolata, viene visualizzato un errore che informa che il modello non può contenere i dati incollati.|  
|**Limiti di query**|Il limite di riga predefinito è un milione di righe, aumentabile specificando **MaxIntermediateRowSize** nel file msmdsrv ini. Vedere [Proprietà DAX](../../analysis-services/server-properties/dax-properties.md) per informazioni dettagliate.
|**Formule DAX**|Quando si eseguono query su un modello tabulare in modalità DirectQuery, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] converte tutte le formule DAX e le definizioni di misure in istruzioni SQL. Le formule DAX che contengono elementi non convertibili in sintassi SQL causeranno errori di convalida nel modello.<br /><br /> Questa restrizione riguarda principalmente alcune funzioni DAX. Per le misure, le formule DAX vengono convertite in operazioni basate su set nell'archivio dati relazionale. Per questo motivo, sono supportate tutte le misure create in modo implicito. <br /><br /> Quando si verifica un errore di convalida, è necessario, riscrivere una formula, inserire una funzione diversa o applicare una soluzione alternativa usando colonne derivate nell'origine dati.  Se un modello tabulare include formule contenenti funzioni incompatibili, queste verranno indicate quando si passa alla modalità DirectQuery nella finestra di progettazione. <br /><br />**Nota:**  Alcune formule del modello vengono convalidate quando si passa alla modalità DirectQuery, ma restituiscono risultati diversi a seconda che vengano eseguite nella cache o nell'archivio dati relazionale. Il motivo è che i calcoli eseguiti sulla cache usano la semantica del motore di analisi in memoria che contiene molte funzionalità intese a emulare il comportamento di Excel, mentre le query eseguite sui dati archiviati sull'origine dati relazionali usano la semantica di SQL Server.<br /><br />Per altre informazioni, vedere [compatibilità delle formule DAX in modalità DirectQuery](../../analysis-services/tabular-models/dax-formula-compatibility-in-directquery-mode-ssas-2016.md).|  
|**Coerenza delle formula**|In alcuni casi, la stessa formula può restituire risultati diversi in un modello memorizzato nella cache rispetto a un modello DirectQuery che usa unicamente l'archivio dati relazionale. Queste differenze sono una conseguenza delle differenze semantiche tra il motore di analisi in memoria e SQL Server.<br /><br /> Per un elenco completo dei problemi di compatibilità, incluse le funzioni che potrebbero restituire risultati diversi quando il modello viene distribuito in tempo reale, vedere [compatibilità delle formule DAX in modalità DirectQuery (SQL Server Analysis Services)](http://msdn.microsoft.com/981b6a68-434d-4db6-964e-d92f8eb3ee3e).|  
|**Limitazioni MDX**|Nessun nome di oggetto relativo. Tutti i nomi di oggetto devono essere completi.<br /><br /> Nessuna istruzione MDX con ambito sessione (set denominati, membri calcolati, celle calcolate, totali visualizzati, membri predefiniti e così via), ma è possibile usare costrutti con ambito query, come la clausola 'WITH'.<br /><br /> Nessuna tupla con membri da livelli diversi in clausole sub-SELECT MDX.<br /><br /> Nessuna gerarchia definita dall'utente.<br /><br /> Nessuna query SQL nativa. Normalmente, Analysis Services supporta un subset T-SQL, ma non per modelli DirectQuery.|  

## <a name="data-sources-supported-for-directquery"></a>Origini dati supportate per DirectQuery
I modelli tabulari DirectQuery a livello di compatibilità 1200 e versioni successiva sono compatibili con i provider e origini dati seguenti:

Origine dati   |Versioni  |Provider
---------|---------|---------
Microsoft SQL Server    |  2008 e versioni successive      |       Provider OLE DB per SQL Server, provider OLE DB di SQL Server Native Client, provider di dati .NET Framework per SQL Client  
Database SQL di Microsoft Azure    |   All      |  Provider OLE DB per SQL Server, provider OLE DB di SQL Server Native Client, provider di dati .NET Framework per SQL Client            
Microsoft Azure SQL Data Warehouse     |   All     |  Provider di dati .NET Framework per SQL Client       
Piattaforma di strumenti analitici Microsoft SQL     |   All      |  Provider OLE DB per SQL Server, provider OLE DB di SQL Server Native Client, provider di dati .NET Framework per SQL Client       
Database relazionali Oracle     |  Oracle 9i e versioni successive       |  Provider OLE DB Oracle       
Database relazionali di Teradata    |  Teradata V2R6 e versioni successive     | Provider di dati .NET per Teradata        

## <a name="connecting-to-a-data-source"></a>Connessione a un'origine dati
Quando si progetta un modello DirectQuery in SSDT, connettendosi a un'origine dati e selezionando le tabelle e campi da includere nel modello è un'operazione molto simile a quanto avviene con modelli in memoria. 

Se DirectQuery è già attiva ma non è stata ancora connessa a un'origine dati, è possibile usare Importazione guidata tabella per la connessione all'origine dati, la selezione di tabelle e campi, la specifica di query SQL e così via. La differenza è che al termine dell'operazione nessun dato viene effettivamente importato nella cache in memoria. 

![Importazione DirectQuery completata](../../analysis-services/tabular-models/media/directquery-import-success.png)

Se Importazione guidata tabella è stata già usata per importare dati, ma la modalità DirectQuery non è ancora attiva, quando questa operazione verrà eseguita la memoria cache verrà cancellata.

  
## <a name="additional-articles-in-this-section"></a>Altri articoli in questa sezione
[Abilitare la modalità DirectQuery in SSDT](../../analysis-services/tabular-models/enable-directquery-mode-in-ssdt.md)

[Abilitare la modalità DirectQuery in SSMS](../../analysis-services/tabular-models/enable-directquery-mode-in-ssms.md)

[Aggiungere dati di esempio a un modello DirectQuery in modalità progettazione](../../analysis-services/tabular-models/add-sample-data-to-a-directquery-model-in-design-mode.md)

[Definire le partizioni nei modelli DirectQuery](../../analysis-services/tabular-models/define-partitions-in-directquery-models-ssas-tabular.md)
  
[Testare un modello in modalità DirectQuery](../../analysis-services/tabular-models/test-a-model-in-directquery-mode.md)

[Compatibilità delle formule DAX in modalità DirectQuery](../../analysis-services/tabular-models/dax-formula-compatibility-in-directquery-mode-ssas-2016.md)
  
