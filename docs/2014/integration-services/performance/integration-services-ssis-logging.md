---
title: Registrazione di Integration Services (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- containers [Integration Services], logs
- Windows Event log provider [Integration Services]
- XML File log provider [Integration Services]
- SQL Server Profiler, log provider
- SQL Server Integration Services packages, logs
- SSIS packages, logs
- tasks [Integration Services], logs
- logs [Integration Services], log providers
- Integration Services packages, logs
- log providers [Integration Services]
- packages [Integration Services], logs
- Text File log provider
- SQL Server log provider
ms.assetid: 65e17889-371f-4951-9a7e-9932b2d0dcde
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 2478f1605b7fb67d8328be905956cbaae8e3c243
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62889813"
---
# <a name="integration-services-ssis-logging"></a>Registrazione di Integration Services (SSIS)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] include i provider di log che è possibile utilizzare per implementare la registrazione in pacchetti, contenitori e attività. Tramite la registrazione è possibile acquisire informazioni di run-time su un pacchetto, che consentono di controllare e risolvere i problemi del pacchetto ogni volta che viene eseguito. Nel log è ad esempio possibile acquisire il nome dell'operatore che ha eseguito il pacchetto, nonché la data e l'ora di inizio e di fine dell'esecuzione.  
  
 È possibile configurare l'ambito di registrazione che si verifica durante l'esecuzione di un pacchetto nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Per altre informazioni, vedere [Abilitare la registrazione per l'esecuzione di pacchetti nel server SSIS](../enable-logging-for-package-execution-on-the-ssis-server.md)  
  
 Si può anche includere la registrazione quando si esegue un pacchetto con l'utilità del prompt dei comandi **dtexec** . Per ulteriori informazioni sugli argomenti del prompt dei comandi che supportano la registrazione, vedere [dtexec Utility](../packages/dtexec-utility.md).  
  
## <a name="configure-logging-in-sql-server-data-tools"></a>Configurare la registrazione in SQL Server Data Tools  
 I log sono associati ai pacchetti e vengono configurati a livello del pacchetto. Ogni attività o contenitore di un pacchetto può registrare informazioni in qualsiasi log del pacchetto. Le attività e i contenitori di un pacchetto possono essere abilitati per la registrazione anche se per il pacchetto la registrazione non è stata attivata. È possibile, ad esempio, abilitare la registrazione in un'attività Esegui SQL senza abilitarla nel pacchetto padre. Un pacchetto, un contenitore o un'attività possono registrare voci in più log. È possibile scegliere di abilitare la registrazione solo sul pacchetto oppure su ogni singolo contenitore o attività presente nel pacchetto.  
  
 Quando si aggiunge un log a un pacchetto, è necessario scegliere il provider di log e il percorso del log. Il provider di log specifica il formato dei dati del log, ad esempio un database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o un file di testo.  
  
 
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] sono disponibili i provider di log seguenti:  
  
-   Provider di log File di testo, che scrive le voci di log in file di testo ASCII in formato CSV. L'estensione predefinita dei file per questo provider è log.  
  
-   Provider di log [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] , che scrive tracce che è possibile visualizzare utilizzando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Profiler. L'estensione predefinita dei file per questo provider è trc.  
  
    > [!NOTE]  
    >  In un pacchetto in esecuzione in modalità a 64 bit non è possibile usare il provider di log di [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] .  
  
-   Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di log, che scrive le `sysssislog` voci di log nella tabella [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di un database.  
  
-   Provider di log Registro eventi di Windows, che scrive le voci nel registro applicazioni del registro eventi di Windows sul computer locale.  
  
-   Provider di log File XML, che scrive file di log in formato XML. L'estensione predefinita dei file per questo provider è xml.  
  
 Se si aggiunge un provider di log a un pacchetto o si configura la registrazione a livello di codice, sarà possibile utilizzare un ProgID o un ClassID per identificare il provider di log, anziché utilizzare i nomi visualizzati in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , nella finestra di dialogo **Configura log SSIS** .  
  
 Nella tabella seguente sono elencati i ProgID e i ClassID per i provider di log disponibili in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e i percorsi dei log in cui scrivono i provider.  
  
|Provider di log|ProgID|ClassID|Location|  
|------------------|------------|-------------|--------------|  
|File di testo|DTS.LogProviderTextFile|{0A039101-ACC1-4E06-943F-279948323883}|La gestione connessione file utilizzata dal provider di log specifica il percorso del file di testo.|  
|SQL Server Profiler|DTS.LogProviderSQLProfiler|{E93F6300-AE0C-4916-A7BF-A8D0CE12C77A}|La gestione connessione file utilizzata dal provider di log specifica il percorso del file utilizzato da [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)].|  
|SQL Server|DTS.LogProviderSQLServer|{94150B25-6AEB-4C0D-996D-D37D1C4FDEDA}|La gestione connessione OLE DB usata dal provider di log indica il database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in cui si trova la tabella sysssislog contenente le voci di log.|  
|Registro eventi di Windows|DTS.LogProviderEventLog|{071CC8EB-C343-4CFF-8D58-564B92FCA3CF}|Il registro applicazioni nel Visualizzatore eventi di Windows contiene le informazioni del log di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .|  
|File XML|DTS.LogProviderXMLFile|{440945A4-2A22-4F19-B577-EAF5FDDC5F7A}|La gestione connessione file utilizzata dal provider di log specifica il percorso del file XML.|  
  
 È inoltre possibile creare provider di log personalizzati. Per altre informazioni, vedere [Creating a Custom Log Provider](../extending-packages-custom-objects/log-provider/creating-a-custom-log-provider.md).  
  
 I provider di log di un pacchetto sono membri della raccolta dei provider di log del pacchetto. Se si crea un pacchetto e si implementa la registrazione tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , sarà possibile visualizzare l'elenco dei membri della raccolta nelle cartelle **Provider di log** della scheda **Esplora pacchetti** di Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Per configurare un provider di log è necessario specificarne il nome, la descrizione e la gestione connessione utilizzata. Il provider di log [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizza una gestione connessione OLE DB. I provider di log File di testo, [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]e File XML utilizzano gestioni connessioni file. Il provider di log Registro eventi di Windows non utilizza invece una gestione connessione, perché scrive direttamente nel Registro eventi di Windows. Per ulteriori informazioni, vedere [OLE DB Connection Manager](../connection-manager/ole-db-connection-manager.md) e [File Connection Manager](../connection-manager/file-connection-manager.md).  
  
### <a name="logging-customization"></a>Personalizzazione della registrazione  
 Per la personalizzazione della registrazione di un evento o la creazione di un messaggio personalizzato, in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è disponibile uno schema di informazioni comunemente registrate, che è possibile includere nelle voci di log. Lo schema del log di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] delinea le informazioni che è possibile registrare. È possibile selezionare elementi dallo schema per ogni voce di log.  
  
 Un pacchetto e le attività e i contenitori associati non devono necessariamente registrare le stesse informazioni. Inoltre le singole attività incluse in un pacchetto o contenitore possono registrare informazioni diverse. Ad esempio, un pacchetto potrebbe registrare informazioni relative agli operatori quando viene avviato, una delle attività potrebbe registrare la causa dell'esito negativo dell'attività e un'altra attività potrebbe registrare informazioni quando si verificano errori. Se un pacchetto e le attività e i contenitori associati utilizzano più log, in tutti i log vengono registrate le stesse informazioni.  
  
 È possibile selezionare il livello di registrazione più adatto alle proprie esigenze specificando gli eventi e le informazioni di ogni evento da registrare. A seconda delle specifiche esigenze le informazioni fornite da alcuni eventi potrebbero risultare più utili rispetto a quelle di altri eventi. Potrebbe risultare utile, ad esempio, registrare solo il nome del computer e dell'operatore dell'evento **PreExecute** , ma tutte le informazioni disponibili per l'evento **Error** .  
  
 Per impedire che i file di log utilizzino una quantità di spazio su disco elevata o per evitare un'attività di registrazione eccessiva che potrebbe influire negativamente sulle prestazioni, è possibile selezionare gli eventi e le informazioni da registrare. È possibile, ad esempio, configurare un log in modo che per ogni errore vengano registrati solo il nome del computer e la data.  
  
 Nella finestra di dialogo [!INCLUDE[ssIS](../../includes/ssis-md.md)] Configura log SSIS **di Progettazione** sono disponibili le opzioni di registrazione.  
  
