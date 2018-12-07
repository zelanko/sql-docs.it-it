---
title: Utilità dtexec | Microsoft Docs
ms.custom: ''
ms.date: 08/26/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 7b6867fa-1039-49b3-90fb-85b84678a612
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bcbef7c771d402d1532ecaece4426666920f785b
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52513387"
---
# <a name="dtexec-utility"></a>Utilità dtexec
  L'utilità del prompt dei comandi **dtexec** viene usata per configurare ed eseguire i pacchetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Con l'utilità **dtexec** è possibile accedere a tutte le funzionalità di configurazione ed esecuzione dei pacchetti, ad esempio parametri, connessioni, proprietà, variabili, registrazione e indicatori di stato. L'utilità **dtexec** consente di caricare i pacchetti da queste origini: server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , file di progetto con estensione ispac, database di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , archivio pacchetti [!INCLUDE[ssIS](../../includes/ssis-md.md)] e file system.  
  
> **NOTA:** quando si usa la versione corrente dell'utilità **dtexec** per eseguire un pacchetto creato tramite una versione precedente di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], l'utilità aggiorna temporaneamente il pacchetto al formato di pacchetto corrente. Tuttavia, non è possibile usare l'utilità **dtexec** per salvare il pacchetto aggiornato. Per altre informazioni su come rendere permanente l'aggiornamento di un pacchetto alla versione corrente, vedere [Upgrade Integration Services Packages](../../integration-services/install-windows/upgrade-integration-services-packages.md).  
  
 In questo argomento sono contenute le sezioni seguenti:  
  
