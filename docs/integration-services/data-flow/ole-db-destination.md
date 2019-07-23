---
title: Destinazione OLE DB | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.oledbdest.f1
- sql13.dts.designer.oledbdestadapter.connection.f1
- sql13.dts.designer.oledbdestadapter.mappings.f1
- sql13.dts.designer.oledbdestadapter.errorhandling.f1
helpviewer_keywords:
- fast-load data access mode [Integration Services]
- OLE DB destination [Integration Services]
- fast load options [Integration Services]
- fast-load options [Integration Services]
- destinations [Integration Services], OLE DB
- fast load data access mode [Integration Services]
- inserting data
ms.assetid: 873a2fa0-2a02-41fc-a80a-ec9767f36a8a
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 0e406e5966b9b865d7e25d8156880f333d5cba26
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67897152"
---
# <a name="ole-db-destination"></a>Destinazione OLE DB

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  La destinazione OLE DB consente di caricare dati in un'ampia gamma di database conformi con OLE DB, tramite una tabella o vista di database oppure un comando SQL. L'origine OLE DB, ad esempio, può caricare dati nelle tabelle dei database di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Access e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Se l'origine dati è [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007, è richiesta una gestione connessione diversa rispetto alle versioni precedenti di Excel. Per altre informazioni, vedere [Connessione a una cartella di lavoro di Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md).  
  
 Sono disponibili cinque diverse modalità di accesso ai dati per il caricamento dei dati:  
  
-   Vista o tabella. È possibile specificare una vista o tabella esistente o creare una nuova tabella.  
  
-   Vista o tabella che utilizza opzioni per il caricamento rapido. È possibile specificare una tabella esistente o creare una nuova tabella.  
  
-   Vista o tabella specificata in una variabile.  
  
-   Vista o tabella specificata in una variabile che utilizza opzioni per il caricamento rapido.  
  
-   Risultato di un'istruzione SQL.  
  
> [!NOTE]  
>  La destinazione OLE DB non supporta parametri. Per eseguire un'istruzione INSERT con parametri, è possibile utilizzare la trasformazione Comando OLE DB. Per altre informazioni, vedere [Trasformazione Comando OLE DB](../../integration-services/data-flow/transformations/ole-db-command-transformation.md).  
  
 Quando nella destinazione OLE DB vengono caricati dati che utilizzano un Double-Byte Character Set (DBCS), è possibile che tali dati vengano danneggiati se nella modalità di accesso non viene utilizzata l'opzione di caricamento rapido e la gestione connessione OLE DB utilizza il provider [!INCLUDE[msCoName](../../includes/msconame-md.md)] OLE DB per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SQLOLEDB). Per assicurare l'integrità dei dati DBCS è necessario configurare Gestione connessione OLE DB in modo da usare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client o una delle modalità di accesso con caricamento rapido: **Tabella o vista - Caricamento rapido** o **Variabile nome vista o nome tabella - Caricamento rapido**. Entrambe le opzioni sono disponibili nella finestra di dialogo **Editor destinazione OLE DB** . Durante la programmazione modello a oggetti di [!INCLUDE[ssIS](../../includes/ssis-md.md)], è necessario impostare la proprietà AccessMode su **OpenRowset con FastLoad** o **OpenRowset con FastLoad da variabile**.  
  
> [!NOTE]  
>  Se si usa la finestra di dialogo **Editor destinazione OLE DB[!INCLUDE[ssIS](../../includes/ssis-md.md)] in Progettazione**  per creare la tabella di destinazione in cui la destinazione OLE DB inserisce i dati, sarà necessario selezionare la nuova tabella manualmente. È necessario eseguire la selezione manuale quando un provider OLE DB, ad esempio il provider Microsoft OLE DB per DB2, aggiunge automaticamente gli identificatori di schema al nome della tabella.  
  