#### <a name="log-schema"></a>Schema del log  
 Nella tabella seguente vengono descritti gli elementi dello schema del log.  
  
|Elemento|Descrizione|  
|-------------|-----------------|  
|Computer|Nome del computer in cui è stato generato l'evento.|  
|Operatore|Identifica l'utente che ha avviato il pacchetto.|  
|SourceName|Nome del contenitore o dell'attività in cui è stato generato l'evento.|  
|SourceID|Identificatore univoco del pacchetto, contenitore Ciclo For, Ciclo Foreach o Sequenza oppure attività in cui è stato generato l'evento.|  
|ExecutionID|GUID dell'istanza di esecuzione del pacchetto.<br /><br /> L'esecuzione di un singolo pacchetto potrebbe creare voci di log con valori diversi per l'elemento ExecutionID. Ad esempio, quando si esegue un pacchetto in [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], la fase di convalida potrebbe creare voci di log con un elemento ExecutionID che corrisponde a [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. La fase di esecuzione potrebbe invece creare voci di log con un elemento ExecutionID che corrisponde a dtshost.exe. Per fornire un altro esempio, quando si esegue un pacchetto che contiene attività Esegui pacchetto, ognuna di queste attività esegue un pacchetto figlio. Questi pacchetti figlio potrebbero creare voci di log con un elemento ExecutionID diverso rispetto alle voci di log create dal pacchetto.|  
|MessageText|Messaggio associato alla voce di log.|  
|DataBytes|Matrice di byte specifica della voce di log. Il significato di questo campo varia a seconda della voce di log.|  
  
 Nella tabella seguente sono descritti tre elementi aggiuntivi dello schema del log che non sono disponibili nella scheda **Dettagli** della finestra di dialogo **Configura log SSIS** .  
  
