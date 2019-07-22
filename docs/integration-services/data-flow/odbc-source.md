---
title: Origine ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.odbcsource.f1
- sql13.ssis.designer.odbcsource.connection.f1
- sql13.ssis.designer.odbcsource.columns.f1
- sql13.ssis.designer.odbcsource.errorhandling.f1
ms.assetid: abcf34eb-9140-4100-82e6-b85bccd22abe
author: janinezhang
ms.author: janinez
ms.openlocfilehash: b1f6f2ae1e1d3043e7f505527599b7035c777cff
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68038765"
---
# <a name="odbc-source"></a>Origine ODBC

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Tramite l'origine ODBC vengono estratti dati da un database supportato da ODBC mediante una tabella di database, una vista o un'istruzione SQL.  
  
 Per l'origine ODBC sono disponibili le modalità di accesso ai dati seguenti per l'estrazione dei dati:  
  
-   Vista o tabella.  
  
-   Risultato di un'istruzione SQL.  
  
 L'origine utilizza una gestione connessione ODBC che specifica il provider da utilizzare.  
  
 Un'origine ODBC include le colonne di output dei dati di origine. Durante il mapping delle colonne di output nella destinazione ODBC alle colonne di destinazione, possono verificarsi errori se non viene eseguito il mapping di alcuna colonna di output alle colonne di destinazione. È possibile eseguire il mapping di colonne di tipi diversi, ma se i dati di output non sono compatibili per la destinazione, si verifica un errore in fase di esecuzione. A seconda del comportamento in seguito all'errore, l'impostazione dell'errore verrà ignorata, provocherà un problema o la riga verrà inviata all'output degli errori.  
  
 L'origine ODBC include un output regolare e un output degli errori.  
  
## <a name="error-handling"></a>Gestione degli errori  
 L'origine ODBC include un output degli errori. L'output degli errori del componente include le colonne di output seguenti:  
  
-   **Error Code** (Codice errore): numero che corrisponde all'errore corrente. Per un elenco degli errori, vedere la documentazione per il database supportato da ODBC in uso. Per un elenco dei codici di errore SSIS, vedere la Guida di riferimento ai messaggi e ai codici di errore SSIS.  
  
-   **Error Column**(Colonna errore): colonna di origine che causa l'errore (per gli errori di conversione).  
  
