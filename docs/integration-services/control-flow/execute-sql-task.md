---
description: Attività Esegui SQL
title: Attività Esegui SQL
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.executesqltask.f1
- sql13.dts.designer.executesqltask.general.f1
- sql13.dts.designer.executesqltask.parametermapping.f1
- sql13.dts.designer.executesqltask.resultset.f1
helpviewer_keywords:
- Transact-SQL statements, SSIS
- statements [Integration Services]
- batches [Integration Services]
- Execute SQL task [Integration Services]
ms.assetid: bebb2e8c-0410-43b2-ac2f-6fc80c8f2e9e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0b8155db361eeffd3b84ba1aadf313ecef4652e9
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/19/2020
ms.locfileid: "92196541"
---
# <a name="execute-sql-task"></a>Attività Esegui SQL

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]

  L'attività Esegui SQL consente di eseguire istruzioni SQL o stored procedure da un pacchetto. L'attività può includere una o più istruzioni SQL che vengono eseguite in ordine sequenziale. È possibile utilizzare l'attività Esegui SQL per gli scopi seguenti:  
  
-   Troncare una tabella o una vista per prepararla per l'inserimento di dati.  
  
-   Creare, modificare ed eliminare oggetti di database come tabelle e viste.  
  
-   Ricreare tabelle dei fatti e delle dimensioni prima di caricarvi i dati.  
  
-   Eseguire stored procedure. Se l'istruzione SQL richiama una stored procedure che restituisce risultati da una tabella temporanea, utilizzare l'opzione WITH RESULT SETS per definire metadati per il set di risultati.  
  
-   Salvare in una variabile il set di righe restituito da una query.  
  
 L'attività Esegui SQL può essere usata in combinazione con i contenitori Ciclo Foreach e Ciclo For per eseguire più istruzioni SQL. Questi contenitori consentono di implementare flussi di controllo ripetuti in un pacchetto e possono eseguire più volte l'attività Esegui SQL. Utilizzando ad esempio il contenitore Ciclo Foreach, il pacchetto può enumerare i file in una cartella ed eseguire ripetutamente un'attività Esegui SQL per elaborare l'istruzione SQL archiviata in ogni file.  
  
## <a name="connect-to-a-data-source"></a>Connettersi a un'origine dati  
 Per connettersi all'origine dei dati su cui eseguire l'istruzione SQL o la stored procedure, l'attività Esegui SQL può utilizzare diversi tipi di gestione connessione, elencati nella tabella seguente.  
  
|Tipo di connessione|Gestione connessione|  
|---------------------|------------------------|  
|EXCEL|[Gestione connessione Excel](../../integration-services/connection-manager/excel-connection-manager.md)|  
|OLE DB|[Gestione connessione OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md)|  
|ODBC|[Gestione connessione ODBC](../../integration-services/connection-manager/odbc-connection-manager.md)|  
|ADO|[Gestione connessione ADO](../../integration-services/connection-manager/ado-connection-manager.md)|  
|ADO.NET|[Gestione connessione ADO.NET](../../integration-services/connection-manager/ado-net-connection-manager.md)|  
|SQLMOBILE|[Gestione connessione SQL Server Compact Edition](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|  
  
## <a name="create-sql-statements"></a>Creare istruzioni SQL  
 L'origine delle istruzioni SQL utilizzate da questa attività può essere una proprietà dell'attività che contiene un'istruzione, una connessione a un file che contiene una o più istruzioni oppure il nome di una variabile che contiene un'istruzione. Le istruzioni SQL devono essere scritte nel sottolinguaggio del sistema di gestione di database (DBMS) di origine. Per altre informazioni, vedere [Query di Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-queries.md).  
  
 Se le istruzioni SQL sono memorizzate in un file, per connettersi al file l'attività utilizzerà una gestione connessione file. Per altre informazioni, vedere [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md).  
  
 In Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] per creare query SQL è possibile digitare le istruzioni nella finestra di dialogo **Editor attività Esegui SQL** o utilizzare l'interfaccia utente grafica **Generatore di query**. 
  
> [!NOTE]  
>  L'attività Esegui SQL non è in grado di elaborare correttamente le istruzioni SQL valide scritte al di fuori dell'attività stessa.  
  
> [!NOTE]  
>  L'attività Esegui SQL usa il valore di enumerazione ParseMode **RecognizedAll** . Per altre informazioni, vedere [Spazio dei nomi ManagedBatchParser](/dotnet/api/managedbatchparser).  
  
## <a name="send-multiple-statements-in-a-batch"></a>Inviare più istruzioni in un batch  
 Se un'attività Esegui SQL include più istruzioni, sarà possibile raggrupparle ed eseguirle come batch, utilizzando il comando GO per segnalare la fine del batch. Tutte le istruzioni SQL comprese tra due comandi GO vengono inviate in batch al provider OLE DB per l'esecuzione. Il comando SQL può includere più batch separati da comandi GO.  
  
 I tipi di istruzioni SQL che è possibile raggruppare in un batch sono soggetti a restrizioni. Per altre informazioni, vedere [Batch di istruzioni](../../relational-databases/native-client-odbc-queries/executing-statements/batches-of-statements.md).  
  
 Se l'attività Esegui SQL esegue un batch di istruzioni SQL, al batch verranno applicate le regole seguenti:  
  
-   Può restituire un set di risultati una sola istruzione, che deve essere la prima del batch.  
  
-   Se il set di risultati utilizza associazioni di risultati, le query dovranno restituire lo stesso numero di colonne. Se le query restituiscono numeri di colonne diversi, l'attività avrà esito negativo. Le query eseguite dall'attività, ad esempio DELETE o INSERT, possono tuttavia avere esito positivo anche se l'attività non viene eseguita correttamente.  
  
-   Se le associazioni di risultati utilizzano nomi di colonne, la query dovrà restituire colonne con nomi uguali a quelli del set di risultati dell'attività. Se le colonne non sono presenti, l'attività avrà esito negativo.  
  
-   Se l'attività utilizza un'associazione di parametri, tutte le query incluse nel batch dovranno avere lo stesso numero e gli stessi tipi di parametri.  
  
## <a name="run-parameterized-sql-commands"></a>Eseguire comandi SQL con parametri  
 Le istruzioni SQL e le stored procedure utilizzano spesso parametri di input, parametri di output e codici restituiti. L'attività Esegui SQL supporta parametri di tipo **Input**, **Output**e **ReturnValue** . Il tipo **Input** viene usato per i parametri di input, il tipo **Output** per i parametri di output e il tipo **ReturnValue** per i codici restituiti.  
  
> [!NOTE]  
>  È possibile utilizzare parametri in un'attività Esegui SQL solo se il provider di dati li supporta.  
  