|Elemento|Descrizione|  
|-------------|-----------------|  
|StartTime|Ora di inizio dell'esecuzione del contenitore o dell'attività.|  
|EndTime|Ora di arresto dell'esecuzione del contenitore o dell'attività.|  
|DataCode|Valore intero facoltativo che in genere contiene un valore dell'enumerazione <xref:Microsoft.SqlServer.Dts.Runtime.DTSExecResult> che indica il risultato dell'esecuzione del contenitore o dell'attività:<br /><br /> 0 - Esito positivo<br /><br /> 1 - Esito negativo<br /><br /> 2 - Esecuzione completata<br /><br /> 3 - Esecuzione annullata|  
  
##### <a name="log-entries"></a>Voci di log  
 
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] supporta voci di log per gli eventi predefiniti e offre voci di log personalizzate per molti oggetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Tali eventi e voci di log personalizzate sono elencati nella finestra di dialogo **Configura log SSIS** di Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 Nella tabella seguente vengono descritti gli eventi predefiniti che è possibile abilitare per scrivere voci di log quando si verificano eventi di run-time. Queste voci sono relative ai file eseguibili, al pacchetto e alle attività e ai contenitori inclusi nel pacchetto. Il nome della voce di log corrisponde al nome dell'evento di run-time che è stato generato e che ha causato la scrittura della voce.  
  