-   Colonne dei dati di output standard.  
  
 A seconda dell'impostazione del comportamento in seguito all'errore, l'origine ODBC supporta la restituzione degli errori (conversione dei dati, troncamento) che si verificano durante il processo di estrazione nell'output degli errori. Per altre informazioni, vedere [Editor destinazione ODBC &#40;pagina Gestione connessione&#41;](../../integration-services/data-flow/odbc-destination-editor-connection-manager-page.md).  
  
## <a name="data-type-support"></a>Supporto dei tipi di dati  
 Per informazioni sui tipi di dati supportati dall'origine ODBC, vedere Connettore per ODBC (Open Database Connectivity).  
  
## <a name="extract-options"></a>Opzioni di estrazione  
 L'origine ODBC usa la modalità **Batch** o **Row-by-Row** . La modalità utilizzata è determinata dalla proprietà **FetchMethod** . Nell'elenco seguente vengono descritte le diverse modalità.  
  
-   **Batch**: il componente tenta di usare il metodo di recupero più efficiente in base alle funzionalità del provider ODBC rilevate. Per la maggior parte degli attuali provider ODBC, tale metodo è SQLFetchScroll con associazione di matrici (in cui le dimensioni delle matrici sono determinate dalla proprietà **BatchSize** ). Se si seleziona **Batch** e il provider non supporta questo metodo, la destinazione ODBC passa automaticamente alla modalità **Riga per riga** .  
  
-   **Row-by Row** (Riga per riga): il componente usa SQLFetch per recuperare le righe una per volta.  
  
 Per altre informazioni sulla proprietà **FetchMethod** , vedere [Proprietà personalizzate dell'origine ODBC](../../integration-services/data-flow/odbc-source-custom-properties.md).  
  
## <a name="parallelism"></a>Parallelism  
 Non sussiste alcuna limitazione al numero di componenti dell'origine ODBC che possono essere eseguiti in parallelo rispetto alla stessa tabella o a tabelle diverse, nello stesso computer o in computer diversi, ad eccezione dei normali limiti di sessione globali.  
  
 Alcune limitazioni del provider ODBC utilizzato possono tuttavia ridurre il numero di connessioni simultanee tramite il provider. Queste limitazioni riducono il numero di possibili istanze parallele supportate per l'origine ODBC. Lo sviluppatore di SSIS deve essere a conoscenza delle limitazioni di qualsiasi provider ODBC utilizzato e tenerne conto in caso di compilazione di pacchetti SSIS.  
  
## <a name="troubleshooting-the-odbc-source"></a>Risoluzione dei problemi relativi all'origine ODBC  
 È possibile registrare le chiamate eseguite dall'origine ODBC a provider di dati esterni. Questa funzionalità di registrazione può essere utilizzata per risolvere i problemi relativi al caricamento di dati da origini dati esterne eseguito dall'origine ODBC. Per registrare le chiamate eseguite dall'origine ODBC a provider di dati esterni, abilitare la traccia di Gestione driver ODBC. Per altre informazioni, vedere la documentazione di Microsoft su *come generare una traccia ODBC con l'amministratore dell'origine dati ODBC*.  
  
## <a name="configuring-the-odbc-source"></a>Configurazione dell'origine ODBC  
 È possibile configurare l'origine ODBC a livello di codice o tramite Progettazione SSIS.  
  
 La finestra di dialogo **Editor avanzato** contiene le proprietà che è possibile impostare a livello di codice.  
  
 Per aprire la finestra di dialogo **Editor avanzato** :  
  
-   Nella schermata **Flusso di dati** del progetto di [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] fare clic con il pulsante destro del mouse sull'origine ODBC e scegliere **Visualizza editor avanzato**.  
  
 Per altre informazioni sulle proprietà che è possibile impostare nella finestra di dialogo Editor avanzato, vedere [Proprietà personalizzate dell'origine ODBC](../../integration-services/data-flow/odbc-source-custom-properties.md).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Estrarre dati tramite l'origine ODBC](../../integration-services/data-flow/extract-data-by-using-the-odbc-source.md)  
  
-   [Proprietà personalizzate dell'origine ODBC](../../integration-services/data-flow/odbc-source-custom-properties.md)  
  
## <a name="odbc-source-editor-connection-manager-page"></a>Editor origine ODBC (pagina Gestione connessione)
  Utilizzare la pagina **Gestione connessione** della finestra di dialogo **ODBC Source Editor** per selezionare la gestione connessione ODBC per l'origine. Tramite questa pagina è inoltre possibile selezionare una tabella o una vista del database.  
  
### <a name="task-list"></a>Elenco attività  
 **Per aprire ODBC Source Editor (pagina Gestione connessione)**  
  
-   In [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], aprire il pacchetto [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] che contiene l'origine ODBC.  
  
-   Nella scheda **Flusso di dati** fare doppio clic sull'origine ODBC.  
  
### <a name="options"></a>Opzioni  
  
#### <a name="connection-manager"></a>Gestione connessione  
 Consente di selezionare una gestione connessione ODBC esistente nell'elenco o di creare una nuova connessione facendo clic su **Nuova** . La connessione può essere a qualsiasi database supportato da ODBC.  
  
#### <a name="new"></a>Nuovo  
 Fare clic su **Nuovo**. Viene visualizzata la finestra di dialogo **Configura gestione connessione ODBC** in cui è possibile creare una nuova gestione connessione ODBC.  
  
#### <a name="data-access-mode"></a>Modalità di accesso ai dati  
 Consente di selezionare il metodo per la selezione dei dati dall'origine. Le opzioni disponibili vengono visualizzate nella tabella seguente.  
  
|Opzione|Descrizione|  
|------------|-----------------|  
|Nome tabella|Consente di recuperare dati da una tabella o da una vista nell'origine dati ODBC. Se si seleziona questa opzione, scegliere un valore nell'elenco per le opzioni seguenti:|  
||**Nome tabella o vista**: selezionare una tabella o vista disponibile nell'elenco o digitare un'espressione regolare per identificare la tabella.|  
||Questo elenco contiene solo le prime 1000 tabelle. Se il database contiene più di 1000 tabelle, è possibile digitare l'inizio di un nome di tabella o utilizzare il carattere jolly (*) per immettere qualsiasi parte del nome e visualizzare la tabella o le tabelle che si desidera utilizzare.|  
|Comando SQL|Consente di recuperare dati dall'origine dati ODBC utilizzando una query SQL. Scrivere la query nella sintassi del database di origine che si sta utilizzando. Se si seleziona questa opzione, immettere una query in uno dei modi seguenti:|  
||Immettere il testo della query SQL nel campo **Testo comando SQL** .|  
||Fare clic su **Sfoglia** per caricare la query SQL da un file di testo.|  
||Fare clic su **Analizza query** per verificare la sintassi del testo della query.|  
  
#### <a name="preview"></a>Anteprima  
 Fare clic su **Anteprima** per visualizzare un massimo di 200 righe dei dati estratti dalla tabella o dalla vista selezionata.  
  
## <a name="odbc-source-editor-columns-page"></a>Editor origine ODBC (pagina Colonne)
  Usare la pagina **Colonne** della finestra di dialogo **Editor origine ODBC** per eseguire il mapping tra una colonna di output e ogni colonna esterna (di origine).  
  
### <a name="task-list"></a>Elenco attività  
 **Per aprire ODBC Source Editor (pagina Colonne)**  
  
1.  In [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], aprire il pacchetto [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] che contiene l'origine ODBC.  
  
2.  Nella scheda **Flusso di dati** fare doppio clic sull'origine ODBC.  
  
3.  In **ODBC Source Editor**, fare clic su **Colonne**.  
  
### <a name="options"></a>Opzioni  
  
#### <a name="available-external-columns"></a>Colonne esterne disponibili  
 Elenco delle colonne esterne disponibili nell'origine dei dati. Non è possibile utilizzare questa tabella per l'aggiunta o l'eliminazione di colonne. Selezionare le colonne da utilizzare dall'origine. Le colonne scelte vengono aggiunte all'elenco **Colonna esterna** nell'ordine in cui vengono selezionate.  
  
 Selezionare la casella di controllo **Seleziona tutto** per selezionare tutte le colonne.  
  
#### <a name="external-column"></a>Colonna esterna  
 Una vista delle colonne esterne (di origine) nell'ordine in cui vengono presentate durante la configurazione di componenti che utilizzano i dati dell'origine ODBC.  
  
#### <a name="output-column"></a>Colonna di output  
 Consente di immettere un nome univoco per ogni colonna di output. Per impostazione predefinita viene suggerito il nome della colonna esterna (di origine) selezionata. È comunque possibile scegliere qualsiasi nome descrittivo univoco. Il nome immesso viene visualizzato in Progettazione SSIS.  
  
## <a name="odbc-source-editor-error-output-page"></a>Editor origine ODBC (pagina Output degli errori)
  Usare la pagina **Output degli errori** della finestra di dialogo **ODBC Source Editor** (Editor origine ODBC) per selezionare le opzioni di gestione degli errori.  
  
### <a name="task-list"></a>Elenco attività  
 **Per aprire ODBC Source Editor (pagina Output degli errori)**  
  
-   In [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], aprire il pacchetto [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] che contiene l'origine ODBC.  
  
-   Nella scheda **Flusso di dati** fare doppio clic sull'origine ODBC.  
  
-   In **ODBC Source Editor**(Editor origine ODBC) fare clic su **Output degli errori**.  
  
### <a name="options"></a>Opzioni  
  
#### <a name="inputoutput"></a>Input/Output  
 Consente di visualizzare il nome dell'origine dei dati.  
  
#### <a name="column"></a>colonna  
 Non usato.  
  
#### <a name="error"></a>Errore  
 Consente di selezionare il modo in cui l'origine ODBC deve gestire gli errori in un flusso: ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
#### <a name="truncation"></a>Troncamento  
 Consente di selezionare il modo in cui l'origine ODBC deve gestire il troncamento in un flusso: ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
#### <a name="description"></a>Descrizione  
 Non usato.  
  
#### <a name="set-this-value-to-selected-cells"></a>Imposta questo valore nelle celle selezionate  
 Consente di selezionare il modo in cui l'origine ODBC gestisce tutte le celle selezionate in caso di errore o troncamento: ignorare l'errore, reindirizzare la riga o interrompere il componente.  
  
#### <a name="apply"></a>Applica  
 Consente di applicare le opzioni di gestione degli errori alle celle selezionate.  
  
### <a name="error-handling-options"></a>Opzioni di gestione degli errori  
 Utilizzare le opzioni seguenti per configurare il modo in cui l'origine ODBC gestisce errori e troncamenti.  
  
#### <a name="fail-component"></a>Interrompi componente  
 Quando si verifica un errore o un troncamento l'attività Flusso di dati viene interrotta. Questo è il comportamento predefinito.  
  
#### <a name="ignore-failure"></a>Ignora errore  
 L'errore o il troncamento vengono ignorati.  
  
#### <a name="redirect-flow"></a>Reindirizza flusso  
 La riga che determina l'errore o il troncamento viene inviata all'output degli errori dell'origine ODBC.  
  
  