> [!NOTE]  
>  In base al tipo di destinazione può essere necessario modificare l'istruzione CREATE TABLE generata dalla finestra di dialogo **Editor destinazione OLE DB** . Alcune destinazioni non supportano ad esempio i tipi di dati utilizzati dall'istruzione CREATE TABLE.  
  
 Per connettersi a un'origine dei dati questa destinazione utilizza una gestione connessione OLE DB, che specifica il provider OLE DB da utilizzare. Per altre informazioni, vedere [Gestione connessione OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md).  
  
 Con un progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] viene inoltre fornito l'oggetto di origine dati da cui è possibile creare una gestione connessione OLE DB, rendendo disponibili origini dati e viste origine dati alla destinazione OLE DB.  
  
 Una destinazione OLE DB include i mapping tra le colonne di input e quelle nell'origine dei dati della destinazione. Non è necessario eseguire il mapping delle colonne di input a tutte le colonne di destinazione ma, a seconda delle proprietà delle colonne di destinazione, se alle colonne di destinazione non corrispondono colonne di input è possibile che vengano generati errori. Se, ad esempio, una colonna di destinazione non ammette valori Null, sarà necessario eseguire il mapping di una colonna di input a tale colonna. È inoltre necessario che i tipi di dati delle colonne di cui è stato eseguito il mapping siano compatibili. Non è ad esempio possibile eseguire il mapping di una colonna di input con un tipo di dati string a una colonna di destinazione con un tipo di dati numeric.  
  
 La destinazione OLE DB include un input regolare e un output degli errori.  
  
 Per altre informazioni sui tipi di dati, vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="fast-load-options"></a>Opzioni per il caricamento rapido  
 Se la destinazione OLE DB usa una modalità di accesso ai dati con caricamento rapido, nell'interfaccia utente della destinazione, ovvero in **Editor destinazione OLE DB**, sarà possibile specificare le opzioni di caricamento rapido seguenti:  
  
-   È possibile mantenere i valori Identity del file di dati importato o utilizzare valori univoci assegnati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   È possibile mantenere i valori Null durante le operazioni di caricamento bulk.  
  
-   È possibile controllare i vincoli sulla tabella o vista di destinazione durante le operazioni di importazione bulk.  
  
-   È possibile acquisire un blocco a livello di tabella per la durata dell'operazione di caricamento bulk.  
  
-   È possibile specificare il numero di righe nel batch e le dimensioni del commit.  
  
 Alcune opzioni di caricamento rapido sono archiviate in proprietà specifiche della destinazione OLE DB. Ad esempio, FastLoadKeepIdentity specifica se mantenere i valori Identity, FastLoadKeepNulls specifica se mantenere i valori Null e FastLoadMaxInsertCommitSize specifica il numero di righe di cui eseguire il commit come batch. Altre opzioni di caricamento rapido sono archiviate in un elenco con valori delimitati da virgole nella proprietà FastLoadOptions. Se la destinazione OLE DB usa tutte le opzioni di caricamento rapido archiviate in FastLoadOptions ed elencate nella finestra di dialogo **Editor destinazione OLE DB** , il valore della proprietà verrà impostato su **TABLOCK, CHECK_CONSTRAINTS, ROWS_PER_BATCH=1000**. Il valore 1000 indica che la destinazione è configurata per l'utilizzo di batch di 1000 righe.  
  
> [!NOTE]  
>  Un eventuale esito negativo della verifica dei vincoli nella destinazione causa l'interruzione dell'intero batch di righe definito da FastLoadMaxInsertCommitSize.  
  
 Oltre alle opzioni di caricamento rapido elencate nella finestra di dialogo **Editor destinazione OLE DB** , è possibile configurare la destinazione OLE DB in modo da usare le opzioni per il caricamento bulk seguenti digitandole nella proprietà FastLoadOptions della finestra di dialogo **Editor avanzato** .  
  