-   [Server Integration Services e file di progetto](#server)  
  
-   [Considerazioni sull'installazione in computer a 64 bit](#bit)  
  
-   [Considerazioni sui computer con installazioni side-by-side](#side)  
  
-   [Fasi di esecuzione](#phases)  
  
-   [Codici di uscita restituiti](#exit)  
  
-   [Regole della sintassi](#syntaxRules)  
  
-   [Utilizzo di dtexec da xp_cmdshell](#cmdshell)  
  
-   [Sintassi](#syntax)  
  
-   [Parametri](#parameter)  
  
-   [Osservazioni](#remark)  
  
-   [Esempi](#example)  
  
##  <a name="server"></a> Server Integration Services e file di progetto  
 Quando si usa **dtexec** per eseguire pacchetti nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], **dtexec** chiama le stored procedure [catalog.create_execution &#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md), [catalog.set_execution_parameter_value &#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md) e [catalog.start_execution &#40;SSISDB Database&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md) per creare un'esecuzione, impostare i valori dei parametri e avviare l'esecuzione. Tutti i log di esecuzione possono essere visualizzati dal server nelle viste correlate o tramite report standard disponibili in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Per altre informazioni sui report, vedere [Report per il server Integration Services](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports).  
  
 Di seguito è riportato un esempio relativo all'esecuzione di un pacchetto nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
```  
DTExec /ISSERVER "\SSISDB\folderB\Integration Services Project17\Package.dtsx" /SERVER "." /Envreference 2 /Par "$Project::ProjectParameter(Int32)";1 /Par "Parameter(Int32)";21 /Par "CM.sqlcldb2.SSIS_repro.InitialCatalog";ssisdb /Par "$ServerOption::SYNCHRONIZED(Boolean)";True  
```  
  
 Quando si usa **dtexec** per eseguire un pacchetto dal file di progetto con estensione ispac, le opzioni correlate sono /Proj[ect] e /Pack[age] utilizzate per specificare il percorso del progetto e il nome di flusso del pacchetto. Quando si converte un progetto nel modello di distribuzione del progetto eseguendo la **Conversione guidata progetto di Integration Services** da [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], tramite la procedura guidata viene generato un file di progetto con estensione ispac. Per altre informazioni, vedere [Distribuire progetti e pacchetti di Integration Services (SSIS)](../../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md).  
  
 È possibile usare **dtexec** con gli strumenti di pianificazione di terze parti per pianificare i pacchetti distribuiti nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
##  <a name="bit"></a> Considerazioni sull'installazione in computer a 64 bit  
 In un computer a 64 bit, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] installa una versione a 64 bit dell'utilità **dtexec** (dtexec.exe). Se è necessario eseguire alcuni pacchetti nella modalità a 32 bit, installare la versione a 32 bit dell'utilità **dtexec** . Per installare la versione a 32 bit dell'utilità **dtexec** , è necessario selezionare gli strumenti client o [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] durante l'installazione.  
  
 Per impostazione predefinita, un computer a 64 bit contenente le versioni a 64 bit e a 32 bit di un'utilità del prompt dei comandi di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] installata eseguirà la versione a 32 bit al prompt dei comandi. Viene eseguita la versione a 32 bit perché il percorso della directory della versione a 32 bit compare nella variabile di ambiente PATH prima del percorso della directory della versione a 64 bit. In genere, il percorso della directory a 32 bit è *\<unità>*:\Programmi (x86) \Microsoft SQL Server\110\DTS\Binn, mentre il percorso della directory a 64 bit è *\<unità>*:\Programmi\Microsoft SQL Server\110\DTS\Binn.  
  
> **NOTA:** se si usa SQL Server Agent per eseguire l'utilità, SQL Server Agent usa automaticamente la versione a 64 bit dell'utilità. Per trovare l'eseguibile corretto per l'utilità, SQL Server Agent utilizza il Registro di sistema, non la variabile di ambiente PATH.  
  
 Per assicurarsi di eseguire la versione a 64 bit dell'utilità al prompt dei comandi, è possibile eseguire una delle azioni seguenti:  
  
-   Aprire una finestra del prompt dei comandi, accedere alla directory che contiene la versione a 64 bit dell'utilità, *\<unità>*:\Programmi\Microsoft SQL Server\110\DTS\Binn, quindi eseguire l'utilità da quel percorso.  
  
-   Al prompt dei comandi eseguire l'utilità immettendo il percorso completo (*\<unità>*:\Programmi\Microsoft SQL Server\110\DTS\Binn) della versione a 64 bit dell'utilità.  
  
-   Modificare in modo definitivo l'ordine dei percorsi nella variabile di ambiente PATH spostando il percorso della versione a 64 bit (*\<unità>*:\Programmi\Microsoft SQL Server\110\DTS\Binn) prima del percorso della versione a 32 bit (*\<unità>*:\Programmi(x86)\Microsoft SQL Server\110\DTS\Binn).  
  
##  <a name="side"></a> Considerazioni sui computer con installazioni side-by-side  
 Se [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] è installato in un computer con [!INCLUDE[ssISversion2005](../../includes/ssisversion2005-md.md)] o [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] , vengono installate più versioni dell'utilità **dtexec** .  
  
 Per assicurarsi di eseguire la versione corretta dell'utilità, al prompt dei comandi eseguirla immettendo il percorso completo (*\<unità>*:\Programmi\Microsoft SQL Server\\<versione\>\DTS\Binn).  
  
##  <a name="phases"></a> Fasi di esecuzione  
 L'esecuzione di questa utilità si articola nelle quattro fasi descritte di seguito.  
  
1.  Determinazione dell'origine del comando: il prompt dei comandi legge l'elenco delle opzioni e degli argomenti specificati. Tutte le fasi successive vengono ignorate se viene rilevata un'opzione **/?** o **/HELP** .  
  
2.  Caricamento dei pacchetti: viene caricato il pacchetto specificato dall'opzione **/SQL**, **/FILE**o **/DTS** .  
  
3.  Configurazione: le opzioni vengono elaborate nell'ordine riportato di seguito.  
  
    -   Opzioni che impostano i flag, le variabili e le proprietà dei pacchetti.  
  
    -   Opzioni che verificano la versione e la build del pacchetto.  
  
    -   Opzioni che configurano il comportamento dell'utilità in fase di esecuzione, ad esempio la creazione di report.  
  
4.  Convalida ed esecuzione: il pacchetto viene eseguito oppure convalidato ma non eseguito se è stata specificata l'opzione **/VALIDATE** .  
  
##  <a name="exit"></a> Codici di uscita restituiti  
 **Codici di uscita restituiti dall'utilità dtexec**  
  
 Durante l'esecuzione di un pacchetto è possibile che **dtexec** restituisca un codice di uscita. Il codice di uscita viene utilizzato per popolare la variabile ERRORLEVEL, il cui valore può essere testato nelle istruzioni condizionali o nella logica di diramazione in un file batch. Nella tabella seguente vengono elencati i valori che l'utilità **dtexec** può impostare all'uscita.  
  
|valore|Descrizione|  
|-----------|-----------------|  
|0|Il pacchetto è stato eseguito correttamente.|  
|1|Il pacchetto non è stato eseguito.|  
|3|L'esecuzione del pacchetto è stata annullata dall'utente.|  
|4|L'utilità non è stata in grado di individuare il pacchetto richiesto. Risulta impossibile trovare il pacchetto.|  
|5|L'utilità non è stata in grado di caricare il pacchetto richiesto. Risulta impossibile caricare il pacchetto.|  
|6|L'utilità ha rilevato un errore interno oppure un errore sintattico o semantico nella riga di comando.|  
  
##  <a name="syntaxRules"></a> Regole della sintassi  
 **Regole di sintassi dell'utilità**  
  
 Tutte le opzioni devono essere precedute da una barra (/) o un segno meno (-). Le opzioni riportate di seguito sono precedute da una barra (/), che può tuttavia essere sostituita dal segno meno (-).  
  
 Se l'argomento contiene uno spazio, deve essere racchiuso tra virgolette. Se non è racchiuso tra virgolette, un argomento non può contenere spazi vuoti.  
  
 Le virgolette doppie all'interno di stringhe racchiuse tra virgolette rappresentano virgolette singole di escape.  
  
 Le opzioni e gli argomenti, escluse le password, non fanno distinzione tra maiuscole e minuscole.  
  
##  <a name="cmdshell"></a> Utilizzo di dtexec da xp_cmdshell  
 **Utilizzo di dtexec da xp_cmdshell**  
  
 È possibile eseguire dtexec dal prompt di **xp_cmdshell** . Nell'esempio seguente viene illustrato come eseguire un pacchetto denominato UpsertData.dtsx e ignorare il codice restituito:  
  
```  
EXEC xp_cmdshell 'dtexec /f "C:\UpsertData.dtsx"'  
```  
  
 Nell'esempio seguente viene illustrato come eseguire lo stesso pacchetto e acquisire il codice restituito:  
  
```  
DECLARE @returncode int  
EXEC @returncode = xp_cmdshell 'dtexec /f "C:\UpsertData.dtsx"'  
```  
  
> **IMPORTANTE** Nelle nuove installazioni, in [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]l'opzione **xp_cmdshell** risulta disabilitata per impostazione predefinita. L'opzione può essere abilitata eseguendo la stored procedure di sistema **sp_configure** . Per altre informazioni, vedere [Opzione di configurazione del server xp_cmdshell](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md).  
  
##  <a name="syntax"></a> Sintassi  
  
```  
dtexec /option [value] [/option [value]]...  
```  
  
##  <a name="parameter"></a> Parametri  
  
-   **/?** [*option_name*]: (facoltativo). Consente di visualizzare le opzioni del prompt dei comandi o le informazioni della Guida relative all'opzione *option_name* specificata e quindi di chiudere l'utilità.  
  
     Se si specifica un argomento *option_name*, **dtexec** avvia la documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e visualizza l'argomento relativo all'utilità dtexec.  
  
-   **/Ca[llerInfo]**: (facoltativo). Specifica informazioni aggiuntive per l'esecuzione di un pacchetto. Quando si esegue un pacchetto utilizzando SQL Server Agent, tramite l'agente è possibile impostare questo argomento per specificare che l'esecuzione del pacchetto venga richiamata da SQL Server Agent. Questo parametro viene ignorato quando l'utilità **dtexec** viene eseguita dalla riga di comando.  
  
-   **/CheckF[ile]** *filespec*: (facoltativo). Imposta la proprietà **CheckpointFileName** del pacchetto sul percorso e sul file specificati in *filespec*. Questo file viene utilizzato quando il pacchetto viene riavviato. Se si specifica questa opzione ma si omette il valore del nome file, la proprietà **CheckpointFileName** del pacchetto viene impostata su una stringa vuota. Se si omette questa opzione, i valori nel pacchetto vengono conservati.  
  
-   **/CheckP[ointing]** *{on\off}* : (facoltativo). Consente di impostare un valore che determina se il pacchetto utilizzerà i checkpoint durante l'esecuzione. Il valore **on** indica che un pacchetto la cui esecuzione ha avuto esito negativo deve essere rieseguito. In questo caso, il motore di run-time utilizza il file del checkpoint per riavviare il pacchetto dal punto in cui si è verificato l'errore.  
  
     Il valore predefinito è on se l'opzione viene dichiarata senza un valore. L'esecuzione del pacchetto avrà esito negativo se il valore viene impostato su on, ma non risulta possibile trovare il file del checkpoint. Se si omette questa opzione, il valore impostato nel pacchetto viene conservato. Per ulteriori informazioni, vedere [Restart Packages by Using Checkpoints](../../integration-services/packages/restart-packages-by-using-checkpoints.md).  
  
     L'opzione **/CheckPointing on** di dtexec equivale a impostare la proprietà **SaveCheckpoints** del pacchetto su True e la proprietà **CheckpointUsage** su Always.  
  
-   **/Com[mandFile]** *filespec*: (facoltativo). Specifica le opzioni di comando eseguite con **dtexec**. Il file specificato in *filespec* viene aperto e le relative opzioni vengono lette finché non viene rilevata la fine del file. *filespec* è un file di testo. L'argomento *filespec* consente di specificare il nome e il percorso del file di comando da associare all'esecuzione del pacchetto.  
  
-   **/Conf[igFile]** *filespec*: (facoltativo). Consente di specificare un file di configurazione da cui estrarre valori. Se si utilizza questa opzione, è possibile impostare una configurazione della fase di esecuzione diversa rispetto alla configurazione specificata in fase di progettazione per il pacchetto. È possibile archiviare impostazioni di configurazione diverse in un file di configurazione XML e quindi caricare tali impostazioni tramite l'opzione **/ConfigFile** prima dell'esecuzione del pacchetto.  
  
     È possibile usare l'opzione **/ConfigFile** per caricare in fase di esecuzione configurazioni aggiuntive non specificate in fase di progettazione. Non è tuttavia possibile usare l'opzione **/ConfigFile** per sostituire valori configurati specificati anche in fase di progettazione. Per informazioni sull'applicazione delle configurazioni dei pacchetti, vedere [Package Configurations](../../integration-services/packages/package-configurations.md).  
  
-   **/Conn[ection]** *id_or_name;connection_string [[;id_or_name;connection_string]...]*: (facoltativo). Consente di specificare che la gestione connessione con il nome o il GUID indicato si trova nel pacchetto e che è stata specificata una stringa di connessione.  
  
     Questa opzione richiede che vengano specificati entrambi i parametri: il nome o il GUID della gestione connessione deve essere specificato nell'argomento *id_or_name*, mentre nell'argomento *connection_string* deve essere specificata una stringa di connessione valida. Per altre informazioni, vedere [Connessioni in Integration Services &#40;SSIS&#41;](../../integration-services/connection-manager/integration-services-ssis-connections.md).  
  
     In fase di esecuzione è possibile usare l'opzione **/Connection** per caricare le configurazioni di pacchetto da una posizione diversa da quella specificata in fase di progettazione. I valori di queste configurazioni sostituiscono i valori specificati in origine. È tuttavia possibile usare l'opzione **/Connection** solo per le configurazioni che usano una gestione connessione, ad esempio le configurazioni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per capire come sono applicate le configurazioni dei pacchetti, vedere [Configurazioni di pacchetto](../../integration-services/packages/package-configurations.md) e [Differenze di funzionamento delle funzionalità di Integration Services in SQL Server 2016](https://msdn.microsoft.com/library/611d22fa-5ac7-485e-9a40-7131e852f794).  
  
-   **/Cons[oleLog]** [[*displayoptions*];[*list_options*;*src_name_or_guid*]...]: (facoltativo). Consente di visualizzare le voci di log specificate nella console durante l'esecuzione del pacchetto. Se questa opzione viene omessa, non verrà visualizzata alcuna voce di log nella console. Se si specifica l'opzione senza tuttavia alcun parametro per limitare la visualizzazione, verrà visualizzata ogni voce di log. Per limitare il numero di voci visualizzate nella console, è possibile specificare le colonne da visualizzare tramite il parametro *displayoptions* e limitare i tipi di voci di log tramite il parametro *list_options* .  
  
    > **NOTA:**  quando si esegue un pacchetto nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usando il parametro **S/ISSERVER** , l'output della console è limitato e la maggior parte delle opzioni **/Cons[oleLog]** non è applicabile. Tutti i log di esecuzione possono essere visualizzati dal server nelle viste correlate o tramite report standard disponibili in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Per altre informazioni sui report, vedere [Report per il server Integration Services](../../integration-services/performance/monitor-running-packages-and-other-operations.md#reports).  
  
     Sono disponibili i valori *displayoptions* seguenti:  
  
    -   N (Name)  
  
    -   C (Computer)  
  
    -   O (Operator)  
  
    -   S (Source Name)  
  
    -   G (Source GUID)  
  
    -   X (Execution GUID)  
  
    -   M (Message)  
  
    -   T (Time Start and End)  
  
     Sono disponibili i valori *list_options* seguenti:  
  
    -   *I* - Specifica l'elenco di inclusione. Solo i nomi o i GUID delle origini specificati vengono registrati.  
  
    -   *E* - Specifica l'elenco di esclusione. I nomi o i GUID delle origini specificati non vengono registrati.  
  
    -   Il parametro *src_name_or_guid* specificato per inclusioni o esclusioni è un nome di evento o un nome o un GUID dell'origine.  
  
     Se nello stesso prompt dei comandi si usano più opzioni **/ConsoleLog** , queste interagiscono nel modo di seguito descritto:  
  
    -   L'ordine di visualizzazione non è significativo.  
  
    -   Se nella riga di comando non sono presenti elenchi di inclusioni, gli elenchi di esclusioni vengono applicati a tutti i tipi di voci di log.  
  
    -   Se nella riga di comando sono presenti elenchi di inclusione, all'unione di tutti gli elenchi di inclusione vengono applicati gli elenchi di esclusione.  
  
     Per esempi relativi all'opzione **/ConsoleLog** , vedere la sezione **Osservazioni** .  
  
--   **/D[ts]** *package_path*: (facoltativo). Carica un pacchetto dall'archivio pacchetti SSIS. I pacchetti archiviati nell'archivio pacchetti SSIS vengono distribuiti tramite il modello di distribuzione del pacchetto legacy. Per eseguire i pacchetti distribuiti nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] tramite il modello di distribuzione del progetto, usare l'opzione **/ISServer**. Per ulteriori informazioni sui modelli di distribuzione del pacchetto e del progetto, vedere [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx).  
  
     The *package_path* argument specifies the relative path of the [!INCLUDE[ssIS](../../includes/ssis-md.md)] package, starting at the root of the SSIS Package Store, and includes the name of the [!INCLUDE[ssIS](../../includes/ssis-md.md)] package. If the path or file name specified in the *package_path* argument contains a space, you must put quotation marks around the *package_path* argument.  
  
     The **/DTS** option cannot be used together with the **/File** or **/SQL** option. If multiple options are specified, **dtexec** fails.  
  
-   **/De[crypt]**  *password*: (facoltativo). Consente di impostare la password di decrittografia utilizzata per caricare un pacchetto con password crittografata.  
  
-   (Facoltativo) Consente di creare i file di dump del debug, con estensione MDMP e TMP, quando si verificano uno o più eventi specificati durante l'esecuzione del pacchetto. L'argomento *error code* specifica il tipo di codice evento (errore, avviso o informazione) che genera la creazione di file di dump del debug. Per specificare più codici evento, separare ciascun argomento *error code* con un punto e virgola (;). Non includere virgolette con l'argomento *error code* .  
  
     Nell'esempio seguente vengono generati i file di dump del debug se si verifica l'errore DTS_E_CANNOTACQUIRECONNECTIONFROMCONNECTIONMANAGER.  
  
    ```  
    /Dump 0xC020801C  
    ```  
  
     **/Dump** *error code*: per impostazione predefinita, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] archivia i file di dump del debug nella cartella *\<unità>*:\Programmi\Microsoft SQL Server\110\Shared\ErrorDumps.  
  
    > **NOTA:** i file di dump del debug possono contenere informazioni riservate. Utilizzare un elenco di controllo di accesso (ACL) per limitare l'accesso ai file oppure copiare i file in una cartella con accesso limitato. Ad esempio, prima di inviare i file del debug al supporto tecnico Microsoft, si consiglia di rimuovere eventuali informazioni sensibili o riservate.  
  
     Per applicare questa opzione a tutti i pacchetti eseguiti dall'utilità **dtexec** , aggiungere un valore REG_SZ **DumpOnCodes** alla chiave del registro di sistema HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS\Setup\DtsPath. Il valore dei dati in **DumpOnCodes** specifica il codice di errore o i codici che generano la creazione di file di dump del debug da parte del sistema. Più codici di errore devono essere separati da un punto e virgola (;).  
  
     Se si aggiunge un valore **DumpOnCodes** alla chiave del registro di sistema e si usa l'opzione **/Dump** , il sistema crea file di dump del debug basati su entrambe le impostazioni.  
  
     Per ulteriori informazioni sui file di dump del debug, vedere [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md).  
  
-   **/DumpOnError**: (facoltativo). Consente di creare i file di dump del debug, con estensione mdmp e tpm, quando si verifica un errore durante l'esecuzione del pacchetto.  
  
     Per impostazione predefinita, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] archivia i file di dump del debug nella cartella *\<unità>*:\Programmi\Microsoft SQL Server\110\Shared\ErrorDumps.  
  
    > **NOTA:** i file di dump del debug possono contenere informazioni riservate. Utilizzare un elenco di controllo di accesso (ACL) per limitare l'accesso ai file oppure copiare i file in una cartella con accesso limitato. Ad esempio, prima di inviare i file del debug al supporto tecnico Microsoft, si consiglia di rimuovere eventuali informazioni sensibili o riservate.  
  
     Per applicare questa opzione a tutti i pacchetti eseguiti dall'utilità **dtexec** , aggiungere un valore REG_DWORD **DumpOnError** alla chiave del registro di sistema HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft SQL Server\110\SSIS\Setup\DtsPath. Il valore REG_DWORD **DumpOnError** determina se è necessario usare l'opzione **/DumpOnError** con l'utilità **dtexec** :  
  
    -   Un valore dei dati diverso da zero indica che verranno creati file di dump del debug quando si verifica un errore, indipendentemente dall'uso dell'opzione **/DumpOnError** con l'utilità **dtexec** .  
  
    -   Un valore dei dati pari a zero indica che non verranno creati file di dump del debug a meno che non venga usata l'opzione **/DumpOnError** con l'utilità **dtexec** .  
  
     Per ulteriori informazioni sui file di dump del debug, vedere [Generating Dump Files for Package Execution](../../integration-services/troubleshooting/generating-dump-files-for-package-execution.md).  
  
-   **/Env[Reference]** *environment reference ID*: (facoltativo). Specifica il riferimento all'ambiente (ID) utilizzato dall'esecuzione del pacchetto, per un pacchetto distribuito nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Nei parametri configurati per l'associazione alle variabili verranno utilizzati i valori delle variabili contenuti nell'ambiente.  
  
     Usare l'opzione **/Env[Reference]** insieme alle opzioni **/ISServer** e **/Server** .  
  
     Questo parametro viene utilizzato da SQL Server Agent.  
  --   **/F[ile]** *filespec*: (facoltativo). Carica un pacchetto salvato nel file system. I pacchetti salvati nel file system vengono distribuiti tramite il modello di distribuzione del pacchetto legacy. Per eseguire i pacchetti distribuiti nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] tramite il modello di distribuzione del progetto, usare l'opzione **/ISServer** . Per ulteriori informazioni sui modelli di distribuzione del pacchetto e del progetto, vedere [Deployment of Projects and Packages](deploy-integration-services-ssis-projects-and-packages.md).  

  L'argomento *filespec* specifica il percorso e il nome file del pacchetto. È possibile specificare il percorso in formato UNC (Universal Naming Convention) o come percorso locale. Se nel percorso o nel nome file specificato nell'argomento *filespec* è contenuto uno spazio, è necessario racchiudere l'argomento *filespec* tra virgolette.  
  
     L'opzione **/File** non può essere usata in combinazione con l'opzione **/DTS** o **/SQL** . Se si specificano più opzioni, l'esecuzione di **dtexec** avrà esito negativo.  
  
-   **/H[elp]** [*option_name*]: (facoltativo). Consente di visualizzare le informazioni della Guida relative alle opzioni o all'opzione specificata dall'argomento *option_name* e quindi di chiudere l'utilità.  
  
     Se si specifica un argomento *option_name* , **dtexec** avvia la documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e visualizza l'argomento relativo all'utilità dtexec.  
  
-   **/ISServer** *packagepath*: (facoltativo). Esegue un pacchetto distribuito nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Con l'argomento *PackagePath* vengono specificati il percorso completo e il nome file del pacchetto distribuito nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Se nel percorso o nel nome file specificato nell'argomento *PackagePath* è contenuto uno spazio, è necessario racchiudere l'argomento *PackagePath* tra virgolette.  
  
     Il formato del pacchetto è il seguente:  
  
    ```  
    \<catalog name>\<folder name>\<project name>\package file name  
    ```  
  
     Usare l'opzione **/Server** insieme all'opzione **/ISSERVER** . Un pacchetto nel server SSIS può essere eseguito solo con l'autenticazione di Windows. Per accedere al pacchetto viene utilizzato l'utente corrente di Windows. Se si omette l'opzione /Server, viene usata l'istanza locale predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     L'opzione **/ISSERVER** non può essere usata in combinazione con l'opzione **/DTS**, **/SQL** o **/File** . Se si specificano più opzioni, l'esecuzione di dtexec avrà esito negativo.  
  
     Questo parametro viene utilizzato da SQL Server Agent.  
  
-   **/L[ogger]** *classid_orprogid;configstring*: (facoltativo). Associa uno o più provider di log all'esecuzione di un pacchetto di [!INCLUDE[ssIS](../../includes/ssis-md.md)] . Il parametro *classid_orprogid* specifica il provider di log e può essere specificato come un GUID di classe. L'argomento *configstring* è la stringa utilizzata per configurare il provider di log.  
  
     Di seguito sono elencati i provider di log disponibili:  
  
    -   File di testo  
  
        -   ProgID: DTS.LogProviderTextFile.1  
  
        -   ClassID: {59B2C6A5-663F-4C20-8863-C83F9B72E2EB}  
  
    -   [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]:  
  
        -   ProgID: DTS.LogProviderSQLProfiler.1  
  
        -   ClassID: {5C0B8D21-E9AA-462E-BA34-30FF5F7A42A1}  
  
    -   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
        -   ProgID: DTS.LogProviderSQLServer.1  
  
        -   ClassID: {6AA833A1-E4B2-4431-831B-DE695049DC61}  
  
    -   Registro eventi di Windows  
  
        -   ProgID: DTS.LogProviderEventLog.1  
  
        -   ClassID: {97634F75-1DC7-4F1F-8A4C-DAF0E13AAA22}  
  
    -   File XML  
  
        -   ProgID: DTS.LogProviderXMLFile.1  
  
        -   ClassID: {AFED6884-619C-484F-9A09-F42D56E1A7EA}  
  
-   **/M[axConcurrent]** *concurrent_executables*: (facoltativo). Consente di specificare il numero di file eseguibili che il pacchetto è in grado di eseguire contemporaneamente. Il valore specificato deve essere un valore intero non negativo oppure -1. Il valore -1 indica che [!INCLUDE[ssIS](../../includes/ssis-md.md)] supporta un numero massimo di file eseguibili in esecuzione simultanea uguale al numero totale di processori nel computer in cui è eseguito il pacchetto, più due.  
  
-   **/Pack[age]** *PackageName*: (facoltativo). Specifica il pacchetto che viene eseguito. Questo parametro viene utilizzato principalmente quando si esegue il pacchetto da [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
-   **/P[assword]** *password*: (facoltativo). Consente il recupero di un pacchetto protetto tramite l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Questa opzione viene usata in combinazione con l'opzione **/User** . Se si omette l'opzione **/Password** e viene usata l'opzione **/User** , verrà usata una password vuota. Il valore di *password* può essere racchiuso tra virgolette.  
  
    > **IMPORTANTE** [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
-   **/Par[ameter]** [$Package:: | $Project:: | $ServerOption::] *parameter_name* [(data_type)]; *literal_value*: (facoltativo). Specifica i valori dei parametri. È possibile specificare più opzioni **/Parameter** . I tipi di dati sono CLR TypeCodes come stringhe. Per un parametro non stringa, il tipo di dati viene specificato in parentesi, dopo il nome del parametro.  
  
     L'opzione **/Parameter** può essere specificata solo con l'opzione **/ISServer** .  
  
     È possibile utilizzare i prefissi $Package, $Project e $ServerOption per indicare rispettivamente un parametro di pacchetto, un parametro di progetto e un parametro di opzione server. Il pacchetto è il tipo di parametro predefinito.  
  
     Di seguito è riportato un esempio relativo all'esecuzione di un pacchetto e all'impostazione di myvalue per il parametro di progetto (myparam) e del valore intero 12 per il parametro di pacchetto (anotherparam).  
  
     `Dtexec /isserver "SSISDB\MyFolder\MyProject\MyPackage.dtsx" /server "." /parameter $Project::myparam;myvalue /parameter anotherparam(int32);12`  
  
     È inoltre possibile impostare le proprietà di gestione connessione utilizzando i parametri. Per identificare un parametro di gestione connessione utilizzare il prefisso CM.  
  
     Nell'esempio seguente la proprietà InitialCatalog della gestione connessione SourceServer è impostata su `ssisdb`.  
  
    ```  
    /parameter CM.SourceServer.InitialCatalog;ssisdb  
    ```  
  
     Nell'esempio seguente la proprietà ServerName della gestione connessione SourceServer è impostata su un punto (.) per indicare il server locale.  
  
    ```  
    /parameter CM.SourceServer.ServerName;.  
    ```  
  
-   **/Proj[ect]** *ProjectFile*: (facoltativo). Specifica il progetto da cui recuperare il pacchetto che viene eseguito. Con l'argomento *ProjectFile* viene specificato il nome file con estensione ispac. Questo parametro viene utilizzato principalmente quando si esegue il pacchetto da [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)].  
  
-   **/Rem** *comment*: (facoltativo). Include i commenti nel prompt dei comandi o nei file di comando. L'argomento è facoltativo. Il valore di *comment* è una stringa che deve essere racchiusa tra virgolette o non deve contenere spazi. Se non si specifica alcun argomento, viene inserita una riga vuota. Durante la fase di determinazione dell'origine del comando, i valori*comment* vengono eliminati.  
  
-   **/Rep[orting]** *level* [*;event_guid_or_name*[*;event_guid_or_name*[...]]: (facoltativo). Specifica i tipi di messaggi da segnalare. Le opzioni relative alle opzioni per *level* sono elencate di seguito:  
  
     **N** Nessun report.  
  
     **E** Gli errori vengono segnalati.  
  
     **W** Gli avvisi vengono segnalati.  
  
     **I** I messaggi informativi vengono segnalati.  
  
     **C** Gli eventi personalizzati vengono segnalati.  
  
     **D** Gli eventi relativi alle attività Flusso di dati vengono segnalati.  
  
     **P** Lo stato viene segnalato.  
  
     **V** Report dettagliati.  
  
     Gli argomenti V e N escludono tutti gli altri argomenti e pertanto devono essere specificati da soli. Se non si specifica l'opzione **/Reporting** , il livello predefinito è **E** (errori), **W** (avvisi) e **P** (stato).  
  
     Tutti gli eventi sono preceduti da un timestamp nel formato "AA/MM/GG HH:MM:SS" e da un GUID o un nome descrittivo se disponibile.  
  
     Il parametro facoltativo *event_guid_or_name* è un elenco di eccezioni per i provider di log. ovvero gli eventi da non registrare che potrebbero altrimenti essere stati registrati.  
  
     Non è necessario escludere un evento se normalmente non viene registrato per impostazione predefinita.  
  
-   **/Res[tart]** {*deny | force | ifPossible*}: (facoltativo). Specifica un nuovo valore per la proprietà <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> nel pacchetto. Di seguito è descritto il significato di ogni parametro.  
  
     *Deny* Imposta la proprietà <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> su <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSCheckpointUsage.DTSCU_NEVER>.  
  
     *Force* Imposta la proprietà <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> su <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSCheckpointUsage.DTSCU_ALWAYS>.  
  
     *ifPossible* Imposta la proprietà <xref:Microsoft.SqlServer.Dts.Runtime.Package.CheckpointUsage%2A> su <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.DTSCheckpointUsage.DTSCU_IFEXISTS>.  
  
     Se non si specifica alcun valore, viene usato il valore predefinito **force** .  
  
-   **/Set** [$Sensitive::]*propertyPath;value*: (facoltativo). Ignora la configurazione di un parametro, una variabile, una proprietà, un contenitore, un provider di log, un enumeratore Foreach o una connessione all'interno di un pacchetto. Se si specifica questa opzione, **/Set** modifica il valore dell'argomento *propertyPath* nel valore specificato. È possibile specificare più opzioni **/Set** .  
  
     Oltre a usare l'opzione **/Set** con l'opzione **/F[ile]** , è anche possibile usare **/Set** con l'opzione **/ISServer** o **/Project** . Quando si usa **/Set** con **/Project**, **/Set** imposta i valori dei parametri. Quando si usa **/Set** con **/ISServer**, **/Set** imposta gli override delle proprietà. Quando **/Set** viene usata con **/ISServer**, è possibile anche usare il prefisso facoltativo $Sensitive per indicare che la proprietà è sensibile nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
     È possibile determinare il valore di *propertyPath* eseguendo la Configurazione guidata pacchetto. I percorsi per gli elementi selezionati vengono visualizzati nella pagina finale **Completamento procedura guidata** e possono essere copiati e incollati. Se si utilizza la procedura guidata soltanto a questo scopo, è possibile annullare la procedura guidata dopo aver copiato i percorsi.  
  
     Di seguito è riportato un esempio relativo all'esecuzione di un pacchetto salvato nel file system e all'impostazione di un nuovo valore per una variabile:  
  
     `dtexec /f mypackage.dtsx /set \package.variables[myvariable].Value;myvalue`  
  
     Di seguito è riportato un esempio relativo all'esecuzione di un pacchetto dal file di progetto con estensione ispac e all'impostazione dei parametri di pacchetto e di progetto.  
  
     `/Project c:\project.ispac /Package Package1.dtsx /SET \Package.Variables[$Package::Parameter];1 /SET \Package.Variables[$Project::Parameter];1`  
  
     È possibile usare l'opzione **/Set** per modificare il percorso da cui vengono caricate le configurazioni di pacchetto. Non è tuttavia possibile usare l'opzione **/Set** per ignorare un valore specificato da una configurazione in fase di progettazione. Per capire come sono applicate le configurazioni dei pacchetti, vedere [Configurazioni di pacchetto](../../integration-services/packages/package-configurations.md) e [Differenze di funzionamento delle funzionalità di Integration Services in SQL Server 2016](https://msdn.microsoft.com/library/611d22fa-5ac7-485e-9a40-7131e852f794).  
  
-   **/Ser[ver]** *server*: (facoltativo). Se si specifica l'opzione **/SQL** o **/DTS** , questa opzione specifica il nome del server dal quale recuperare il pacchetto. Se si omette l'opzione **/Server** e si specifica l'opzione **/SQL** o **/DTS** , verrà tentata l'esecuzione del pacchetto nel server locale. Il valore *server_instance* può essere racchiuso fra virgolette.  
  
     L'opzione **/Ser[ver]** è obbligatoria se è specificata l'opzione **/ISServer** .  
  
--   **/SQ[L]** *package_path*: carica un pacchetto archiviato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel database **msdb**. I pacchetti archiviati nel database **msdb** vengono distribuiti tramite il modello di distribuzione del pacchetto. Per eseguire i pacchetti distribuiti nel server [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] tramite il modello di distribuzione del progetto, usare l'opzione **/ISServer** . Per ulteriori informazioni sui modelli di distribuzione del pacchetto e del progetto, vedere [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx).   
  
     The *package_path* argument specifies the name of the package to retrieve. If folders are included in the path, they are terminated with backslashes ("\\"). The *package_path* value can be quoted. If the path or file name specified in the *package_path* argument contains a space, you must put quotation marks around the *package_path* argument.  
  
     You can use the **/User**, **/Password**, and **/Server** options together with the **/SQL** option.  
  
     If you omit the **/User** option, Windows Authentication is used to access the package. If you use the **/User** option, the **/User** login name specified is associated with [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Authentication.  
  
     The **/Password** option is used only together with the **/User** option. If you use the **/Password** option, the package is accessed with the user name and password information provided. If you omit the **/Password** option, a blank password is used.  
  
    > **IMPORTANT!!** [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
     If the **/Server** option is omitted, the default local instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] is assumed.  
  
     The **/SQL** option cannot be used together with the **/DTS** or **/File** option. If multiple options are specified, **dtexec** fails.  
  
-   **/Su[m]**: (facoltativo). Consente di visualizzare un contatore incrementale con il numero di righe che verranno ricevute dal componente successivo.  
  
-   **/U[ser]** *user_name*: (facoltativo). Consente il recupero di un pacchetto protetto tramite l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Questa opzione viene usata solo se si specifica l'opzione **/SQL** . Il valore *user_name* può essere racchiuso tra virgolette.  
  
    > **IMPORTANTE**  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
-   **/Va[lidate]**: (facoltativo). Consente di arrestare l'esecuzione del pacchetto dopo la fase di convalida, quindi il pacchetto non viene eseguito. Durante la convalida, se si usa l'opzione **/WarnAsError** l'utilità **dtexec** interpreta un avviso come un errore e pertanto il pacchetto viene chiuso se durante la convalida viene generato un avviso.  
  
-   **/VerifyB[uild]** *major*[*;minor*[*;build*]]: (facoltativo). Consente di verificare il numero di build di un pacchetto rispetto ai numeri di build specificati durante la fase di verifica negli argomenti *major*, *minor*e *build* . Se i numeri non corrispondono, il pacchetto non verrà eseguito.  
  
     I valori sono di tipo integer long. L'argomento può avere uno dei tre formati seguenti. Il valore *major* è sempre obbligatorio:  
  
    -   *major*  
  
    -   *major*;*minor*  
  
    -   *major*; *minor*; *build*  
  
-   **/VerifyP[ackageID]** *packageID*: (facoltativo). Consente di verificare il GUID del pacchetto da eseguire in base al valore specificato nell'argomento *package_id* .  
  
-   **/VerifyS[igned]**: (facoltativo). Comporta il controllo della firma digitale del pacchetto da parte di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Se il pacchetto non è firmato o se la firma non è valida, il pacchetto ha esito negativo. Per altre informazioni, vedere [Identificazione dell'origine dei pacchetti con firme digitali](../../integration-services/security/identify-the-source-of-packages-with-digital-signatures.md).  
  
    > **IMPORTANTE** Se [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è configurato per la verifica della firma del pacchetto, gli unici controlli che vengono eseguiti sono quelli relativi alla presenza e alla validità della firma digitale, nonché all'attendibilità dell'origine. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] non controlla se il pacchetto è stato modificato.  
  
    > **NOTA:** il valore facoltativo **BlockedSignatureStates** del Registro di sistema può specificare un'impostazione più restrittiva rispetto all'opzione per la firma digitale impostata in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] o nella riga di comando **dtexec** . In questo caso, l'impostazione del Registro di sistema più restrittiva ha la precedenza rispetto ad altre impostazioni.  
  
-   **/VerifyV[ersionID]** *versionID*: (facoltativo). Consente di verificare il GUID di versione di un pacchetto da eseguire in base al valore specificato nell'argomento *version_id* durante la fase di convalida del pacchetto.  
  
-   **/VLog** *[Filespec]*: (facoltativo). Consente di scrivere tutti gli eventi dei pacchetti Integration Services nei provider di log abilitati durante la progettazione del pacchetto. Per consentire l'abilitazione di un provider di log per i file di testo e la scrittura degli eventi del log in un file di testo specifico, includere un percorso e un nome file come parametro *Filespec* .  
  
     Se non si include il parametro *Filespec* , non sarà possibile abilitare un provider di log per i file di testo. Gli eventi del log verranno scritti solo nei provider di log abilitati durante la progettazione del pacchetto.  
  
-   **/W[arnAsError]**: (facoltativo). Poiché un avviso viene interpretato come un errore, il pacchetto non viene eseguito se durante la convalida viene generato un avviso. Se non viene generato alcun avviso durante la convalida e si omette l'opzione **/Validate** , il pacchetto viene eseguito.  
  
-   **/X86**: (facoltativo). Determina l'esecuzione del pacchetto in modalità a 32 bit in un computer a 64 bit da parte di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Questa opzione viene impostata da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent quando sono soddisfatte le condizioni seguenti:  
  
    -   Il tipo di passaggio del processo è **Pacchetto SQL Server Integration Services**.  
  
    -   L'opzione **Usa runtime a 32 bit** nella scheda **Opzioni di esecuzione** della finestra di dialogo **Nuovo passaggio di processo** è selezionata.  
  
     È anche possibile impostare questa opzione per un passaggio del processo di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent usando le stored procedure o SQL Server Management Objects (SMO) per creare il processo a livello di codice.  
  
     Questa opzione è utilizzata solo da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Questa opzione viene ignorata se si esegue l'utilità **dtexec** dal prompt dei comandi.  
  
##  <a name="remark"></a> Osservazioni  
 L'ordine in cui vengono specificate le opzioni del comando può influire sulla modalità di esecuzione del pacchetto:  
  
-   Le opzioni vengono elaborate nell'ordine che occupano nella riga di comando. I file di comando vengono letti in base all'ordine con cui vengono rilevati nella riga di comando, in modo analogo ai comandi nel file di comando.  
  
-   Se la stessa opzione, lo stesso parametro o la stessa variabile compare più volte nella stessa istruzione della riga di comando, l'ultima istanza dell'opzione avrà la precedenza sulle altre.  
  
-   Le opzioni **/Set** e **/ConfigFile** vengono elaborate nell'ordine in cui vengono rilevate.  
  
##  <a name="example"></a> Esempi  
 Gli esempi seguenti illustrano come usare l'utilità del prompt dei comandi **dtexec** per configurare ed eseguire i pacchetti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
 **Esecuzione di pacchetti**  
  
 Per eseguire un pacchetto di [!INCLUDE[ssIS](../../includes/ssis-md.md)] salvato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizzando l'autenticazione di Windows, utilizzare il codice seguente:  
  
```  
dtexec /sq pkgOne /ser productionServer  
```  
  
 Per eseguire un pacchetto di [!INCLUDE[ssIS](../../includes/ssis-md.md)] salvato nella cartella del file system nell'archivio pacchetti SSIS, utilizzare il codice seguente:  
  
```  
dtexec /dts "\File System\MyPackage"  
```  
  
 Per convalidare un pacchetto che utilizza l'autenticazione di Windows ed è salvato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] senza tuttavia eseguirlo, utilizzare il codice seguente:  
  
```  
dtexec /sq pkgOne /ser productionServer /va  
```  
  
 Per eseguire un pacchetto di [!INCLUDE[ssIS](../../includes/ssis-md.md)] salvato nel file system, utilizzare il codice seguente:  
  
```  
dtexec /f "c:\pkgOne.dtsx"   
```  
  
 Per eseguire un pacchetto di [!INCLUDE[ssIS](../../includes/ssis-md.md)] salvato nel file system e per specificare le opzioni di registrazione, utilizzare il codice seguente:  
  
```  
dtexec /f "c:\pkgOne.dtsx" /l "DTS.LogProviderTextFile;c:\log.txt"  
```  
  
 Per eseguire un pacchetto che utilizza l'autenticazione di Windows ed è salvato nell'istanza predefinita locale di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], e verificarne la versione prima della sua esecuzione, utilizzare il codice seguente:  
  
```  
dtexec /sq pkgOne /verifyv {c200e360-38c5-11c5-11ce-ae62-08002b2b79ef}  
```  
  
 Per eseguire un pacchetto di [!INCLUDE[ssIS](../../includes/ssis-md.md)] salvato nel file system e configurato esternamente, utilizzare il codice seguente:  
  
```  
dtexec /f "c:\pkgOne.dtsx" /conf "c:\pkgOneConfig.cfg"  
```  
  
> **NOTA:** gli argomenti *package_path* e *filespec* dell'opzione /SQL, /DTS o /FILE devono essere racchiusi tra virgolette se il percorso o il nome del file contiene uno spazio. Se non è racchiuso tra virgolette, un argomento non può contenere spazi vuoti.  
  
 **Opzioni di registrazione**  
  
 Si supponga, ad esempio, che i tipi di voci di log siano A, B e C. Nell'esempio seguente l'opzione **ConsoleLog** senza alcun parametro visualizza tutti e tre i tipi di log con tutti i campi:  
  
```  
/CONSOLELOG  
```  
  
 Nell'opzione seguente vengono visualizzati tutti i tipi di log, ma solo con le colonne Name e Message:  
  
```  
/CONSOLELOG NM  
```  
  
 Nell'opzione seguente vengono visualizzate tutte le colonne, ma solo per il tipo di voce di log A:  
  
```  
/CONSOLELOG I;LogEntryTypeA  
```  
  
 Nell'opzione seguente viene visualizzato solo il tipo di voce di log A con le colonne Name e Message:  
  
```  
/CONSOLELOG NM;I;LogEntryTypeA  
```  
  
 L'opzione seguente consente di visualizzare le voci di log per i tipi di voci di log A e B:  
  
```  
/CONSOLELOG I;LogEntryTypeA;LogEntryTypeB  
```  
  
 È possibile ottenere gli stessi risultati usando più opzioni **ConsoleLog** :  
  
```  
/CONSOLELOG I;LogEntryTypeA /CONSOLELOG I;LogEntryTypeB  
```  
  
 Se l'opzione **ConsoleLog** viene usata senza parametri, vengono visualizzati tutti i campi. L'inclusione di un parametro *list_options* comporta la visualizzazione solo del tipo di voce di log A con tutti i campi:  
  
```  
/CONSOLELOG NM;I;LogEntryTypeA /CONSOLELOG  
```  
  
 L'esempio seguente visualizza tutte le voci di log eccetto il tipo di voce di log A, ovvero visualizza i tipi di voce di log B e C:  
  
```  
/CONSOLELOG E;LogEntryTypeA  
```  
  
 Nell'esempio seguente gli stessi risultati vengono ottenuti usando più opzioni **ConsoleLog** e una singola esclusione:  
  
```  
/CONSOLELOG E;LogEntryTypeA /CONSOLELOG  
/CONSOLELOG E;LogEntryTypeA /CONSOLELOG E;LogEntryTypeA  
/CONSOLELOG E;LogEntryTypeA;LogEntryTypeA  
```  
  
 Nell'esempio seguente non viene visualizzato alcun messaggio di log poiché, quando un tipo di file di log si trova sia nell'elenco delle inclusioni sia in quello delle esclusioni, esso verrà escluso.  
  
```  
/CONSOLELOG E;LogEntryTypeA /CONSOLELOG I;LogEntryTypeA  
```  
  
 **Opzione SET**  
  
 L'esempio seguente illustra come usare l'opzione **/SET** tramite cui è possibile modificare il valore di qualsiasi variabile o proprietà del pacchetto quando si avvia il pacchetto dalla riga di comando.  
  
```  
/SET \package\DataFlowTask.Variables[User::MyVariable].Value;newValue  
```  
  
 **Opzione Project**  
  
 L'esempio seguente illustra come usare le opzioni **/Project** e **/Package** .  
  
```  
/Project c:\project.ispac /Package Package1.dtsx  
```  
  
 L'esempio seguente illustra come usare le opzioni **/Project** e **/Package** e come impostare i parametri del pacchetto e del progetto.  
  
```  
/Project c:\project.ispac /Package Package1.dtsx /SET \Package.Variables[$Package::Parameter];1 /SET \Package.Variables[$Project::Parameter];1  
  
```  
  
 **Opzione ISServer**  
  
 L'esempio seguente illustra come usare l'opzione **/ISServer** .  
  
```  
dtexec /isserver "\SSISDB\MyFolder\MyProject\MyPackage.dtsx" /server "."  
```  
  
 L'esempio seguente illustra come usare l'opzione **/ISServer** e come impostare i parametri del progetto e di gestione connessione.  
  
```  
/Server localhost /ISServer "\SSISDB\MyFolder\Integration Services Project1\Package.dtsx" /Par "$Project::ProjectParameter(Int32)";1 /Par "CM.SourceServer.InitialCatalog";SourceDB  
  
```  
  
## <a name="related-content"></a>Contenuto correlato  
 Intervento sul blog relativo a [codici di uscita, DTEXEC e catalogo SSIS](https://www.mattmasson.com/2012/02/exit-codes-dtexec-and-ssis-catalog/), su www.mattmasson.com.  
  
  