## <a name="specify-a-result-set-type"></a>Specificare un tipo di set di risultati  
 A seconda del tipo di comando SQL, all'attività Esegui SQL può essere restituito o meno un set di risultati. Se si utilizzano ad esempio le istruzioni SELECT, viene in genere restituito un set di risultati, mentre questo non avviene per le istruzioni INSERT. Il set di risultati restituito da un'istruzione SELECT può contenere zero, una o più righe. Le stored procedure possono restituire anche un valore intero, detto codice restituito, che indica lo stato dell'esecuzione della procedura. In questo caso il set di risultati è costituito da una sola riga.  
  
## <a name="configure-the-execute-sql-task"></a>Configurare l'attività Esegui SQL  
 Per configurare l'attività Esegui SQL, procedere nel modo seguente:  
  
-   Specificare il tipo di gestione connessione da utilizzare per la connessione a un database.  
  
-   Specificare il tipo di set di risultati restituito dall'istruzione SQL.  
  
-   Specificare un timeout per l'istruzione SQL.  
  
-   Specificare l'origine dell'istruzione SQL.  
  
-   Indicare se l'attività salta la fase di preparazione per l'istruzione SQL.  
  
-   Se si utilizza il tipo di connessione ADO, è necessario indicare se l'istruzione SQL è una stored procedure. Per altri tipi di connessione questa proprietà è di sola lettura e ha sempre valore **false**.  
  
 È possibile impostare le proprietà a livello di programmazione o tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  

## <a name="general-page---execute-sql-task-editor"></a>Pagina Generale - Editor attività Esegui SQL
 Usare la pagina **Generale** della finestra di dialogo **Editor attività Esegui SQL** per configurare l'attività Esegui SQL e specificare l'istruzione SQL eseguita dall'attività.  