|Opzione per il caricamento rapido|Descrizione|  
|----------------------|-----------------|  
|KILOBYTES_PER_BATCH|Specifica le dimensioni in kilobyte del batch da inserire. L'opzione ha il formato **KILOBYTES_PER_BATCH** = \< valore intero positivo **>** .|  
|FIRE_TRIGGERS|Specifica se attivare o meno i trigger sulla tabella inserita. La sintassi dell'opzione è **FIRE_TRIGGERS**. La presenza dell'opzione indica che i trigger vengono attivati.|  
|ORDER|Specifica la modalità con ordinare i dati in input. La sintassi dell'opzione è ORDER \<nome colonna> ASC&#124;DESC. È possibile elencare qualsiasi numero di colonne e l'indicazione del tipo di ordinamento è facoltativa. Se il tipo di ordinamento viene omesso, l'operazione di inserimento verrà eseguita presupponendo che i dati non siano ordinati.<br /><br /> Nota: è possibile migliorare le prestazioni usando l'opzione ORDER per ordinare i dati di input in base all'indice cluster nella tabella.|  
  
 Anche se nelle parole chiave non viene rilevata la distinzione tra maiuscole e minuscole, le parole chiave [!INCLUDE[tsql](../../includes/tsql-md.md)] vengono in genere digitate in maiuscolo.  
  
 Per sapere di più sulle opzioni di caricamento rapido, vedere [BULK INSERT &#40;Transact-SQL&#41;](../../t-sql/statements/bulk-insert-transact-sql.md).  
  
## <a name="troubleshooting-the-ole-db-destination"></a>Risoluzione dei problemi relativi alla destinazione OLE DB  
 È possibile registrare le chiamate eseguite dalla destinazione OLE DB a provider di dati esterni. Questa funzionalità di registrazione può essere utilizzata per risolvere i problemi relativi al salvataggio di dati in origini dati esterne da parte della destinazione OLE DB. Per registrare le chiamate eseguite dalla destinazione OLE DB a provider di dati esterni, attivare la registrazione dei pacchetti e selezionare l'evento **Diagnostic** a livello di pacchetto. Per altre informazioni, vedere [Risoluzione dei problemi relativi agli strumenti per l'esecuzione del pacchetto](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="configuring-the-ole-db-destination"></a>Configurazione della destinazione OLE DB  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Nella finestra di dialogo **Editor avanzato** sono disponibili le proprietà che è possibile impostare a livello di codice. Per ulteriori informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor avanzato** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Proprietà personalizzate OLE DB](../../integration-services/data-flow/ole-db-custom-properties.md)  
  
 Per ulteriori informazioni sulle procedure per l'impostazione delle proprietà, fare clic su uno degli argomenti seguenti:  
  
-   [Caricamento dei dati tramite la destinazione OLE DB](../../integration-services/data-flow/load-data-by-using-the-ole-db-destination.md)  
  