|Eventi|Descrizione|  
|------------|-----------------|  
|**OnError**|Viene inserita una voce del registro quando si verifica un errore.|  
|**OnExecStatusChanged**|Viene scritta una voce del registro quando un'attività (non un contenitore) viene sospesa o ripresa durante il debug.|  
|**OnInformation**|Viene scritta una voce del registro durante la convalida e l'esecuzione di un eseguibile per la segnalazione di informazioni.|  
|**OnPostExecute**|Viene registrata una voce di log non appena l'esecuzione del file eseguibile viene completata.|  
|**OnPostValidate**|Viene registrata una voce di log dopo la convalida del file eseguibile.|  
|**OnPreExecute**|Viene registrata una voce di log immediatamente prima dell'esecuzione del file eseguibile.|  
|**OnPreValidate**|Viene registrata una voce di log all'avvio della convalida del file eseguibile.|  
|**OnProgress**|Viene registrata una voce di log dopo un avanzamento percettibile dell'esecuzione del file eseguibile.|  
|**OnQueryCancel**|Viene registrata una voce di log in qualsiasi momento dell'elaborazione dell'attività in cui è possibile annullare l'esecuzione.|  
|**OnTaskFailed**|Viene registrata una voce di log quando un'attività ha esito negativo.|  
|**OnVariableValueChanged**|Viene registrata una voce di log quando il valore di una variabile viene modificato.|  
|**OnWarning**|Viene registrata una voce di log in corrispondenza di un avviso.|  
|**PipelineComponentTime**|Per ogni componente del flusso di dati, viene registrata una voce di log per ogni fase di convalida ed esecuzione. La voce di log specifica il tempo di elaborazione per ogni fase.|  
|**Diagnostica**|Viene registrata una voce di log che fornisce informazioni diagnostiche.<br /><br /> È ad esempio possibile registrare un messaggio prima e dopo ogni chiamata a un provider di dati esterno. Per altre informazioni, vedere [Risoluzione dei problemi relativi agli strumenti per l'esecuzione del pacchetto](../troubleshooting/troubleshooting-tools-for-package-execution.md).|  
  
 Per il pacchetto e per molte attività sono disponibili voci di log personalizzate che è possibile abilitare per la registrazione. Per l'attività Invia messaggi è ad esempio disponibile la voce di log personalizzata **SendMailTaskBegin** , che registra informazioni quando l'attività viene avviata, ma prima che invii un messaggio di posta elettronica. Per altre informazioni, vedere [Custom Messages for Logging](../custom-messages-for-logging.md).  
  
### <a name="differentiating-package-copies"></a>Differenziazione delle copie di un pacchetto  
 I dati del log includono il nome e il GUID del pacchetto a cui appartengono le voci di log. Se si crea un nuovo pacchetto copiando un pacchetto esistente, verranno copiati anche il nome e il GUID del pacchetto esistente. Possono essere pertanto presenti due pacchetti con nome e GUID uguali e questo può impedire di distinguere tali pacchetti nei dati del log.  
  
 Per eliminare questa ambiguità, è consigliabile modificare il nome e il GUID dei nuovi pacchetti. In [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] è possibile rigenerare il GUID nella proprietà `ID` e modificare il valore della proprietà `Name` nella finestra Proprietà. È inoltre possibile modificare il GUID e il nome a livello di codice oppure eseguendo **dtutil** dal prompt dei comandi. Per altre informazioni, vedere [Impostazione delle proprietà di un pacchetto](../set-package-properties.md) e [Utilità dtutil](../dtutil-utility.md).  
  
### <a name="parent-logging-options"></a>Opzioni di registrazione padre  
 Spesso le opzioni di registrazione delle attività e dei contenitori Ciclo For, Ciclo Foreach e Sequenza corrispondono a quelle del pacchetto o di un contenitore padre. In questo caso è possibile configurarle in modo che ereditino l'impostazione delle opzioni di registrazione del contenitore padre. Ad esempio, in un contenitore Ciclo For che include un'attività Esegui SQL l'attività può utilizzare le opzioni di registrazione impostate nel contenitore. Per consentire l'utilizzo delle opzioni di registrazione padre, è necessario impostare la proprietà LoggingMode del contenitore su **UseParentSetting**. Questa impostazione può essere eseguita nella finestra **Proprietà** di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o nella finestra di dialogo **Configura log SSIS** di Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
### <a name="logging-templates"></a>Modelli di registrazione  
 Nella finestra di dialogo **Configura log SSIS** è inoltre possibile creare e salvare come modelli le configurazioni di registrazione utilizzate di frequente. I modelli possono essere quindi applicati in più pacchetti. Ciò consente di applicare una strategia di registrazione consistente tra più pacchetti e di modificare le impostazione di log dei pacchetti semplicemente aggiornando e applicando i modelli. I modelli vengono archiviati in file XML.  
  
 **Per configurare la registrazione tramite la finestra di dialogo Configura log SSIS**  
  
1.  Abilitare il pacchetto e le attività associate per la registrazione. La registrazione può venire eseguita a livello del pacchetto, del contenitore e dell'attività. È possibile specificare log diversi per pacchetti, contenitori e attività.  
  
2.  Selezionare un provider di log e aggiungere un log per il pacchetto. È possibile creare log solo a livello di pacchetto. Inoltre attività o contenitori devono utilizzare uno dei log creati per il pacchetto. I possibili provider di log a cui può essere associato un log sono file di testo, [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], registro eventi di Windows o file XML. Per altre informazioni, vedere [Abilitare la registrazione di pacchetti in SQL Server Data Tools](../enable-package-logging-in-sql-server-data-tools.md).  
  
3.  Selezionare gli eventi e le informazioni dello schema del registro relative a ogni evento che si desidera registrare. Per altre informazioni, vedere [Configurazione della registrazione tramite un file di configurazione salvato](../configure-logging-by-using-a-saved-configuration-file.md).  
  
### <a name="configuration-of-log-provider"></a>Configurazione del provider di log  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 La creazione e la configurazione del provider di log avviene in un passaggio dell'implementazione della registrazione in un pacchetto. Per ulteriori informazioni, vedere [Integration Services registrazione](integration-services-ssis-logging.md).  
  
 Dopo avere creato un provider di log è possibile visualizzarne e modificarne le proprietà nella finestra Proprietà di [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)].  
  
 Per informazioni sull'impostazione di queste proprietà a livello di programmazione, vedere la documentazione per la classe <xref:Microsoft.SqlServer.Dts.Runtime.LogProvider> .  
  
### <a name="logging-for-data-flow-tasks"></a>Registrazione per le attività Flusso di dati  
 L'attività Flusso di dati offre molte voci di log personalizzate che è possibile utilizzare per monitorare e regolare le prestazioni. È ad esempio possibile monitorare i componenti che potrebbero causare perdite di memoria o tenere traccia del tempo necessario per eseguire un componente specifico. Per un elenco di queste voci di log personalizzate e un output di registrazione di esempio, vedere [Data Flow Task](../control-flow/data-flow-task.md).  
  