Per sapere di più sul linguaggio di query Transact-SQL, vedere [Guida di riferimento a Transact-SQL &#40;Motore di database&#41;](../../t-sql/language-reference.md).  
  
### <a name="static-options"></a>Opzioni statiche  
 **Nome**  
 Consente di specificare un nome univoco per l'attività Esegui SQL nel flusso di lavoro. Il nome specificato verrà visualizzato in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Descrizione**  
 Consente di immettere una descrizione per l'attività Esegui SQL. È consigliabile includere nella descrizione informazioni sugli scopi dell'attività, in modo da ottenere pacchetti autodocumentati e semplificarne quindi la gestione.  
  
 **TimeOut**  
 Consente di specificare il numero massimo di secondi per cui l'attività verrà eseguita prima del timeout. Il valore 0 corrisponde a un intervallo infinito. Il valore predefinito è 0.  
  
> [!NOTE]  
>  Il timeout delle stored procedure non si verifica se queste emulano la funzionalità di sospensione specificando un periodo di tempo per la creazione di connessioni e il completamento di transazioni maggiore rispetto al numero di secondi indicato da **TimeOut**. Le stored procedure che eseguono query sono comunque soggette alle restrizioni di tempo specificate da **TimeOut**.  
  
 **CodePage**  
 Consente di specificare la tabella codici da utilizzare durante la conversione di valori Unicode in variabili. Il valore predefinito corrisponde alla tabella codici del computer locale.  
  
> [!NOTE]  
>  Quando l'attività Esegui SQL usa una gestione connessione ADO o ODBC, la proprietà **CodePage** non è disponibile. Se la soluzione richiede l'utilizzo di una tabella codici, utilizzare una gestione connessione OLE DB o ADO.NET con l'attività Esegui SQL.  
  
 **TypeConversionMode**  
 Se si imposta questa proprietà su **Allowed**, l'attività Esegui SQL tenterà di convertire il parametro di output e i risultati della query nel tipo di dati della variabile a cui sono assegnati i risultati. Si applica al tipo di set di risultati **Riga singola** .  
  
 **ResultSet**  
 Consente di specificare il tipo di risultati previsto per un'istruzione SQL in fase di esecuzione. È possibile scegliere tra **Riga singola**, **Set dei risultati completo**, **XML**o **Nessuno**.  
  
 **ConnectionType**  
 Consente di scegliere il tipo di gestione connessione da utilizzare per la connessione a un'origine dati. I tipi di connessione disponibili includono **OLE DB**, **ODBC**, **ADO**, **ADO.NET** e **SQLMOBILE**.  
  
 **Argomenti correlati:** [Gestione connessione OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md), [Gestione connessione ODBC](../../integration-services/connection-manager/odbc-connection-manager.md), [Gestione connessione ADO](../../integration-services/connection-manager/ado-connection-manager.md), [Gestione connessione ADO.NET](../../integration-services/connection-manager/ado-net-connection-manager.md), [Gestione connessione SQL Server Compact Edition](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)  
  
 **Connection**  
 Consente di scegliere una connessione da un elenco di gestioni connessione definite. Per creare una nuova connessione, selezionare \<**New connection...**>.  
  
 **SQLSourceType**  
 Consente di selezionare il tipo di origine dell'istruzione SQL eseguita dall'attività.  
  
 A seconda del tipo di gestione connessione utilizzato dall'attività Esegui SQL, è necessario utilizzare indicatori di parametro specifici nelle istruzioni SQL con parametri.    
  
 Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Input diretto**|Consente di impostare l'origine su un'istruzione Transact-SQL. Selezionando questo valore, verrà visualizzata l'opzione dinamica **SQLStatement**.|  
|**Connessione file**|Consente di selezionare un file contenente un'istruzione Transact-SQL. Impostando questa opzione, verrà visualizzata l'opzione dinamica **FileConnection**.|  
|**Variabile**|Consente di impostare l'origine su una variabile che definisce l'istruzione Transact-SQL. Se si seleziona questo valore, viene visualizzata l'opzione dinamica **SourceVariable**.|  
  
 **QueryIsStoredProcedure**  
 Indica se l'istruzione SQL specificata da eseguire è una stored procedure. Questa proprietà è di lettura/scrittura solo se l'attività utilizza una gestione connessione ADO. Altrimenti, la proprietà è di sola lettura e il relativo valore è **false**.  
  
 **BypassPrepare**  
 Indica se l'istruzione SQL è stata preparata.  Il valore**true** ignora la preparazione, il valore **false** prepara l'istruzione SQL prima dell'esecuzione. Questa opzione è disponibile solo con le connessioni OLE DB che supportano la preparazione.  
  
 **Argomenti correlati:**  [Esecuzione preparata](../../relational-databases/native-client-odbc-queries/executing-statements/prepared-execution.md)  
  
 **Sfoglia**  
 Individuare un file contenente un'istruzione SQL tramite la finestra di dialogo **Apri** . Selezionare un file per copiarne il contenuto sotto forma di istruzione SQL nella proprietà **SQLStatement** .  
  
 **Compila query**  
 Consente di creare un'istruzione SQL tramite la finestra di dialogo **Generatore query** , uno strumento grafico usato per la creazione di query. Questa opzione è disponibile quando l'opzione **SQLSourceType** è impostata su **Input diretto**.  
  
 **Analizza query**  
 Consente di convalidare la sintassi dell'istruzione SQL.  
  
### <a name="sqlsourcetype-dynamic-options"></a>Opzioni dinamiche SQLSourceType  
  
#### <a name="sqlsourcetype--direct-input"></a>SQLSourceType = Input diretto  
 **SQLStatement**  
 Digitare l'istruzione SQL da eseguire nella casella di opzione oppure fare clic sul pulsante (...) per digitare l'istruzione SQL nella finestra di dialogo **Immetti query SQL** o fare clic su **Compila query** per comporre l'istruzione con la finestra di dialogo **Generatore di query**.  
  
 **Argomenti correlati:** [Generatore di query](../integration-services-ssis-queries.md)  
  
#### <a name="sqlsourcetype--file-connection"></a>SQLSourceType = Connessione file  
 **FileConnection**  
 Selezionare una gestione connessione file nell'elenco oppure fare clic su \<**New connection...**> per creare una nuova gestione connessione.  
  
 **Argomenti correlati:** [Gestione connessione file](../../integration-services/connection-manager/file-connection-manager.md), [Editor gestione connessione file](../connection-manager/file-connection-manager.md)  
  
#### <a name="sqlsourcetype--variable"></a>SQLSourceType = Variabile  
 **SourceVariable**  
 Selezionare una variabile esistente oppure fare clic su \<**New variable...**> per creare una nuova variabile.  
  
 **Argomenti correlati:** [Variabili di Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Aggiungere una variabile](../integration-services-ssis-variables.md)  
 
## <a name="parameter-mapping-page---execute-sql-task-editor"></a>Pagina Mapping parametri - Editor attività Esegui SQL
Usare la pagina **Mapping parametri** della finestra di dialogo **Editor attività Esegui SQL** per eseguire il mapping tra variabili e parametri nell'istruzione SQL.  
  
### <a name="options"></a>Opzioni  
 **Nome variabile**  
 Dopo aver aggiunto un mapping dei parametri facendo clic su **Aggiungi**, selezionare una variabile di sistema o una variabile definita dall'utente nell'elenco oppure fare clic su \<**New variable...**> per aggiungere una nuova variabile usando la finestra di dialogo **Aggiungi variabile**.  
  
 **Argomenti correlati:** [Variabili di Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md)  
  
 **Direzione**  
 Consente di selezionare la direzione del parametro. Eseguire il mapping di ogni variabile a un parametro di input, a un parametro di output o a un codice restituito.  
  
 **Tipo di dati**  
 Selezionare il tipo di dati del parametro. L'elenco dei tipi di dati disponibili è specifico del provider selezionato per la gestione connessione utilizzata dall'attività.  
  
 **Nome parametro**  
 Consente di specificare un nome per il parametro.  
  
 A seconda del tipo di gestione connessione utilizzata dall'attività, è necessario specificare numeri o nomi di parametri. Alcuni tipi di gestioni delle connessioni prevedono che il primo carattere del nome del parametro sia il segno \@, nomi specifici come \@Param1 oppure nomi di colonna come nomi di parametri.  
  
 **Dimensioni parametro**  
 Fornisce le dimensioni dei parametri a lunghezza variabile, ad esempio stringhe e campi binario.  
  
 Tale impostazione assicura che il provider allochi spazio sufficiente per i valori dei parametri a lunghezza variabile.  
  
 **Aggiungere**  
 Fare clic su questo pulsante per aggiungere un mapping dei parametri.  
  
 **Rimuovi**  
 Selezionare un mapping dei parametri nell'elenco e quindi fare clic su **Rimuovi**.  
 
## <a name="result-set-page---execute-sql-task-editor"></a>Pagina Set dei risultati - Editor attività Esegui SQL
La pagina **Set dei risultati** della finestra di dialogo **Editor attività Esegui SQL** consente di eseguire il mapping dei risultati dell'istruzione SQL a variabili nuove o esistenti. Le opzioni disponibili in questa finestra di dialogo sono disabilitate se **ResultSet** è impostato su **None**nella pagina Generale.  
  
### <a name="options"></a>Opzioni  
 **Nome risultato**  
 Dopo aver aggiunto un set di mapping del set di risultati facendo clic su **Aggiungi**, specificare un nome per il risultato. A seconda del tipo di set di risultati, è necessario utilizzare nomi specifici per i risultati.  
  
 Se il set di risultati è di tipo **Riga singola**, è possibile utilizzare o il nome di una colonna restituita dalla query o il numero che rappresenta la posizione di una colonna nell'elenco di colonne di una colonna restituita dalla query.  
  
 Se il set di risultati è di tipo **Set dei risultati completo** o **XML**, sarà necessario usare 0 come nome del set di risultati.  
 
  
 **Nome variabile**  
 Eseguire il mapping del set di risultati a una variabile selezionando una variabile o facendo clic su \<**New variable...**> per aggiungere una nuova variabile usando la finestra di dialogo **Aggiungi variabile**.  
  
 **Aggiungere**  
 Fare clic su questo pulsante per aggiungere un mapping del set di risultati.  
  
 **Rimuovi**  
 Selezionare un mapping del set di risultati e quindi fare clic su **Rimuovi**.  
 
## <a name="parameters-in-the-execute-sql-task"></a>Parametri nell'attività Esegui SQL
Le istruzioni SQL e le stored procedure usano spesso parametri di **input** , parametri di **output** e codici restituiti. In [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], l'attività Esegui SQL supporta i tipi di parametro **Input**, **Output**e **ReturnValue** . Il tipo **Input** viene usato per i parametri di input, il tipo **Output** per i parametri di output e il tipo **ReturnValue** per i codici restituiti.  
  
> [!NOTE]  
>  È possibile utilizzare parametri in un'attività Esegui SQL solo se il provider di dati li supporta.  
  
 Sui parametri inclusi nei comandi SQL, comprese le query e le stored procedure, viene eseguito il mapping a variabili definite dall'utente create nell'ambito dell'attività Esegui SQL, in un contenitore padre o nell'ambito del pacchetto. I valori delle variabili possono essere impostati in fase di progettazione o popolati dinamicamente in fase di esecuzione. È inoltre possibile eseguire il mapping dei parametri a variabili di sistema. Per altre informazioni, vedere [Variabili di Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md) e [Variabili di sistema](../../integration-services/system-variables.md).  
  
 Tuttavia, l'utilizzo di parametri e di codici restituiti in un'attività Esegui SQL non si limita solo alla conoscenza dei tipi di parametro supportati dall'attività e del modo in cui si esegue il mapping di questi parametri. Sono previsti ulteriori requisiti e linee guida per utilizzare correttamente i parametri e i codici restituiti nell'attività Esegui SQL. Nella parte restante di questo argomento vengono illustrati tali requisiti e linee guida:  
  
-   [Uso di nomi e marcatori di parametro](#Parameter_names_and_markers)  
  
-   [Uso di parametri con i tipi di dati di data e ora](#Date_and_time_data_types)  
  
-   [Uso di parametri nelle clausole WHERE](#WHERE_clauses)  
  
-   [Uso di parametri con le stored procedure](#Stored_procedures)  
  
-   [Recupero dei valori dei codici restituiti](#Return_codes)    
  
###  <a name="parameter-names-and-markers"></a><a name="Parameter_names_and_markers"></a> Nomi e marcatori di parametro  
 Nella sintassi del comando SQL possono essere utilizzati marcatori di parametro diversi, a seconda del tipo di connessione utilizzato dall'attività Esegui SQL. Per il tipo di gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)], ad esempio, l'indicatore di parametro usato nel comando SQL deve avere il formato **\@varParameter**, mentre per il tipo di connessione OLE DB l'indicatore di parametro deve essere costituito da un punto interrogativo (?).  
  
 Anche i nomi che è possibile utilizzare come nomi di parametro nei mapping tra variabili e parametri variano a seconda del tipo di gestione connessione. Il tipo di gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] usa ad esempio un nome definito dall'utente con prefisso \@, mentre il tipo di gestione connessione OLE DB richiede nomi di parametro costituiti dal valore numerico di un ordinale in base 0.  
  
 Nella tabella seguente sono riepilogati i requisiti dei comandi SQL, a seconda dei tipi di gestione connessione utilizzati dall'attività Esegui SQL.  
  
|Tipo di connessione|Marcatore di parametro|Nome parametro|Comando SQL di esempio|  
|---------------------|----------------------|--------------------|-------------------------|  
|ADO|?|Param1, Param2, ...|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
|[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|\@\<parameter name>|\@\<parameter name>|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = \@parmContactID|  
|ODBC|?|1, 2, 3, ...|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
|EXCEL e OLE DB|?|0, 1, 2, 3, ...|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
  
#### <a name="use-parameters-with-adonet-and-ado-connection-managers"></a>Usare parametri con le gestioni connessioni ADO.NET e ADO  
 [!INCLUDE[vstecado](../../includes/vstecado-md.md)] e le gestioni connessioni ADO hanno requisiti specifici per i comandi SQL che usano parametri:  
  
-   Le gestioni connessioni [!INCLUDE[vstecado](../../includes/vstecado-md.md)] richiedono che il comando SQL usi nomi di parametro come indicatori di parametro. È pertanto possibile eseguire il mapping direttamente delle variabili ai parametri. Se ad esempio sulla variabile `@varName` viene eseguito il mapping a un parametro di nome `@parName` , fornirà il valore per il parametro `@parName`.  
  
-   Per le gestioni connessioni ADO, è necessario che il comando SQL utilizzi punti interrogativi (?) come marcatori di parametro. Tuttavia, come nomi di parametro è possibile utilizzare qualsiasi nome definito dall'utente, ad eccezione dei valori interi.  
  
 Per fornire i valori ai parametri sulle variabili viene eseguito il mapping ai nomi di parametro. L'attività Esegui SQL utilizza quindi il valore ordinale del nome di parametro nell'elenco dei parametri per caricare i valori dalle variabili ai parametri.  
  
#### <a name="use-parameters-with-excel-odbc-and-ole-db-connection-managers"></a>Usare parametri con le gestioni connessioni EXCEL, ODBC e OLE DB  
 Per le gestioni connessioni EXCEL, ODBC e OLE DB, è necessario che il comando SQL utilizzi punti interrogativi (?) come marcatori di parametro e valori numerici in base 0 o in base 1 come nomi di parametro. Se l'attività Esegui SQL utilizza la gestione connessione ODBC, il nome del parametro di cui viene eseguito il mapping al primo parametro nella query è 1, altrimenti è 0. Per i parametri successivi, il valore numerico del nome del parametro indica il parametro del comando SQL a cui viene eseguito il mapping del nome di parametro. Sul parametro di nome 3, ad esempio, viene eseguito il mapping al terzo parametro, rappresentato dal terzo punto interrogativo (?) nel comando SQL.  
  
 Per fornire i valori ai parametri, sulle variabili viene eseguito il mapping ai nomi di parametro e l'attività Esegui SQL utilizza il valore ordinale del nome di parametro per caricare i valori dalle variabili ai parametri.  
  
 A seconda del provider utilizzato dalla gestione connessione, alcuni tipi di dati OLE DB potrebbero non essere supportati. Il driver per Excel, ad esempio, riconosce solo un set limitato di tipi di dati. Per altre informazioni sul comportamento del provider Jet usato insieme al driver per Excel, vedere [Origine Excel](../../integration-services/data-flow/excel-source.md).  
  
#### <a name="use-parameters-with-ole-db-connection-managers"></a>Usare parametri con le gestioni connessioni OLE DB  
 Quando l'attività Esegui SQL usa la gestione connessione OLE DB, è disponibile la proprietà BypassPrepare dell'attività. Questa proprietà deve essere impostata su **true** se l'attività Esegui SQL usa istruzioni SQL con parametri.  
  
 Quando si utilizza una gestione connessione OLE DB, non è possibile utilizzare sottoquery con parametri, perché l'attività Esegui SQL non può derivare le informazioni sui parametri tramite il provider OLE DB. Tuttavia, è possibile utilizzare un'espressione per concatenare i valori dei parametri nella stringa di query e impostare la proprietà SqlStatementSource dell'attività.  
  
###  <a name="use-parameters-with-date-and-time-data-types"></a><a name="Date_and_time_data_types"></a> Usare parametri con i tipi di dati di data e ora  
  
#### <a name="use-date-and-time-parameters-with-adonet-and-ado-connection-managers"></a>Usare parametri di data e ora con le gestioni connessioni ADO.NET e ADO  
 Durante la lettura dei tipi di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , **time** and **datetimeoffset**, un'attività Esegui SQL che usa una gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] o ADO prevede i requisiti aggiuntivi seguenti:  
  
-   Per i dati **time** , una gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] richiede che i dati vengano archiviati in un parametro con tipo di parametro **Input** o **Output**e con tipo di dati **string**.  
  
-   Per i dati **datetimeoffset** , una gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] richiede che i dati vengano archiviati in uno dei parametri seguenti:  
  
    -   Un parametro il cui tipo di parametro è **Input** e il cui tipo di dati è **string**.  
  
    -   Un parametro il cui tipo di parametro è **Output** o **ReturnValue**e il cui tipo di dati è **datetimeoffset**, **stringa**, o **datetime2**. Se si seleziona un parametro il cui tipo di dati è **string** o **datetime2**, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] converte i dati in string o datetime2.  
  
-   Una gestione connessione ADO richiede che i dati **time** o **datetimeoffset** vengano archiviati in un parametro il cui tipo di parametro è **Input** o **Output**e il cui tipo di dati è **adVarWchar**.  
  
 Per altre informazioni sui tipi di dati [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e sul relativo mapping nei tipi di dati [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], vedere [Tipi di dati &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md) e [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
#### <a name="use-date-and-time-parameters-with-ole-db-connection-managers"></a>Usare parametri di data e ora con le gestioni connessioni OLE DB  
 Quando si usa una gestione connessione OLE DB, un'attività Esegui SQL prevede requisiti di archiviazione specifici per i tipi di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**date**, **time**, **datetime**, **datetime2**e **datetimeoffset**. È necessario archiviare questi dati in uno dei seguenti tipi di parametro:  
  
-   Un parametro di input del tipo di dati NVARCHAR.  
  
-   Un parametro di output con il tipo di dati appropriato, come elencato nella tabella seguente.  
  
    |Tipo di parametro di**Output**|Tipo di dati date|  
    |-------------------------------|--------------------|  
    |DBDATE|**date**|  
    |DBTIME2|**time**|  
    |DBTIMESTAMP|**datetime**, **datetime2**|  
    |DBTIMESTAMPOFFSET|**datetimeoffset**|  
  
 Se i dati non vengono archiviati nel parametro di input o di output appropriato, il pacchetto non viene eseguito correttamente.  
  
#### <a name="use-date-and-time-parameters-with-odbc-connection-managers"></a>Usare parametri di data e ora con le gestioni connessioni ODBC  
 Quando si usa una gestione connessione ODBC, un'attività Esegui SQL prevede requisiti di archiviazione specifici per i tipi di dati di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]**date**, **time**, **datetime**, **datetime2**o **datetimeoffset**. È necessario archiviare questi dati in uno dei seguenti tipi di parametro:  
  
-   Un parametro di **input** del tipo di dati SQL_WVARCHAR  
  
-   Un parametro di **output** con il tipo di dati appropriato, come elencato nella tabella seguente.  
  
    |Tipo di parametro di**Output**|Tipo di dati date|  
    |-------------------------------|--------------------|  
    |SQL_DATE|**date**|  
    |SQL_SS_TIME2|**time**|  
    |SQL_TYPE_TIMESTAMP<br /><br /> -oppure-<br /><br /> SQL_TIMESTAMP|**datetime**, **datetime2**|  
    |SQL_SS_TIMESTAMPOFFSET|**datetimeoffset**|  
  
 Se i dati non vengono archiviati nel parametro di input o di output appropriato, il pacchetto non viene eseguito correttamente.  
  
###  <a name="use-parameters-in-where-clauses"></a><a name="WHERE_clauses"></a> Usare parametri nelle clausole WHERE  
 I comandi SELECT, INSERT, UPDATE e DELETE includono spesso la clausola WHERE per specificare filtri che definiscono le condizioni che ogni riga nelle tabelle di origine deve soddisfare per essere qualificata per un comando SQL. I parametri specificano i valori del filtro per la clausola WHERE.  
  
 È possibile utilizzare marcatori di parametro per specificare dinamicamente i valori dei parametri. Le regole che determinano se è possibile utilizzare marcatori di parametro e nomi di parametro in un'istruzione SQL dipendono dal tipo di gestione connessione utilizzato dall'attività Esegui SQL.  
  
 Nella tabella seguente sono elencati esempi di comandi SELECT per tipo di gestione connessione. Le istruzioni INSERT, UPDATE e DELETE sono analoghe. Negli esempi l'istruzione SELECT viene usata per recuperare dalla tabella **Product** del database [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] i prodotti con **ProductID** compreso tra i valori specificati da due parametri.  
  
|Tipo di connessione|Sintassi dell'istruzione SELECT|  
|---------------------|-------------------|  
|EXCEL, ODBC e OLEDB|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
|ADO|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
|[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|`SELECT* FROM Production.Product WHERE ProductId > @parmMinProductID AND ProductID < @parmMaxProductID`|  
  
 Gli esempi richiedono parametri con i nomi seguenti:  
  
-   Per le gestioni connessioni EXCEL e OLED DB vengono utilizzati i nomi di parametro 0 e 1. Per il tipo di connessione ODBC vengono utilizzati 1 e 2.  
  
-   Per il tipo di connessione ADO è possibile utilizzare qualsiasi nome per i due parametri, ad esempio Param1 e Param2, ma è necessario eseguire il mapping di entrambi i parametri in base alla relativa posizione ordinale nell'elenco di parametri.  
  
-   Per il tipo di connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] vengono usati i nomi di parametro \@parmMinProductID e \@parmMaxProductID.  
  
###  <a name="use-parameters-with-stored-procedures"></a><a name="Stored_procedures"></a> Usare parametri con le stored procedure  
 Anche i comandi SQL che eseguono stored procedure possono utilizzare il mapping dei parametri. Come avviene per le regole delle query con parametri, anche le regole che determinano la modalità di utilizzo di marcatori di parametro e nomi di parametro dipendono dal tipo di gestione connessione utilizzato dall'attività Esegui SQL.  
  
 Nella tabella seguente sono elencati esempi di comandi EXEC per tipo di gestione connessione. Gli esempi eseguono la stored procedure **uspGetBillOfMaterials** nel database [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)]. La stored procedure usa i parametri di **input** `@StartProductID` e `@CheckDate`.  
  
|Tipo di connessione|Sintassi dell'istruzione EXEC|  
|---------------------|-----------------|  
|EXCEL e OLEDB|`EXEC uspGetBillOfMaterials ?, ?`|  
|ODBC|`{call uspGetBillOfMaterials(?, ?)}`<br /><br /> Per altre informazioni sulla sintassi ODBC, vedere l'argomento [Procedure Parameters](../../odbc/reference/develop-app/procedure-parameters.md)(Parametri di procedura) nella guida di riferimento per programmatori ODBC in MSDN Library.|  
|ADO|Se IsQueryStoredProcedure è impostato su **False**, `EXEC uspGetBillOfMaterials ?, ?`<br /><br /> Se IsQueryStoredProcedure è impostato su **True**, `uspGetBillOfMaterials`|  
|[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|Se IsQueryStoredProcedure è impostato su **False**, `EXEC uspGetBillOfMaterials @StartProductID, @CheckDate`<br /><br /> Se IsQueryStoredProcedure è impostato su **True**, `uspGetBillOfMaterials`|  
  
 La sintassi per l'utilizzo dei parametri di output richiede che dopo ogni marcatore di parametro venga specificata la parola chiave OUTPUT. Ad esempio, la sintassi del parametro di output seguente è corretta: `EXEC myStoredProcedure ? OUTPUT`.  
  
 Per altre informazioni sull'utilizzo di parametri di input e di output con le stored procedure Transact-SQL, vedere [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md).  
 
### <a name="map-query-parameters-to-variables"></a>Eseguire il mapping di parametri di query a variabili
In questa sezione viene descritto come usare un'istruzione SQL con parametri nell'attività Esegui SQL e come creare mapping tra variabili e parametri dell'istruzione SQL.  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che si desidera utilizzare.  
  
2.  In Esplora soluzioni fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di controllo** .  
  
4.  Se il pacchetto non include già un'attività Esegui SQL, aggiungerne una al flusso di controllo del pacchetto. Per altre informazioni, vedere [Aggiunta o eliminazione di un'attività o un contenitore in un flusso di controllo](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md).  
  
5.  Fare doppio clic sull'attività Esegui SQL.  
  
6.  Specificare un comando SQL con parametri in uno dei modi seguenti:  
  
    -   Usare l'input diretto e digitare il comando SQL nella proprietà SQLStatement.  
  
    -   Usare l'input diretto, fare clic su **Compila query**, quindi creare un comando SQL usando gli strumenti grafici disponibili in Generatore query.  
  
    -   Utilizzare una connessione file e quindi fare riferimento al file che contiene il comando SQL.  
  
    -   Utilizzare una variabile e quindi fare riferimento alla variabile che contiene il comando SQL.  
  
     I marcatori di parametro che è possibile utilizzare nelle istruzioni SQL con parametri dipendono dal tipo di connessione utilizzato dall'attività Esegui SQL.  
  
    |Tipo di connessione|Marcatore di parametro|  
    |---------------------|----------------------|  
    |ADO|?|  
    |ADO.NET e SQLMOBILE|\@\<parameter name>|  
    |ODBC|?|  
    |EXCEL e OLE DB|?|  
  
     Nella tabella seguente sono elencati esempi di comandi SELECT per tipo di gestione connessione. I parametri specificano i valori del filtro per la clausola WHERE. Negli esempi l'istruzione SELECT viene usata per recuperare dalla tabella **Product** del database [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] i prodotti con **ProductID** compreso tra i valori specificati da due parametri.  
  
    |Tipo di connessione|Sintassi dell'istruzione SELECT|  
    |---------------------|-------------------|  
    |EXCEL, ODBC e OLEDB|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
    |ADO|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
    |[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|`SELECT* FROM Production.Product WHERE ProductId > @parmMinProductID AND ProductID < @parmMaxProductID`|  
   
7.  Fare clic su **Mapping parametri**.  
  
8.  Per aggiungere un mapping parametri, fare clic su **Aggiungi**.  
  
9. Specificare un nome nella casella **Nome parametro** .  
  
     I nomi dei parametri utilizzati dipendono dal tipo di connessione utilizzato dall'attività Esegui SQL.  
  
    |Tipo di connessione|Nome parametro|  
    |---------------------|--------------------|  
    |ADO|Param1, Param2, ...|  
    |ADO.NET e SQLMOBILE|\@\<parameter name>|  
    |ODBC|1, 2, 3, ...|  
    |EXCEL e OLE DB|0, 1, 2, 3, ...|  
  
10. Selezionare una variabile nell'elenco **Nome variabile** . Per altre informazioni, vedere [Aggiungere, eliminare o modificare l'ambito di una variabile definita dall'utente in un pacchetto](../integration-services-ssis-variables.md).  
  
11. Nell'elenco **Direzione** specificare se il parametro è un input, un output o un valore restituito.  
  
12. Nell'elenco **Tipo di dati** impostare il tipo di dati del parametro.  
  
    > [!IMPORTANT]  
    >  Il tipo di dati del parametro deve essere compatibile con quello della variabile.  
  
13. Ripetere i passaggi da 8 a 11 per ogni parametro nell'istruzione SQL.  
  
    > [!IMPORTANT]  
    >  I mapping dei parametri devono essere specificati nello stesso ordine con cui compaiono i parametri nell'istruzione SQL.  
  
14. Fare clic su **OK**.  

##  <a name="get-the-values-of-return-codes"></a><a name="Return_codes"></a> Recuperare i valori dei codici restituiti  
 Una stored procedure può restituire un valore intero, denominato codice restituito, per indicare lo stato di esecuzione di una procedura. Per implementare codici restituiti nell'attività Esegui SQL, è necessario usare parametri di tipo **ReturnValue** .  
  
 Nella tabella seguente sono elencati, per tipo di gestione connessione, esempi di comandi EXEC che implementano codici restituiti. In tutti gli esempi viene usato un parametro di **input** . Le regole che determinano la modalità d'uso di indicatori di parametro e nomi di parametro sono identiche per tutti i tipi di parametro:**Input**, **Output**e **ReturnValue**.  
  
 In alcune sintassi non è supportato l'utilizzo di valori letterali come parametri. In tali casi è necessario specificare il valore del parametro utilizzando una variabile.  
  
|Tipo di connessione|Sintassi dell'istruzione EXEC|  
|---------------------|-----------------|  
|EXCEL e OLEDB|`EXEC ? = myStoredProcedure 1`|  
|ODBC|`{? = call myStoredProcedure(1)}`<br /><br /> Per altre informazioni sulla sintassi ODBC, vedere l'argomento [Procedure Parameters](../../odbc/reference/develop-app/procedure-parameters.md)(Parametri di procedura) nella guida di riferimento per programmatori ODBC in MSDN Library.|  
|ADO|Se IsQueryStoreProcedure è impostato su **False**, `EXEC ? = myStoredProcedure 1`<br /><br /> Se IsQueryStoreProcedure è impostato su **True**, `myStoredProcedure`|  
|[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|Set IsQueryStoreProcedure è impostato su **True**.<br /><br /> `myStoredProcedure`|  
  
 Nella sintassi illustrata nella tabella precedente, l'attività Esegui SQL usa il tipo di origine **Input diretto** per eseguire la stored procedure. L'attività Esegui SQL può usare anche il tipo di origine **Connessione file** per eseguire una stored procedure. Indipendentemente dal fatto che l'attività Esegui SQL utilizzi il tipo di origine **Input diretto** o **Connessione file** , usare un parametro del tipo **ReturnValue** per implementare il codice restituito.
  
 Per altre informazioni sull'utilizzo di codici restituiti con le stored procedure Transact-SQL, vedere [RETURN &#40;Transact-SQL&#41;](../../t-sql/language-elements/return-transact-sql.md).  
  
## <a name="result-sets-in-the-execute-sql-task"></a>Set di risultati nell’attività Esegui SQL
 La restituzione di un set di risultati all'attività Esegui SQL in un pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] dipende dal tipo di comando SQL utilizzato dall'attività. Se si utilizzano ad esempio le istruzioni SELECT, viene in genere restituito un set di risultati, mentre questo non avviene per le istruzioni INSERT.  
  
 Anche il contenuto del set di risultati varia in base al comando SQL. Il set di risultati restituito da un'istruzione SELECT può ad esempio contenere zero, una o più righe. Il set di risultati di un'istruzione SELECT che restituisce un conteggio o una somma contiene tuttavia una sola riga.  
  
 Per usare i set di risultati in un'attività Esegui SQL non è sufficiente sapere se il comando SQL restituisce un set di risultati né conoscere il contenuto di tale set di risultati. Sono previsti ulteriori requisiti e linee guida per usare correttamente i set di risultati nell'attività Esegui SQL. Nella parte restante di questo argomento vengono illustrati tali requisiti e linee guida:  
  
-   [Impostazione del tipo di un set di risultati](#Result_set_type)  
  
-   [Popolamento di una variabile con un set di risultati](#Populate_variable_with_result_set)  
  
###  <a name="specify-a-result-set-type"></a><a name="Result_set_type"></a> Specificare un tipo di set di risultati  
 L'attività Esegui SQL supporta i tipi di set di risultati seguenti:  
  
-   Se la query non restituisce risultati, sarà usato il set di risultati **Nessuno** . Questo set di risultati può essere usato ad esempio per le query che aggiungono, modificano ed eliminano record in una tabella.  
  
-   Se la query restituisce una sola riga, sarà usato il set di risultati **Riga singola** . Questo set di risultati può ad esempio essere usato per un'istruzione SELECT che restituisce un conteggio o una somma.  
  
-   Se la query restituisce più righe, sarà usato il set di risultati **Set dei risultati completo** . Questo set di risultati può ad esempio essere usato per un'istruzione SELECT che recupera tutte le righe di una tabella.  
  
-   Se la query restituisce un set di risultati in formato XML, sarà usato il set di risultati **XML** . Questo set di risultati può ad esempio essere usato per un'istruzione SELECT che include una clausola FOR XML.  
  
 Se nell'attività Esegui SQL è usato il **Set dei risultati completo** e la query restituisce più set di righe, l'attività restituisce solo il primo di tali set. Se questo set di righe genera un errore, l'attività segnala l'errore. Se altri set di righe generano errori, l'attività non li segnala.  
  
###  <a name="populate-a-variable-with-a-result-set"></a><a name="Populate_variable_with_result_set"></a> Popolare una variabile con un set di risultati  
 Se il set di risultati restituito da una query è una riga singola, un set di righe o di tipo XML, sarà possibile associarlo a una variabile definita dall'utente.  
  
 Se il tipo di set di risultati è **Riga singola**, è possibile associare una colonna nel risultato restituito a una variabile usando il nome della colonna come nome del set di risultati oppure usare la posizione ordinale della colonna nell'elenco di colonne come nome del set di risultati. Il nome del set di risultati per la query `SELECT Color FROM Production.Product WHERE ProductID = ?` , ad esempio, potrebbe essere **Color** o **0**. Se la query restituisce più colonne e si desidera accedere ai valori in tutte le colonne, è necessario associare ogni colonna a una variabile diversa. Se si esegue il mapping delle colonne alle variabili usando numeri come nomi del set di risultati, i numeri riflettono l'ordine in cui le colonne vengono visualizzate nell'elenco di colonne della query. Nella query `SELECT Color, ListPrice, FROM Production.Product WHERE ProductID = ?`, ad esempio, viene usato 0 per la colonna **Color** e 1 per la colonna **ListPrice** . La possibilità di usare un nome di colonna come nome di un set di risultati dipende dal provider per il quale l'attività è configurata. Non tutti i provider permettono l'uso di nomi di colonna.  
  
 Alcune query che restituiscono un singolo valore non includono nomi di colonna. L'istruzione `SELECT COUNT (*) FROM Production.Product` non restituisce ad esempio alcun nome di colonna. Per accedere al risultato restituito è possibile usare la posizione ordinale, 0, come nome del risultato. Per accedere al risultato restituito in base al nome della colonna, la query deve includere una clausola AS \<alias name> che specifichi un nome di colonna. Nell'istruzione `SELECT COUNT (*)AS CountOfProduct FROM Production.Product`è specificato il nome di colonna **CountOfProduct** . Per accedere alla colonna del risultato restituito è quindi possibile usare il nome di colonna, **CountOfProduct** , o la posizione ordinale, 0.  
  
 Se il set di risultati è di tipo **Set dei risultati completo** o **XML**, sarà necessario usare 0 come nome del set di risultati.  
  
 Quando si esegue il mapping di una variabile a un set di risultati con il tipo di set di risultati **Riga singola** , la variabile deve avere un tipo di dati compatibile con quello della colonna contenuta nel set di risultati. Non è possibile, ad esempio, eseguire il mapping di un set di risultati che contiene una colonna con un tipo di dati **String** a una variabile con un tipo di dati numerico. Se si imposta la proprietà **TypeConversionMode** su **Allowed**, l'attività Esegui SQL tenterà di convertire il parametro di output e i risultati della query nel tipo di dati della variabile a cui sono assegnati i risultati.  
  
 È possibile eseguire il mapping di un set di risultati XML solo a una variabile con il tipo di dati **String** o **Object** . Se la variabile ha il tipo di dati **String** , l'attività Esegui SQL restituisce una stringa e l'origine XML può utilizzare i dati XML. Se la variabile ha il tipo di dati **Object** , l'attività Esegui SQL restituisce un oggetto DOM (Document Object Model).  
  
 Un **Set dei risultati completo** deve eseguire il mapping a una variabile con il tipo di dati **Object** . Il risultato restituito è un oggetto set di righe. È possibile usare un contenitore Ciclo ForEach per estrarre i valori di riga della tabella archiviati nella variabile Object nelle variabili del pacchetto e quindi usare un'attività Script per scrivere in un file i dati archiviati nelle variabili del pacchetto. Per una dimostrazione dell'esecuzione di questa operazione tramite un contenitore Ciclo ForEach e un'attività Script, vedere l'esempio CodePlex, relativo all' [esecuzione di parametri SQL e set di risultati](https://go.microsoft.com/fwlink/?LinkId=157863)sul sito Web msftisprodsamples.codeplex.com.  
  
 Nella tabella seguente è disponibile un riepilogo dei tipi di dati delle variabili di cui è possibile eseguire il mapping a set di risultati.  
  
|Tipo di set di risultati|Tipo di dati della variabile|Tipo di oggetto|  
|---------------------|---------------------------|--------------------|  
|Riga singola|Qualunque tipo compatibile con la colonna del tipo nel set di risultati.|Non applicabile|  
|Set dei risultati completo|**Object**|Se l'attività usa una gestione connessione nativa, incluse le gestioni connessioni ADO, OLE DB, Excel e ODBC, l'oggetto restituito è un oggetto **Recordset**ADO.<br /><br /> Se nell'attività viene usata una gestione connessione gestita, ad esempio la gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] , l'oggetto restituito è un oggetto **System.Data.DataSet**.<br /><br /> È possibile usare un'attività Script per accedere all'oggetto **System.Data.DataSet** , come illustrato nell'esempio seguente.<br /><br /> `Dim dt As Data.DataTable`<br /><br /> `Dim ds As Data.DataSet = CType(Dts.Variables("Recordset").Value, DataSet) dt = ds.Tables(0)`|  
|XML|**Stringa**|**Stringa**|  
|XML|**Object**|Se nell'attività è usata una gestione connessione nativa, incluse le gestioni connessioni ADO, OLE DB, Excel e ODBC, l'oggetto restituito è un oggetto **MSXML6.IXMLDOMDocument**.<br /><br /> Se nell'attività viene usata una gestione connessione gestita, ad esempio la gestione connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] , l'oggetto restituito è un oggetto **System.Xml.XmlDocument**.|  
  
 La variabile può essere definita nell'ambito dell'attività Esegui SQL o nell'ambito del pacchetto. Se la variabile viene definita nell'ambito del pacchetto, il set di risultati sarà disponibile per altre attività e contenitori all'interno del pacchetto e per altri pacchetti eseguiti dalle attività Esegui pacchetto o Esegui pacchetto DTS 2000.  
  
 Quando si esegue il mapping di una variabile a un set di risultati di tipo **Riga singola** , i valori non costituiti da stringhe restituiti dall'istruzione SQL vengono convertiti in stringhe se sussistono le condizioni seguenti:  
  
-   La proprietà **TypeConversionMode** è impostata su true. Il valore della proprietà viene impostato nella finestra Proprietà o tramite l' **Editor attività Esegui SQL**.  
  
-   La conversione non comporterà il troncamento dei dati.  
  
## <a name="map-result-sets-to-variables-in-an-execute-sql-task"></a>Mapping di set di risultati a variabili in un'attività Esegui SQL
Questa sezione descrive la procedura per il mapping di un set di risultati a una variabile in un'attività Esegui SQL. Se su un set di risultati viene eseguito il mapping a una variabile, sarà disponibile anche per altri elementi nel pacchetto. Si consideri ad esempio un'attività Script contenente uno script in grado di leggere la variabile e quindi utilizzare i valori del set di risultati oppure un'origine XML in grado di utilizzare il set di risultati archiviato in una variabile. Se viene generato da un pacchetto padre, il set di risultati potrà essere reso disponibile a un pacchetto figlio chiamato da un'attività Esegui pacchetto mappando tale set di risultati a una variabile nel pacchetto padre e quindi creando nel pacchetto figlio una configurazione Variabile pacchetto padre, per l'archiviazione del valore della variabile padre.  
  
1.  In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]aprire il progetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] che contiene il pacchetto desiderato.  
  
2.  In **Esplora soluzioni**fare doppio clic sul pacchetto per aprirlo.  
  
3.  Fare clic sulla scheda **Flusso di controllo** .  
  
4.  Se il pacchetto non include già un'attività Esegui SQL, aggiungerne una al flusso di controllo del pacchetto. Per altre informazioni, vedere [Aggiunta o eliminazione di un'attività o un contenitore in un flusso di controllo](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md).  
  
5.  Fare doppio clic sull'attività Esegui SQL.  
  
6.  Nella pagina **Generale** della finestra di dialogo **Editor attività Esegui SQL** selezionare il tipo di set di risultati **Riga singola**, **Set dei risultati completo**o **XML** .  

7.  Fare clic su **Set dei risultati**.  
  
8.  Per aggiungere un mapping del set dei risultati, fare clic su **Aggiungi**.  
  
9. Selezionare una variabile dall'elenco **Variables Name** (Nome variabili) o crearne una nuova. Per altre informazioni, vedere [Aggiungere, eliminare o modificare l'ambito di una variabile definita dall'utente in un pacchetto](../integration-services-ssis-variables.md).  
  
10. Nell'elenco **Nome risultato** modificare il nome del set di risultati, se lo si desidera.  
  
     È in genere possibile utilizzare il nome della colonna come nome del set di risultati oppure utilizzare la posizione ordinale della colonna nell'elenco di colonne come set di risultati. La possibilità di utilizzare un nome di colonna come nome del set di risultati dipende dal provider per il quale l'attività è configurata. Non tutti i provider permettono l'uso di nomi di colonna.  
  
11. Fare clic su **OK**.  

## <a name="troubleshoot-the-execute-sql-task"></a>Risolvere i problemi relativi all'attività Esegui SQL  
 È possibile registrare le chiamate eseguite dall'attività Esegui SQL a provider di dati esterni. Questa funzionalità di registrazione può essere utilizzata per risolvere i problemi relativi ai comandi SQL eseguiti dall'attività Esegui SQL. Per registrare le chiamate eseguite dall'attività Esegui SQL a provider di dati esterni, abilitare la registrazione dei pacchetti e selezionare l'evento **Diagnostic** a livello del pacchetto. Per altre informazioni, vedere [Risoluzione dei problemi relativi agli strumenti per l'esecuzione del pacchetto](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
 Talvolta un comando SQL o una stored procedure restituiscono più set di risultati. Tali set di risultati includono non solo i set di righe che sono il risultato di query **SELECT** , ma anche valori singoli che sono il risultato di errori di istruzioni **RAISERROR** o **PRINT** . L'attività ignora gli errori nei set di risultati che si verificano dopo il primo set di risultati in base al tipo di gestione connessione utilizzata:  
  
-   Se si utilizzano le gestioni connessioni OLE DB e ADO, l'attività ignora i set di risultati che si verificano dopo il primo set di risultati. Pertanto, con tali gestioni connessioni, l'attività ignora un errore restituito da un comando SQL o da una stored procedure quando l'errore non fa parte del primo set di risultati.  
  
-   Se si utilizzano le gestioni connessioni ODBC e ADO.NET, l'attività non ignora i set di risultati che si verificano dopo il primo set di risultati. Con queste gestioni connessioni, l'attività non riesce e viene restituito un errore qualora un set di risultati diverso dal primo set di risultati contiene un errore.  
  
### <a name="custom-log-entries"></a>Voci di log personalizzate  
 Nella tabella seguente è indicata la voce di log personalizzata disponibile per l'attività Esegui SQL. Per altre informazioni, vedere [registrazione di Integration Services &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
|Voce di log|Descrizione|  
|---------------|-----------------|  
|**ExecuteSQLExecutingQuery**|Fornisce informazioni sulle fasi di esecuzione dell'istruzione SQL. Vengono scritte voci di log quando l'attività acquisisce la connessione al database, quando inizia a preparare l'istruzione SQL e al termine dell'esecuzione dell'istruzione SQL. La voce di log per la fase di preparazione include l'istruzione SQL utilizzata dall'attività.|