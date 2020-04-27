---
title: Modello a oggetti per il caricamento bulk XML di SQL Server (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- bulk load [SQLXML], object model
- ErrorLogFile property
- SGDropTables property
- SGUseID property
- KeepNulls property
- ConnectionCommand property
- SchemaGen property
- XMLFragment property
- SQLXMLBulkLoad object
- ForceTableLock property
- CheckConstraints property
- BulkLoad property
- TempFilePath property
- IgnoreDuplicateKeys property
- Transaction property
- KeepIdentity property
- ConnectionString property
- FireTriggers property
- Execute method
- XML Bulk Load [SQLXML], object model
ms.assetid: a9efbbde-ed2b-4929-acc1-261acaaed19d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1bf68b7f2c8fd1a2cc8d753ddd6348e8161b55c8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66013286"
---
# <a name="sql-server-xml-bulk-load-object-model-sqlxml-40"></a>Modello a oggetti per il caricamento bulk XML di SQL Server (SQLXML 4.0)
  Il modello [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a oggetti Microsoft XML bulk load è costituito dall'oggetto SQLXMLBulkLoad. Questo oggetto supporta i metodi e le proprietà seguenti.  
  
## <a name="methods"></a>Metodi  
 Execute  
 Esegue il caricamento bulk dei dati utilizzando il file dello schema e il file di dati (o flusso) forniti come parametri.  
  
## <a name="properties"></a>Proprietà  
 BulkLoad  
 Specifica se deve essere eseguito un caricamento bulk. Questa proprietà è utile se si desidera generare solo gli schemi (vedere le proprietà SchemaGen, SGDropTables e SGUseID che seguono) e non eseguire un caricamento bulk. Si tratta di una proprietà booleana. Quando la proprietà è impostata su TRUE, viene eseguito il caricamento bulk XML. Quando la proprietà è impostata su FALSE, il caricamento bulk XML non viene eseguito.  
  
 Il valore predefinito è TRUE.  
  
 CheckConstraints  
 Specifica se i vincoli (ad esempio vincoli dovuti alla relazione di chiave primaria/chiave esterna fra colonne) specificati nella colonna devono essere controllati quando il caricamento bulk XML inserisce dati nelle colonne. Si tratta di una proprietà booleana.  
  
 Quando la proprietà è impostata su TRUE, il caricamento bulk XML controlla i vincoli per ogni valore inserito. Di conseguenza, la violazione di un vincolo produce un errore.  
  
> [!NOTE]  
>  Per lasciare questa proprietà impostata su FALSE, è necessario disporre delle autorizzazioni **ALTER TABLE** per le tabelle di destinazione. Per altre informazioni, vedere [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql).  
  
 Il valore predefinito è FALSE. Quando la proprietà è impostata su FALSE, il caricamento bulk XML ignora i vincoli durante un'operazione di inserimento. Nell'implementazione corrente è necessario definire le tabelle nell'ordine delle relazioni di chiave primaria/chiave esterna nello schema di mapping. Di conseguenza, una tabella con una chiave primaria deve essere definita prima della tabella corrispondente contenente la chiave esterna. In caso contrario, il caricamento bulk XML restituisce un errore.  
  
 Si noti che se viene eseguita la propagazione degli ID, questa opzione non viene applicata e il controllo dei vincoli resta attivato. Ciò si verifica quando `KeepIdentity=False` ed è presente una relazione definita in cui il padre è un campo di identità e il valore viene assegnato al figlio non appena generato.  
  
 ConnectionCommand  
 Identifica un oggetto connessione esistente, ad esempio l'oggetto comando ADO o ICommand, che deve essere utilizzato dal caricamento bulk XML. È possibile usare la proprietà ConnectionCommand invece di specificare una stringa di connessione con la proprietà ConnectionString. Se si utilizza ConnectionCommand, è necessario impostare la proprietà Transaction su TRUE.  
  
 Se si utilizzano entrambe le proprietà ConnectionString e ConnectionCommand, il caricamento bulk XML utilizza l'ultima proprietà specificata.  
  
 Il valore predefinito è NULL.  
  
 ConnectionString  
 Identifica la stringa di connessione OLE DB che fornisce le informazioni necessarie per stabilire una connessione a un'istanza del database. Se si utilizzano entrambe le proprietà ConnectionString e ConnectionCommand, il caricamento bulk XML utilizza l'ultima proprietà specificata.  
  
 Il valore predefinito è NULL.  
  
 ErrorLogFile  
 Specifica il nome del file in cui vengono registrati errori e messaggi dal caricamento bulk XML. Il valore predefinito è una stringa vuota, a indicare che non viene eseguita alcuna registrazione.  
  
 FireTriggers  
 Specifica se i trigger definiti nelle tabelle di destinazione devono essere attivati durante l'operazione di caricamento bulk. Il valore predefinito è FALSE.  
  
 Quando la proprietà è impostata su TRUE, i trigger vengono attivati normalmente durante le operazioni di inserimento.  
  
> [!NOTE]  
>  Per lasciare questa proprietà impostata su FALSE, è necessario disporre delle autorizzazioni **ALTER TABLE** per le tabelle di destinazione. Per altre informazioni, vedere [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql).  
  
 Si noti che se viene eseguita la propagazione degli ID, questa opzione non viene applicata e i trigger restano attivati. Ciò si verifica quando `KeepIdentity=False` ed è presente una relazione definita in cui il padre è un campo di identità e il valore viene assegnato al figlio non appena generato.  
  
 ForceTableLock alla  
 Specifica se le tabelle in cui vengono copiati i dati tramite il caricamento bulk XML devono essere bloccate per la durata del caricamento bulk stesso. Si tratta di una proprietà booleana. Quando questa proprietà è impostata su TRUE, il caricamento bulk XML acquisisce blocchi di tabella per la durata del caricamento bulk stesso. Quando la proprietà è impostata su FALSE, il caricamento bulk XML acquisisce un blocco di tabella ogni volta che inserisce un record in una tabella.  
  
 Il valore predefinito è FALSE.  
  
 IgnoreDuplicateKeys  
 Specifica l'operazione da effettuare se viene eseguito un tentativo di inserimento di valori duplicati in una colonna chiave. Se questa proprietà è impostata su TRUE e viene eseguito un tentativo di inserimento di un record con un valore duplicato in una colonna chiave, il record non viene inserito in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Viene invece inserito il record successivo. L'operazione di caricamento bulk, pertanto, non ha esito negativo. Se la proprietà è impostata su FALSE, il caricamento bulk non riesce quando viene eseguito un tentativo di inserimento di un valore duplicato in una colonna chiave.  
  
 Quando la Proprietà IgnoreDuplicateKeys è impostata su TRUE, viene eseguita un'istruzione COMMIT per ogni record inserito nella tabella. Questo comportamento provoca una riduzione delle prestazioni. La proprietà può essere impostata su TRUE solo quando la proprietà Transaction è impostata su FALSE, perché il comportamento transazionale viene implementato utilizzando i file.  
  
 Il valore predefinito è FALSE.  
  
 KeepIdentity  
 Specifica la modalità di gestione dei valori per una colonna di tipo Identity nel file di origine. Si tratta di una proprietà booleana. Quando la proprietà è impostata su TRUE, il caricamento bulk XML assegna i valori specificati nel file di origine alla colonna Identity. Quando la proprietà è impostata su FALSE, l'operazione di caricamento bulk ignora i valori di colonna di tipo Identity specificati nell'origine. In questo caso, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] assegna un valore alla colonna Identity.  
  
 Se il caricamento bulk interessa una colonna che è una chiave esterna che fa riferimento a una colonna Identity in cui sono archiviati valori generati da [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], il caricamento bulk propaga in modo appropriato tali valori Identity nella colonna chiave esterna.  
  
 Il valore di questa proprietà si applica a tutte le colonne interessate dal caricamento bulk. Il valore predefinito è TRUE.  
  
> [!NOTE]  
>  Per lasciare questa proprietà impostata su TRUE, è necessario disporre delle autorizzazioni **ALTER TABLE** per le tabelle di destinazione. In caso contrario, la proprietà deve essere impostata sul valore FALSE. Per altre informazioni, vedere [ALTER TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-table-transact-sql).  
  
 KeepNulls  
 Specifica il valore da utilizzare per una colonna in cui manca un attributo corrispondente o un elemento figlio nel documento XML. Si tratta di una proprietà booleana. Quando la proprietà è impostata su TRUE, il caricamento bulk XML assegna un valore Null alla colonna. Non viene assegnato il valore predefinito della colonna, se presente, in base all'impostazione nel server. Il valore di questa proprietà si applica a tutte le colonne interessate dal caricamento bulk.  
  
 Il valore predefinito è FALSE.  
  
 SchemaGen  
 Specifica se creare le tabelle necessarie prima di eseguire un'operazione di caricamento bulk. Si tratta di una proprietà booleana. Se questa proprietà è impostata su TRUE, vengono create le tabelle identificate nello schema di mapping (il database deve essere presente). Se una o più tabelle sono già presenti nel database, la proprietà SGDropTables determina se le tabelle preesistenti devono essere eliminate e ricreate.  
  
 Il valore predefinito per la proprietà SchemaGen è FALSE. SchemaGen non crea vincoli PRIMARY KEY nelle tabelle appena create. SchemaGen, tuttavia, crea vincoli FOREIGN KEY nel database se è in grado di trovare le `sql:relationship` annotazioni e `sql:key-fields` corrispondenti nello schema di mapping e se il campo chiave è costituito da una sola colonna.  
  
 Si noti che se si imposta la proprietà SchemaGen su TRUE, il caricamento bulk XML esegue le operazioni seguenti:  
  
-   Vengono create le tabelle necessarie dai nomi di elemento e di attributo. È pertanto importante non utilizzare parole riservate di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per i nomi di elemento e di attributo nello schema.  
  
-   Restituisce i dati di overflow per qualsiasi colonna designata utilizzando [SQL: overflow-field](annotation-interpretation-sql-overflow-field.md) nel formato del [tipo di dati XML](/sql/t-sql/xml/xml-transact-sql) .  
  
 SGDropTables  
 Specifica se le tabelle esistenti devono essere eliminate e ricreate. Usare questa proprietà quando la proprietà SchemaGen è impostata su TRUE. Se SGDropTables è FALSE, le tabelle esistenti vengono mantenute. Quando questa proprietà è TRUE, le tabelle esistenti vengono eliminate e ricreate.  
  
 Il valore predefinito è FALSE.  
  
 SGUseID  
 Specifica se l'attributo nello schema di mapping identificato come tipo `id` può essere utilizzato per la creazione di un vincolo PRIMARY KEY quando viene creata la tabella. Utilizzare questa proprietà quando la proprietà SchemaGen è impostata su TRUE. Se SGUseID è TRUE, l'utilità SchemaGen utilizza un attributo per il `dt:type="id"` quale viene specificato come colonna chiave primaria e aggiunge il vincolo di chiave primaria appropriato durante la creazione della tabella.  
  
 Il valore predefinito è FALSE.  
  
 TempFilePath  
 Specifica il percorso del file in cui il caricamento bulk XML crea i file temporanei per un caricamento bulk in transazioni. Questa proprietà è utile solo quando la proprietà Transaction è impostata su TRUE. È necessario assicurarsi che l' [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] account utilizzato per il caricamento bulk XML abbia accesso a questo percorso. Se questa proprietà non è impostata, il caricamento bulk XML archivia i file temporanei nel percorso specificato nella variabile di ambiente TEMP.  
  
 Transazione  
 Specifica se il caricamento bulk deve essere eseguito come transazione. In questo caso, è garantito il rollback se il caricamento bulk ha esito negativo. Si tratta di una proprietà booleana. Se la proprietà è impostata su TRUE, il caricamento bulk viene eseguito in un contesto transazionale. La proprietà TempFilePath è utile solo quando Transaction è impostato su TRUE.  
  
> [!NOTE]  
>  Se si caricano dati binari (ad esempio i tipi di dati XML bin. Hex, bin. Base64 nei tipi di dati [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Binary, image), la proprietà Transaction deve essere impostata su false.  
  
 Il valore predefinito è FALSE.  
  
 XMLFragment  
 Specifica se i dati di origine sono un frammento XML. Un frammento XML è un documento XML privo di singolo elemento di livello principale (radice). Si tratta di una proprietà booleana. Questa proprietà deve essere impostata su TRUE se il file di origine è costituito da un frammento XML.  
  
 Il valore predefinito è FALSE.  
  
  