#### <a name="use-the-pipelinecomponenttime-event"></a>Utilizzo dell'evento PipelineComponentTime  
 La voce di log personalizzata più utile è probabilmente l'evento PipelineComponentTime. Questa voce di log indica il numero di millisecondi che ogni componente del flusso di dati dedica a ognuno dei cinque passaggi principali dell'elaborazione. Nella tabella seguente vengono descritti i passaggi di elaborazione. 
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Gli sviluppatori di Integration Services riconosceranno tali passaggi come i metodi principali di <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>.  
  
|Passaggio|Descrizione|  
|----------|-----------------|  
|Convalida|Il componente verifica la presenza di impostazioni di configurazione e valori di proprietà validi.|  
|PreExecute|Il componente esegue un'unica elaborazione prima di iniziare a elaborare le righe di dati.|  
|PostExecute|Il componente esegue un'unica elaborazione dopo avere elaborato tutte le righe di dati.|  
|ProcessInput|Il componente di destinazione o di trasformazione elabora le righe di dati in ingresso ricevute da un'origine o da una trasformazione a monte.|  
|PrimeOutput|Il componente di origine o di trasformazione riempie i buffer di dati da passare a un componente di destinazione o di trasformazione a valle.|  
  
 Quando si abilita l'evento PipelineComponentTime, in [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] viene registrato un messaggio per ogni passaggio dell'elaborazione eseguito da ogni componente. Nelle voci di log seguenti viene illustrato un subset dei messaggi registrati dal pacchetto di esempio CalculatedColumns di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] :  
  
 `The component "Calculate LineItemTotalCost" (3522) spent 356 milliseconds in ProcessInput.`  
  
 `The component "Sum Quantity and LineItemTotalCost" (3619) spent 79 milliseconds in ProcessInput.`  
  
 `The component "Calculate Average Cost" (3662) spent 16 milliseconds in ProcessInput.`  
  
 `The component "Sort by ProductID" (3717) spent 125 milliseconds in ProcessInput.`  
  
 `The component "Load Data" (3773) spent 0 milliseconds in ProcessInput.`  
  
 `The component "Extract Data" (3869) spent 688 milliseconds in PrimeOutput filling buffers on output "OLE DB Source Output" (3879).`  
  
 `The component "Sum Quantity and LineItemTotalCost" (3619) spent 141 milliseconds in PrimeOutput filling buffers on output "Aggregate Output 1" (3621).`  
  
 `The component "Sort by ProductID" (3717) spent 16 milliseconds in PrimeOutput filling buffers on output "Sort Output" (3719).`  
  
 Queste voci di log indicano che l'attività Flusso di dati ha dedicato la maggior parte del tempo ai passaggi seguenti, riportati in ordine decrescente:  
  
-   L'origine OLE DB denominata "Extract Data" ha dedicato 688 ms al caricamento dei dati.  
  
-   La trasformazione Colonna derivata denominata "Calculate LineItemTotalCost" ha dedicato 356 ms per l'esecuzione dei calcoli sulle righe in ingresso.  
  
-   La trasformazione Aggregazione denominata "Sum Quantity and LineItemTotalCost" ha dedicato in tutto 220 ms (141 per PrimeOutput e 79 per ProcessInput) per l'esecuzione di calcoli e il passaggio di dati alla trasformazione successiva.  
  
## <a name="related-tasks"></a>Attività correlate  
 Nell'elenco seguente sono contenuti collegamenti ad argomenti che illustrano come eseguire attività correlate alla funzionalità di registrazione.  
  
-   [Configura log SSIS - finestra di dialogo](../configure-ssis-logs-dialog-box.md)  
  
-   [Abilitare la registrazione di pacchetti in SQL Server Data Tools](../enable-package-logging-in-sql-server-data-tools.md)  
  
-   [Abilitare la registrazione per l'esecuzione di pacchetti nel server SSIS](../enable-logging-for-package-execution-on-the-ssis-server.md)  
  
-   [Visualizzare le voci di log nella finestra Registra eventi](../view-log-entries-in-the-log-events-window.md)  
  
## <a name="related-content"></a>Contenuto correlato  
 [Strumento DTLoggedExec per la registrazione completa e dettagliata (progetto CodePlex)](https://go.microsoft.com/fwlink/?LinkId=150579)  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare le voci di log nella finestra Registra eventi](../view-log-entries-in-the-log-events-window.md)  
  
  
