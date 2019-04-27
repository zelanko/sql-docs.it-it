---
title: Editor destinazione OLE DB (pagina Gestione connessione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.oledbdestadapter.connection.f1
helpviewer_keywords:
- OLE DB Destination Editor
ms.assetid: ae2200c6-8ba0-49b7-b01a-53425b84d2ed
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 986813601be89e201978e50b76085752e4f34356
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62767153"
---
# <a name="ole-db-destination-editor-connection-manager-page"></a>Editor destinazione OLE DB (pagina Gestione connessione)
  Usare la pagina **Gestione connessione** della finestra di dialogo **Editor destinazione OLE DB** per selezionare la connessione OLE DB per la destinazione. Tramite questa pagina è inoltre possibile selezionare una tabella o una vista del database.  
  
> [!NOTE]  
>  Il `CommandTimeout` proprietà della destinazione OLE DB non è disponibile nel **Editor destinazione OLE DB**, ma può essere impostata utilizzando la **Editor avanzato**. Inoltre alcune opzioni di caricamento rapido sono disponibili solo nell' **Editor avanzato**. Per altre informazioni su queste proprietà, vedere la sezione relativa alla destinazione OLE DB in [Proprietà personalizzate OLE DB](data-flow/ole-db-custom-properties.md).  
  
 Per ulteriori informazioni sulla destinazione OLE DB, vedere [OLE DB Destination](data-flow/ole-db-destination.md).  
  
## <a name="static-options"></a>Opzioni statiche  
 **Gestione connessione OLE DB**  
 Selezionare una gestione connessione esistente nell'elenco o crearne una nuova facendo clic su **Nuova**.  
  
 **Nuova**  
 Consente di creare una nuova gestione connessione usando la finestra di dialogo **Configura gestione connessione OLE DB** .  
  
 **Modalità di accesso ai dati**  
 Consente di specificare il metodo di caricamento dei dati nella destinazione. Per i dati DBCS (Double-Byte Character Set) è necessario utilizzare una delle opzioni di caricamento rapido. Per altre informazioni sulle modalità di accesso ai dati con caricamento rapido, ottimizzate per gli inserimenti bulk, vedere [Destinazione OLE DB](data-flow/ole-db-destination.md).  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|Tabella o vista|Consente di caricare i dati in una tabella o vista nella destinazione OLE DB.|  
|Tabella o vista - Caricamento rapido|Consente di caricare i dati in una tabella o vista nella destinazione OLE DB e di utilizzare l'opzione di caricamento rapido. Per altre informazioni sulle modalità di accesso ai dati con caricamento rapido, ottimizzate per gli inserimenti bulk, vedere [Destinazione OLE DB](data-flow/ole-db-destination.md).|  
|Variabile nome vista o nome tabella|Consente di specificare il nome della vista o della tabella in una variabile.<br /><br /> **Informazioni correlate**: [Uso di variabili nei pacchetti](../../2014/integration-services/use-variables-in-packages.md)|  
|Variabile nome vista o nome tabella - Caricamento rapido|Consente di specificare il nome della vista o della tabella in una variabile e di caricare i dati utilizzando l'opzione di caricamento rapido. Per altre informazioni sulle modalità di accesso ai dati con caricamento rapido, ottimizzate per gli inserimenti bulk, vedere [Destinazione OLE DB](data-flow/ole-db-destination.md).|  
|Comando SQL|Consente di caricare i dati nella destinazione OLE DB utilizzando una query SQL.|  
  
 **Anteprima**  
 Consente di visualizzare in anteprima i risultati nella finestra di dialogo **Anteprima risultati query** . L'anteprima supporta la visualizzazione di un massimo di 200 righe.  
  
## <a name="data-access-mode-dynamic-options"></a>Opzioni dinamiche relative alla modalità di accesso ai dati  
 Ogni impostazione di **Modalità di accesso ai dati** consente di visualizzare un set dinamico di opzioni specifico di tale impostazione. Le sezioni seguenti descrivono ogni opzione dinamica disponibile per ogni impostazione **Modalità di accesso ai dati** .  
  
### <a name="data-access-mode--table-or-view"></a>Modalità di accesso ai dati = Tabella o vista  
 **Nome tabella o vista**  
 Consente di selezionare il nome della tabella o della vista nell'elenco dei nomi disponibili nell'origine dei dati.  
  
 **Nuova**  
 Consente di creare una nuova tabella usando la finestra di dialogo **Crea tabella** .  
  
> [!NOTE]  
>  Quando si fa clic su **Nuova**, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] genera un'istruzione CREATE TABLE predefinita basata sull'origine dati connessa. Questa istruzione CREATE TABLE predefinita non includerà l'attributo FILESTREAM anche se la tabella di origine include una colonna con l'attributo FILESTREAM dichiarato. Per eseguire un componente [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] con l'attributo FILESTREAM, implementare innanzitutto l'archiviazione di FILESTREAM nel database di destinazione. Aggiungere quindi l'attributo FILESTREAM all'istruzione CREATE TABLE nella finestra di dialogo **Crea tabella**. Per altre informazioni, vedere [Dati BLOB &#40;Binary Large Object&#41; &#40;SQL Server&#41;](../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
### <a name="data-access-mode--table-or-view---fast-load"></a>Modalità di accesso ai dati = Tabella o vista - Caricamento rapido  
 **Nome tabella o vista**  
 Consente di selezionare una tabella o vista del database nell'elenco o di creare una nuova tabella facendo clic su **Nuova**.  
  
 **Nuova**  
 Consente di creare una nuova tabella usando la finestra di dialogo **Crea tabella** .  
  
> [!NOTE]  
>  Quando si fa clic su **Nuova**, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] genera un'istruzione CREATE TABLE predefinita basata sull'origine dati connessa. Questa istruzione CREATE TABLE predefinita non includerà l'attributo FILESTREAM anche se la tabella di origine include una colonna con l'attributo FILESTREAM dichiarato. Per eseguire un componente [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] con l'attributo FILESTREAM, implementare innanzitutto l'archiviazione di FILESTREAM nel database di destinazione. Aggiungere quindi l'attributo FILESTREAM all'istruzione CREATE TABLE nella finestra di dialogo **Crea tabella**. Per altre informazioni, vedere [Dati BLOB &#40;Binary Large Object&#41; &#40;SQL Server&#41;](../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 **Mantieni valori Identity**  
 Consente di specificare se copiare i valori Identity durante il caricamento dei dati. Questa proprietà è disponibile solo con l'opzione di caricamento rapido. Il valore predefinito di questa proprietà è `false`.  
  
 **Mantieni valori Null**  
 Consente di specificare che vengano copiati i valori Null durante il caricamento dei dati. Questa proprietà è disponibile solo con l'opzione di caricamento rapido. Il valore predefinito di questa proprietà è `false`.  
  
 **Blocco a livello di tabella**  
 Consente di specificare che la tabella venga bloccata durante il caricamento. Il valore predefinito di questa proprietà è `true`.  
  
 **Vincoli CHECK**  
 Consente di specificare se la destinazione esegue la verifica dei vincoli durante il caricamento dei dati. Il valore predefinito di questa proprietà è `true`.  
  
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
  
### <a name="data-access-mode--table-name-or-view-name-variable"></a>Modalità di accesso ai dati = Variabile nome vista o nome tabella  
 **Nome variabile**  
 Consente di selezionare la variabile che contiene il nome della tabella o vista.  
  
### <a name="data-access-mode--table-name-or-view-name-variable---fast-load"></a>Modalità di accesso ai dati = Variabile nome vista o nome tabella - Caricamento rapido  
 **Nome variabile**  
 Consente di selezionare la variabile che contiene il nome della tabella o vista.  
  
 **Nuova**  
 Consente di creare una nuova tabella usando la finestra di dialogo **Crea tabella** .  
  
> [!NOTE]  
>  Quando si fa clic su **Nuova**, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] genera un'istruzione CREATE TABLE predefinita basata sull'origine dati connessa. Questa istruzione CREATE TABLE predefinita non includerà l'attributo FILESTREAM anche se la tabella di origine include una colonna con l'attributo FILESTREAM dichiarato. Per eseguire un componente [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] con l'attributo FILESTREAM, implementare innanzitutto l'archiviazione di FILESTREAM nel database di destinazione. Aggiungere quindi l'attributo FILESTREAM all'istruzione CREATE TABLE nella finestra di dialogo **Crea tabella**. Per altre informazioni, vedere [Dati BLOB &#40;Binary Large Object&#41; &#40;SQL Server&#41;](../relational-databases/blob/binary-large-object-blob-data-sql-server.md).  
  
 **Mantieni valori Identity**  
 Consente di specificare se copiare i valori Identity durante il caricamento dei dati. Questa proprietà è disponibile solo con l'opzione di caricamento rapido. Il valore predefinito di questa proprietà è `false`.  
  
 **Mantieni valori Null**  
 Consente di specificare che vengano copiati i valori Null durante il caricamento dei dati. Questa proprietà è disponibile solo con l'opzione di caricamento rapido. Il valore predefinito di questa proprietà è `false`.  
  
 **Blocco a livello di tabella**  
 Consente di specificare che la tabella venga bloccata durante il caricamento. Il valore predefinito di questa proprietà è `false`.  
  
 **Vincoli CHECK**  
 Consente di specificare se l'attività esegue la verifica dei vincoli. Il valore predefinito di questa proprietà è `false`.  
  
 **Righe per batch**  
 Consente di specificare il numero di righe di un batch. Il valore predefinito di questa proprietà è **-1**, che indica che non è stato assegnato alcun valore.  
  
> [!NOTE]  
>  Cancellare il contenuto della casella di testo in **Editor destinazione OLE DB** per indicare che non si intende assegnare alcun valore personalizzato alla proprietà.  
  
 **Dimensioni massime commit inserimento**  
 Consente di specificare le dimensioni del batch per le quali la destinazione OLE DB tenta di eseguire il commit durante le operazioni di caricamento rapido. Il valore predefinito di **2147483647** indica che viene eseguito il commit di tutti i dati in un singolo batch dopo che tutte le righe sono state elaborate.  
  
> [!NOTE]  
>  Un valore di **0** potrebbe provocare il blocco del pacchetto in esecuzione se la destinazione OLE DB e un altro componente flusso di dati aggiornano la stessa tabella di origine. Per impedire l'arresto del pacchetto, impostare l'opzione **Dimensioni massime commit inserimento** su **2147483647**.  
  
### <a name="data-access-mode--sql-command"></a>Modalità di accesso ai dati = Comando SQL  
 **Testo comando SQL**  
 Immettere il testo di una query SQL, fare clic su **Compila query**per compilare la query o fare clic su **Sfoglia**per individuare il file che contiene il testo della query.  
  
> [!NOTE]  
>  La destinazione OLE DB non supporta parametri. Per eseguire un'istruzione INSERT con parametri, è possibile utilizzare la trasformazione Comando OLE DB. Per altre informazioni, vedere [Trasformazione Comando OLE DB](data-flow/transformations/ole-db-command-transformation.md).  
  
 **Compila query**  
 Usare la finestra di dialogo **Generatore query** per creare la query SQL con strumenti grafici.  
  
 **Sfoglia**  
 Usare la finestra di dialogo **Apri** per individuare il file contenente il testo della query SQL.  
  
 **Analizza query**  
 Consente di verificare la sintassi del testo della query.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento ai messaggi e agli errori di Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor destinazione OLE DB &#40;pagina Mapping&#41;](../../2014/integration-services/ole-db-destination-editor-mappings-page.md)   
 [Editor destinazione OLE DB &#40;pagina Output degli errori&#41;](../../2014/integration-services/ole-db-destination-editor-error-output-page.md)   
 [Caricamento dei dati tramite la destinazione OLE DB](data-flow/load-data-by-using-the-ole-db-destination.md)  
  
  