-   [Impostazione delle proprietà di un componente del flusso di dati](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="ole-db-destination-editor-connection-manager-page"></a>Editor destinazione OLE DB (pagina Gestione connessione)
  Usare la pagina **Gestione connessione** della finestra di dialogo **Editor destinazione OLE DB** per selezionare la connessione OLE DB per la destinazione. Tramite questa pagina è inoltre possibile selezionare una tabella o una vista del database.  
  
> [!NOTE]  
>  Se l'origine dati è [!INCLUDE[msCoName](../../includes/msconame-md.md)] Office Excel 2007, è richiesta una gestione connessione diversa rispetto alle versioni precedenti di Excel. Per altre informazioni, vedere [Connessione a una cartella di lavoro di Excel](../../integration-services/connection-manager/connect-to-an-excel-workbook.md).  
  
> [!NOTE]  
>  La proprietà **CommandTimeout** della destinazione OLE DB non è disponibile nell' **Editor destinazione OLE DB**, tuttavia può essere impostata usando l' **Editor avanzato**. Inoltre alcune opzioni di caricamento rapido sono disponibili solo nell' **Editor avanzato**. Per altre informazioni su queste proprietà, vedere la sezione relativa alla destinazione OLE DB in [Proprietà personalizzate OLE DB](../../integration-services/data-flow/ole-db-custom-properties.md).  
  
### <a name="static-options"></a>Opzioni statiche  
 **Gestione connessione OLE DB**  
 Selezionare una gestione connessione esistente nell'elenco o crearne una nuova facendo clic su **Nuova**.  
  
 **Nuova**  
 Consente di creare una nuova gestione connessione usando la finestra di dialogo **Configura gestione connessione OLE DB** .  
  
 **Modalità di accesso ai dati**  
 Consente di specificare il metodo di caricamento dei dati nella destinazione. Per i dati DBCS (Double-Byte Character Set) è necessario utilizzare una delle opzioni di caricamento rapido. Per altre informazioni sulle modalità di accesso ai dati con caricamento rapido, ottimizzate per gli inserimenti bulk, vedere [Destinazione OLE DB](../../integration-services/data-flow/ole-db-destination.md).  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|Tabella o vista|Consente di caricare i dati in una tabella o vista nella destinazione OLE DB.|  
|Tabella o vista - Caricamento rapido|Consente di caricare i dati in una tabella o vista nella destinazione OLE DB e di utilizzare l'opzione di caricamento rapido. Per altre informazioni sulle modalità di accesso ai dati con caricamento rapido, ottimizzate per gli inserimenti bulk, vedere [Destinazione OLE DB](../../integration-services/data-flow/ole-db-destination.md).|  
|Variabile nome vista o nome tabella|Consente di specificare il nome della vista o della tabella in una variabile.<br /><br /> **Informazioni correlate**: [Uso di variabili nei pacchetti](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)|  
|Variabile nome vista o nome tabella - Caricamento rapido|Consente di specificare il nome della vista o della tabella in una variabile e di caricare i dati utilizzando l'opzione di caricamento rapido. Per altre informazioni sulle modalità di accesso ai dati con caricamento rapido, ottimizzate per gli inserimenti bulk, vedere [Destinazione OLE DB](../../integration-services/data-flow/ole-db-destination.md).|  
|Comando SQL|Consente di caricare i dati nella destinazione OLE DB utilizzando una query SQL.|  
  
 **Anteprima**  
 Consente di visualizzare in anteprima i risultati nella finestra di dialogo **Anteprima risultati query** . L'anteprima supporta la visualizzazione di un massimo di 200 righe.  
  
### <a name="data-access-mode-dynamic-options"></a>Opzioni dinamiche relative alla modalità di accesso ai dati  
 Ogni impostazione di **Modalità di accesso ai dati** consente di visualizzare un set dinamico di opzioni specifico di tale impostazione. Le sezioni seguenti descrivono ogni opzione dinamica disponibile per ogni impostazione **Modalità di accesso ai dati** .  
  
#### <a name="data-access-mode--table-or-view"></a>Modalità di accesso ai dati = Tabella o vista  
 **Nome tabella o vista**  
 Consente di selezionare il nome della tabella o della vista nell'elenco dei nomi disponibili nell'origine dei dati.  
  
 **Nuova**  
 Consente di creare una nuova tabella usando la finestra di dialogo **Crea tabella** .  
  
> [!NOTE]  
>  Quando si fa clic su **Nuova**, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] genera un'istruzione CREATE TABLE predefinita basata sull'origine dati connessa. Questa istruzione CREATE TABLE predefinita non includerà l'attributo FILESTREAM anche se la tabella di origine include una colonna con l'attributo FILESTREAM dichiarato. Per eseguire un componente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con l'attributo FILESTREAM, implementare innanzitutto l'archiviazione di FILESTREAM nel database di destinazione. Aggiungere quindi l'attributo FILESTREAM all'istruzione CREATE TABLE nella finestra di dialogo **Crea tabella**. Per altre informazioni, vedere [Dati BLOB &#40;Binary Large Object&#41; &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
#### <a name="data-access-mode--table-or-view---fast-load"></a>Modalità di accesso ai dati = Tabella o vista - Caricamento rapido  
 **Nome tabella o vista**  
 Consente di selezionare una tabella o vista del database nell'elenco o di creare una nuova tabella facendo clic su **Nuova**.  
  
 **Nuova**  
 Consente di creare una nuova tabella usando la finestra di dialogo **Crea tabella** .  
  
> [!NOTE]  
>  Quando si fa clic su **Nuova**, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] genera un'istruzione CREATE TABLE predefinita basata sull'origine dati connessa. Questa istruzione CREATE TABLE predefinita non includerà l'attributo FILESTREAM anche se la tabella di origine include una colonna con l'attributo FILESTREAM dichiarato. Per eseguire un componente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con l'attributo FILESTREAM, implementare innanzitutto l'archiviazione di FILESTREAM nel database di destinazione. Aggiungere quindi l'attributo FILESTREAM all'istruzione CREATE TABLE nella finestra di dialogo **Crea tabella**. Per altre informazioni, vedere [Dati BLOB &#40;Binary Large Object&#41; &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 **Mantieni valori Identity**  
 Consente di specificare se copiare i valori Identity durante il caricamento dei dati. Questa proprietà è disponibile solo con l'opzione di caricamento rapido. Il valore predefinito della proprietà è **false**.  
  
 **Mantieni valori Null**  
 Consente di specificare che vengano copiati i valori Null durante il caricamento dei dati. Questa proprietà è disponibile solo con l'opzione di caricamento rapido. Il valore predefinito della proprietà è **false**.  
  
 **Blocco a livello di tabella**  
 Consente di specificare che la tabella venga bloccata durante il caricamento. Il valore predefinito di questa proprietà è **true**.  
  
 **Vincoli CHECK**  
 Consente di specificare se la destinazione esegue la verifica dei vincoli durante il caricamento dei dati. Il valore predefinito di questa proprietà è **true**.  
  
 **Righe per batch**  
 Consente di specificare il numero di righe di un batch. Il valore predefinito di questa proprietà è **-1**, che indica che non è stato assegnato alcun valore.  
  
> [!NOTE]  
>  Cancellare il contenuto della casella di testo in **Editor destinazione OLE DB** per indicare che non si intende assegnare alcun valore personalizzato alla proprietà.  
  
 **Dimensioni massime commit inserimento**  
 Consente di specificare le dimensioni del batch per le quali la destinazione OLE DB tenta di eseguire il commit durante le operazioni di caricamento rapido. Il valore **0** indica che viene eseguito il commit di tutti i dati in un singolo batch dopo che tutte le righe sono state elaborate.  
  
> [!NOTE]  
>  Un valore di **0** potrebbe provocare il blocco del pacchetto in esecuzione se la destinazione OLE DB e un altro componente flusso di dati aggiornano la stessa tabella di origine. Per impedire l'arresto del pacchetto, impostare l'opzione **Dimensioni massime commit inserimento** su **2147483647**.  
  
 Se si specifica un valore per questa proprietà, la destinazione esegue il commit delle righe nei batch le cui dimensioni sono inferiori (a) al valore specificato in **Dimensioni massime commit inserimento**o (b) alle righe restanti nel buffer attualmente in fase di elaborazione.  
  
> [!NOTE]  
>  Un eventuale esito negativo della verifica dei vincoli nella destinazione causa l'interruzione dell'intero batch di righe definito da **Dimensioni massime commit inserimento** .  
  
#### <a name="data-access-mode--table-name-or-view-name-variable"></a>Modalità di accesso ai dati = Variabile nome vista o nome tabella  
 **Nome variabile**  
 Consente di selezionare la variabile che contiene il nome della tabella o vista.  
  
#### <a name="data-access-mode--table-name-or-view-name-variable---fast-load"></a>Modalità di accesso ai dati = Variabile nome vista o nome tabella - Caricamento rapido  
 **Nome variabile**  
 Consente di selezionare la variabile che contiene il nome della tabella o vista.  
  
 **Nuova**  
 Consente di creare una nuova tabella usando la finestra di dialogo **Crea tabella** .  
  
> [!NOTE]  
>  Quando si fa clic su **Nuova**, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] genera un'istruzione CREATE TABLE predefinita basata sull'origine dati connessa. Questa istruzione CREATE TABLE predefinita non includerà l'attributo FILESTREAM anche se la tabella di origine include una colonna con l'attributo FILESTREAM dichiarato. Per eseguire un componente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] con l'attributo FILESTREAM, implementare innanzitutto l'archiviazione di FILESTREAM nel database di destinazione. Aggiungere quindi l'attributo FILESTREAM all'istruzione CREATE TABLE nella finestra di dialogo **Crea tabella**. Per altre informazioni, vedere [Dati BLOB &#40;Binary Large Object&#41; &#40;SQL Server&#41;](../../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 **Mantieni valori Identity**  
 Consente di specificare se copiare i valori Identity durante il caricamento dei dati. Questa proprietà è disponibile solo con l'opzione di caricamento rapido. Il valore predefinito della proprietà è **false**.  
  
 **Mantieni valori Null**  
 Consente di specificare che vengano copiati i valori Null durante il caricamento dei dati. Questa proprietà è disponibile solo con l'opzione di caricamento rapido. Il valore predefinito della proprietà è **false**.  
  
 **Blocco a livello di tabella**  
 Consente di specificare che la tabella venga bloccata durante il caricamento. Il valore predefinito della proprietà è **false**.  
  
 **Vincoli CHECK**  
 Consente di specificare se l'attività esegue la verifica dei vincoli. Il valore predefinito della proprietà è **false**.  
  
 **Righe per batch**  
 Consente di specificare il numero di righe di un batch. Il valore predefinito di questa proprietà è **-1**, che indica che non è stato assegnato alcun valore.  
  
> [!NOTE]  
>  Cancellare il contenuto della casella di testo in **Editor destinazione OLE DB** per indicare che non si intende assegnare alcun valore personalizzato alla proprietà.  
  
 **Dimensioni massime commit inserimento**  
 Consente di specificare le dimensioni del batch per le quali la destinazione OLE DB tenta di eseguire il commit durante le operazioni di caricamento rapido. Il valore predefinito di **2147483647** indica che viene eseguito il commit di tutti i dati in un singolo batch dopo che tutte le righe sono state elaborate.  
  
> [!NOTE]  
>  Un valore di **0** potrebbe provocare il blocco del pacchetto in esecuzione se la destinazione OLE DB e un altro componente flusso di dati aggiornano la stessa tabella di origine. Per impedire l'arresto del pacchetto, impostare l'opzione **Dimensioni massime commit inserimento** su **2147483647**.  
  
#### <a name="data-access-mode--sql-command"></a>Modalità di accesso ai dati = Comando SQL  
 **Testo comando SQL**  
 Immettere il testo di una query SQL, fare clic su **Compila query**per compilare la query o fare clic su **Sfoglia**per individuare il file che contiene il testo della query.  
  
> [!NOTE]  
>  La destinazione OLE DB non supporta parametri. Per eseguire un'istruzione INSERT con parametri, è possibile utilizzare la trasformazione Comando OLE DB. Per altre informazioni, vedere [Trasformazione Comando OLE DB](../../integration-services/data-flow/transformations/ole-db-command-transformation.md).  
  
 **Compila query**  
 Usare la finestra di dialogo **Generatore query** per creare la query SQL con strumenti grafici.  
  
 **Sfoglia**  
 Usare la finestra di dialogo **Apri** per individuare il file contenente il testo della query SQL.  
  
 **Analizza query**  
 Consente di verificare la sintassi del testo della query.  
  
## <a name="ole-db-destination-editor-mappings-page"></a>Editor destinazione OLE DB (pagina Mapping)
  Utilizzare la pagina **Mapping** della finestra di dialogo **Editor destinazione OLE DB** per eseguire il mapping tra le colonne di input e quelle di destinazione.  
  
### <a name="options"></a>Opzioni  
 **Colonne di input disponibili**  
 Consente di visualizzare l'elenco delle colonne di input disponibili. Eseguire un'operazione di trascinamento della selezione per impostare il mapping tra le colonne di input disponibili nella tabella e le colonne di destinazione.  
  
 **Colonne di destinazione disponibili**  
 Consente di visualizzare l'elenco delle colonne di destinazione disponibili. Eseguire un'operazione di trascinamento della selezione per impostare il mapping tra le colonne di destinazione disponibili nella tabella e le colonne di input.  
  
 **Colonna di input**  
 Consente di visualizzare le colonne di input selezionate dall'utente. È possibile rimuovere i mapping selezionando **\<ignora>** per escludere colonne dall'output.  
  
 **Colonna di destinazione**  
 Consente di visualizzare ogni colonna di destinazione disponibile, indipendentemente dal fatto che sia mappata o meno.  
  
## <a name="ole-db-destination-editor-error-output-page"></a>Editor destinazione OLE DB (pagina Output degli errori)
  Usare la pagina **Output degli errori** della finestra di dialogo **Editor destinazione OLE DB** per specificare le opzioni di gestione degli errori.  
  
### <a name="options"></a>Opzioni  
 **Input/Output**  
 Consente di visualizzare il nome dell'input.  
  
 **Colonna**  
 Non usato.  
  
 **Errore**  
 Consente di specificare l'azione da eseguire in caso di errori, ovvero ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
 **Argomenti correlati:** [Gestione degli errori nei dati](../../integration-services/data-flow/error-handling-in-data.md)  
  
 **Troncamento**  
 Non usato.  
  
 **Descrizione**  
 Consente di visualizzare la descrizione dell'operazione.  
  
 **Imposta questo valore nelle celle selezionate**  
 Consente di specificare l'azione che dovrà interessare tutte le celle selezionate in caso di errore o troncamento: ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
 **Applica**  
 Consente di applicare l'opzione di gestione degli errori alle celle selezionate.  
  
## <a name="related-content"></a>Contenuto correlato  
 [Origine OLE DB](../../integration-services/data-flow/ole-db-source.md)  
  
 [Variabili di Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md)  
  
 [Flusso di dati](../../integration-services/data-flow/data-flow.md)  
  
  
