---
title: Aggiornamento dati PowerPivot con SharePoint 2010 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- unattended data refresh [Analysis Services with SharePoint]
- scheduled data refresh [Analysis Services with SharePoint]
- data refresh [Analysis Services with SharePoint]
ms.assetid: 01b54e6f-66e5-485c-acaa-3f9aa53119c9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 04dea4a32303e06d7f0e6c015eef38ba6d267a30
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66070846"
---
# <a name="powerpivot-data-refresh-with-sharepoint-2010"></a>Aggiornamento di dati PowerPivot con SharePoint 2010
  L'aggiornamento dati [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] è un'operazione lato server pianificata che esegue query sulle origini dati esterne per aggiornare i dati [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] in una cartella di lavoro di Excel archiviata in una raccolta contenuto.  
  
 L'aggiornamento dati è una funzionalità incorporata di [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] per SharePoint, per il cui utilizzo è tuttavia necessario eseguire servizi e processi timer specifici nella farm di SharePoint 2010. Spesso, per il completamento dell'aggiornamento dati è richiesta l'esecuzione di alcuni passaggi amministrativi aggiuntivi quali l'installazione di provider di dati e il controllo delle autorizzazioni di database.  
  
 **[!INCLUDE[applies](../includes/applies-md.md)]** SharePoint 2010  
  
> [!NOTE]  
>  
  [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] e SharePoint Server 2013 Excel Services viene usata un'architettura diversa per i modelli di dati di [!INCLUDE[ssGemini](../includes/ssgemini-md.md)] . Nella nuova architettura viene utilizzato Excel Services come componente principale per caricare i modelli di dati in questione. L'architettura di aggiornamento dati utilizzata in precedenza era basata su un server con in esecuzione il servizio di sistema di PowerPivot e [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] in modalità SharePoint per caricare i modelli di dati. Per ulteriori informazioni, vedere [aggiornamento dati PowerPivot con SharePoint 2013](power-pivot-sharepoint/power-pivot-data-refresh-with-sharepoint-2013.md).  
  
 **In questo argomento**  
  
 [Passaggio 1: Abilitare il servizio di archiviazione sicura e generare una chiave master](#bkmk_services)  
  
 [Passaggio 2: Disabilitare le opzioni relative alle credenziali che non si desidera supportare](#bkmk_creds)  
  
 [Passaggio 3: Creare applicazioni di destinazione per l'archiviazione delle credenziali utilizzate nell'aggiornamento dati](#bkmk_stored)  
  
 [Passaggio 4: Configurare il server per l'aggiornamento dati scalabile](#bkmk_scale)  
  
 [Passaggio 5: Installare i provider di dati utilizzati per importare dati PowerPivot](#bkmk_installdp)  
  
 [Passaggio 6: Concedere le autorizzazioni per creare pianificazioni e accedere a origini dati esterne](#bkmk_accounts)  
  
 [Passaggio 7: Abilitare l'aggiornamento della cartella di lavoro per l'aggiornamento dati](#bkmk_upgradewrkbk)  
  
 [Passaggio 8: Verificare la configurazione dell'aggiornamento dati](#bkmk_verify)  
  
 [Modifica delle impostazioni di configurazione per l'aggiornamento dati](#bkmk_config)  
  
 [Ripianificare il processo timer di aggiornamento dati PowerPivot](#configTimerJob)  
  
 [Disabilitare il processo timer di aggiornamento dati](#bkmk_disableDR)  
  
 Una volta completata la configurazione dell'ambiente server e delle relative autorizzazioni, è possibile procedere all'aggiornamento dati. Per utilizzare l'aggiornamento dati, un utente di SharePoint crea una pianificazione in una cartella di lavoro di PowerPivot, specificando la frequenza dell'aggiornamento dati. La creazione della pianificazione è in genere eseguita dal proprietario o dall'autore della cartella di lavoro che ha pubblicato il file in SharePoint. Questi può creare e gestire le pianificazioni dell'aggiornamento dati per le cartelle di lavoro di cui è proprietario. Per altre informazioni, vedere [pianificare un aggiornamento dati &#40;PowerPivot per SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md).  
  
##  <a name="bkmk_services"></a>Passaggio 1: abilitare servizio di archiviazione sicura e generare una chiave master  
 L'aggiornamento dati PowerPivot dipende dal fatto che il servizio di archiviazione sicura fornisca le credenziali utilizzate per eseguire i processi di aggiornamento dati e si connetta a origini dati esterne che utilizzano le credenziali archiviate.  
  
 Se PowerPivot per SharePoint è stato installato tramite l'opzione Nuovo server, il servizio di archiviazione sicura viene configurato automaticamente. Per tutti gli altri scenari di installazione, è necessario creare e configurare un'applicazione del servizio e generare una chiave di crittografia master per il servizio di archiviazione sicura.  
  
> [!NOTE]  
>  È necessario essere un amministratore della farm per configurare il servizio di archiviazione sicura o delegare l'amministrazione di tale servizio a un altro utente. È necessario essere un amministratore dell'applicazione di servizio per configurare o modificare le impostazioni dopo l'abilitazione.  
  
1.  In Gestione applicazioni di Amministrazione centrale fare clic su **Gestisci applicazioni di servizio**.  
  
2.  In Crea della barra multifunzione applicazioni di servizio fare clic su **nuovo**.  
  
3.  Selezionare **servizio di archiviazione sicura**.  
  
4.  Nella pagina **Crea applicazione di archiviazione sicura** immettere un nome per l'applicazione.  
  
5.  In **database**specificare il SQL Server istanza di che ospiterà il database per questa applicazione di servizio. Il valore predefinito è l'istanza del motore di database di SQL Server che ospita i database di configurazione della farm.  
  
6.  In **nome database**immettere il nome del database dell'applicazione di servizio. Il valore predefinito è Secure_Store_Service_DB_\<> GUID. Il nome predefinito corrisponde al nome predefinito dell'applicazione di servizio. Se è stato immesso un nome univoco per l'applicazione del servizio, seguire una convenzione di denominazione simile per il nome del database in modo da poterli gestire insieme.  
  
7.  In **Autenticazione database**l'impostazione predefinita è Autenticazione di Windows. Se si sceglie Autenticazione di SQL Server, fare riferimento alla guida dell'amministratore di SharePoint per le procedure consigliate sull'utilizzo di questo tipo di autenticazione nella farm in uso.  
  
8.  In pool di applicazioni selezionare **Crea nuovo pool di applicazioni.** Specificare un nome descrittivo che consentirà ad altri amministratori di server di identificare la modalità di utilizzo del pool di applicazioni.  
  
9. Selezionare un account di sicurezza per il pool di applicazioni. Specificare un account gestito per utilizzare un account utente di dominio.  
  
10. Accettare i valori predefiniti rimanenti, quindi fare clic su **OK.** L'applicazione di servizio verrà visualizzata con altri servizi gestiti nell'elenco di applicazioni di servizio della farm.  
  
11. Fare clic sull'applicazione del servizio di archiviazione sicura nell'elenco.  
  
12. Nella barra multifunzione applicazioni di servizio fare clic su **Gestisci**.  
  
13. In gestione chiavi fare clic su **genera nuova chiave**.  
  
14. Immettere e confermare una passphrase. La passphrase verrà utilizzata per aggiungere applicazioni di servizio condivise di archiviazione sicura aggiuntive.  
  
15. Fare clic su **OK**.  
  
 Per rendere disponibile la registrazione di controllo delle operazioni del servizio di archiviazione, utile per la risoluzione dei problemi, è necessario abilitarla. Per ulteriori informazioni su come abilitare la registrazione, vedere [Configure servizio di archiviazione sicura (SharePoint 2010)](https://go.microsoft.com/fwlink/p/?LinkID=223294).  
  
##  <a name="bkmk_creds"></a>Passaggio 2: disattivare le opzioni delle credenziali che non si desidera supportare  
 Tramite l'aggiornamento dati PowerPivot vengono fornite in una pianificazione tre opzioni relative alle credenziali. Quando il proprietario di una cartella di lavoro pianifica un aggiornamento dati e sceglie una di queste opzioni, determina l'account con il quale verrà eseguito il processo di aggiornamento dati. L'amministratore stabilisce quali opzioni relative alle credenziali sono disponibili ai proprietari della pianificazione.  
  
 È necessario che sia disponibile almeno un'opzione per eseguire l'aggiornamento dati.  
  
 ![SSAS_PowerpivotKJ_DataRefreshCreds](media/ssas-powerpivotkj-datarefreshcreds.gif "SSAS_PowerpivotKJ_DataRefreshCreds")  
  
 L'opzione 1, **utilizzare l'account di aggiornamento dati configurato dall'amministratore**, viene sempre visualizzata nella pagina di definizione della pianificazione, ma funziona solo se si configura l'account di aggiornamento dati automatico. Per ulteriori informazioni su come creare l'account, vedere [configurare l'account di aggiornamento dati automatico PowerPivot &#40;PowerPivot per SharePoint&#41;](configure-unattended-data-refresh-account-powerpivot-sharepoint.md).  
  
 L'opzione 2, **Connetti usando le credenziali di Windows seguenti**, viene sempre visualizzata nella pagina, ma funziona solo quando si Abilita l'opzione **Consenti agli utenti di immettere credenziali di Windows personalizzate** nella pagina di configurazione dell'applicazione di servizio. Questa opzione è abilitata per impostazione predefinita, tuttavia è possibile disabilitarla se gli svantaggi derivanti dal suo utilizzo sono maggiori dei vantaggi (vedere di seguito).  
  
 L'opzione 3, **Connetti usando le credenziali salvate in servizio di archiviazione sicura**, viene sempre visualizzata nella pagina, ma funziona solo quando il proprietario di una pianificazione fornisce un'applicazione di destinazione valida. Un amministratore deve creare anticipatamente queste applicazioni di destinazione, quindi fornire il nome dell'applicazione a coloro che creeranno le pianificazioni dell'aggiornamento dati. Per ulteriori informazioni su come creare un'applicazione di destinazione per le operazioni di aggiornamento dati, vedere [configurare le credenziali archiviate per l'aggiornamento dati PowerPivot &#40;PowerPivot per SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md).  
  
 **Configurazione delle credenziali opzione 2, "Connetti con le seguenti credenziali utente di Windows"**  
  
 Un'applicazione del servizio PowerPivot include un'opzione relativa alle credenziali che consente ai proprietari delle pianificazioni di immettere un nome utente e una password di Windows arbitrari per l'esecuzione di un processo di aggiornamento dati. Si tratta della seconda opzione relativa alle credenziali presente nella pagina di definizione della pianificazione:  
  
 ![SSAS_PPS_ScheduleDataRefreshCreds](media/ssas-pps-scheduledatarefreshcreds.gif "SSAS_PPS_ScheduleDataRefreshCreds")  
  
 Per impostazione predefinita, questa opzione relativa alla credenziali è abilitata. Quando questa opzione viene abilitata, tramite il servizio di sistema PowerPivot viene generata un'applicazione di destinazione nel servizio di archiviazione sicura per l'archiviazione del nome utente e della password immessi dal proprietario della pianificazione. Un'applicazione di destinazione generata viene creata utilizzando questa convenzione di denominazione\<: guid PowerPivotDataRefresh_>. Viene creata un'applicazione di destinazione per ogni set di credenziali di Windows. Se esiste già un'applicazione di destinazione di proprietà del servizio di sistema PowerPivot in cui sono archiviati il nome utente e la password immessi dal proprietario della pianificazione, tale applicazione di destinazione verrà utilizzata dal servizio di sistema PowerPivot che quindi eviterà di crearne una nuova.  
  
 I principali vantaggi derivanti dall'utilizzo di questa opzione relativa alle credenziali sono la semplicità e la facilità di utilizzo. Il lavoro preliminare è minimo perché le applicazioni di destinazione vengono create automaticamente. Inoltre, l'esecuzione dell'aggiornamento dati con le credenziali del proprietario della pianificazione, che con tutta probabilità è anche l'utente che ha creato la cartella di lavoro, semplifica i requisiti relativi alle autorizzazioni a valle. Quasi sicuramente, questo utente dispone già delle autorizzazioni per il database di destinazione. Quando l'aggiornamento dati viene eseguito con l'identità utente di Windows di questa persona, le connessioni dati che specificano l'utente corrente funzioneranno automaticamente.  
  
 Lo svantaggio che ne deriva è una funzionalità di gestione limitata. Sebbene le applicazioni di destinazione vengano create automaticamente, non vengono eliminate automaticamente né aggiornate quando le informazioni dell'account vengono modificate. Le applicazioni di destinazione potrebbero diventare obsolete a causa dei criteri di scadenza delle password. I processi di aggiornamento dati per i quali vengono utilizzate credenziali scadute non potranno più essere completati. In questi casi, i proprietari delle pianificazioni dovranno aggiornare le loro credenziali fornendo il nome utente e la password correnti nella pianificazione dell'aggiornamento dati. A questo punto, verrà creata una nuova applicazione di destinazione. Man mano che gli utenti aggiungeranno e modificheranno le informazioni delle credenziali nelle pianificazioni dell'aggiornamento dati, aumenterà il numero di applicazioni di destinazione generate automaticamente nel sistema.  
  
 Attualmente non è possibile determinare quali applicazioni di destinazione sono attive e quali inattive, né far risalire un'applicazione di destinazione specifica alle pianificazioni dell'aggiornamento dati che la utilizzano. In generale, è consigliabile non eliminare le applicazioni di destinazione per non compromettere le pianificazioni dell'aggiornamento dati esistenti. L'eliminazione di un'applicazione di destinazione ancora in uso provocherà l'esito negativo dell'aggiornamento dei dati con il messaggio "applicazione di destinazione non trovata", visualizzato nella pagina Cronologia aggiornamento dati della cartella di lavoro.  
  
 Qualora si scegliesse di disabilitare questa opzione, è possibile eliminare in sicurezza tutte le applicazioni di destinazione generate per l'aggiornamento dati PowerPivot.  
  
 **Possibilità di impedire l'utilizzo di credenziali di Windows arbitrarie nelle pianificazioni dell'aggiornamento dati**  
  
1.  In Gestione applicazioni di amministrazione centrale fare clic su **Gestisci applicazioni di servizio**.  
  
2.  Fare clic sul nome dell'applicazione di servizio PowerPivot. Verrà visualizzato il dashboard di gestione PowerPivot.  
  
3.  In azioni fare clic su **Configura impostazioni dell'applicazione di servizio** per aprire la pagina delle impostazioni dell'applicazione di servizio PowerPivot.  
  
4.  Nella sezione aggiornamento dati deselezionare la casella **di controllo Consenti agli utenti di immettere credenziali di Windows personalizzate** .  
  
     ![SSAS_PowerPivotDatarefreshOptions_AllowUser](media/ssas-powerpivotdatarefreshoptions-allowuser.gif "SSAS_PowerPivotDatarefreshOptions_AllowUser")  
  
##  <a name="bkmk_stored"></a>Passaggio 3: creare applicazioni di destinazione per archiviare le credenziali utilizzate nell'aggiornamento dati  
 Dopo avere configurato il servizio di archiviazione sicura, gli amministratori di SharePoint possono creare applicazioni di destinazione per rendere disponibili le credenziali archiviate a scopo di aggiornamento dati, tra cui l'account di aggiornamento dati PowerPivot automatico o qualsiasi altro account utilizzato per eseguire il processo o connettersi a origini dati esterne.  
  
 Ricordare che è necessario creare applicazioni di destinazione per rendere utilizzabili determinate opzioni relative alle credenziali. In modo specifico, è necessario creare applicazioni di destinazione per l'account di aggiornamento dati automatico PowerPivot, più eventuali credenziali archiviate aggiuntive che si prevede verranno utilizzate nelle operazioni di aggiornamento dati.  
  
 Per ulteriori informazioni su come creare applicazioni di destinazione contenenti credenziali archiviate, vedere [configurare l'account di aggiornamento dati automatico powerpivot &#40;PowerPivot per SharePoint&#41;](configure-unattended-data-refresh-account-powerpivot-sharepoint.md) e [configurare le credenziali archiviate per l'aggiornamento dati powerpivot &#40;PowerPivot per SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md).  
  
##  <a name="bkmk_scale"></a>Passaggio 4: configurare il server per l'aggiornamento dati scalabile  
 Per impostazione predefinita, ogni installazione di PowerPivot per SharePoint supporta sia le query su richiesta sia l'aggiornamento dati pianificato.  
  
 Per ogni installazione, è possibile specificare se l'istanza del server Analysis Services supporta sia le query sia l'aggiornamento dati pianificato o se è dedicata a un tipo specifico di operazione. Se si dispone di più installazioni di PowerPivot per SharePoint nella farm, è opportuno dedicare un server alle operazioni di aggiornamento dati se si verificano ritardi o errori durante i processi.  
  
 Inoltre, se l'hardware sottostante supporta questa operazione, è possibile aumentare il numero di processi di aggiornamento dati eseguiti in parallelo. Per impostazione predefinita, il numero di processi che è possibile eseguire in parallelo viene calcolato in base alla memoria del sistema, tuttavia è possibile aumentare il numero se la capacità della CPU è in grado di supportare anche questo carico di lavoro.  
  
 Per altre informazioni, vedere [configurare l'aggiornamento dati dedicato o l'elaborazione solo Query &#40;PowerPivot per SharePoint&#41;](configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint.md).  
  
##  <a name="bkmk_installdp"></a>Passaggio 5: installare i provider di dati utilizzati per importare dati PowerPivot  
 Un'operazione di aggiornamento dati è praticamente la ripetizione di un'operazione di importazione per il recupero dei dati originali. Ciò significa che gli stessi provider di dati utilizzati per importare i dati nell'applicazione client PowerPivot devono essere installati nel server PowerPivot.  
  
 È necessario essere un amministratore locale per installare i provider di dati in un server di Windows. Se si installano driver aggiuntivi, assicurarsi di installarli in tutti i computer della farm SharePoint che dispone di un'installazione di PowerPivot per SharePoint. Se nella farm sono presenti più server PowerPivot, è necessario installare i provider su ognuno.  
  
 Tenere presente che i server SharePoint sono applicazioni a 64 bit. Assicurarsi di installare la versione a 64 bit dei provider di dati utilizzati per supportare le operazioni di aggiornamento dati.  
  
##  <a name="bkmk_accounts"></a>Passaggio 6: concedere le autorizzazioni per creare pianificazioni e accedere a origini dati esterne  
 Gli autori o i proprietari delle cartelle di lavoro devono disporre dell'autorizzazione **Collaborazione** per pianificare l'aggiornamento dati in una cartella di lavoro. Dato questo livello di autorizzazione, può aprire e modificare la pagina di configurazione dell'aggiornamento dati della cartella di lavoro per specificare le credenziali e le informazioni di pianificazione usate per aggiornare i dati.  
  
 Oltre alle autorizzazioni di SharePoint, è necessario rivedere le autorizzazioni di database per le origini dati esterne per assicurarsi che gli account utilizzati durante l'aggiornamento dati dispongano di diritti di accesso sufficienti per i dati. La determinazione dei requisiti relativi alle autorizzazioni richiede un'attenta valutazione poiché le autorizzazioni che è necessario concedere variano a seconda della stringa di connessione nella cartella di lavoro e dell'identità utente con cui viene eseguito il processo di aggiornamento dati.  
  
 **Importanza delle stringhe di connessione esistenti in una cartella di lavoro di PowerPivot per le operazioni di aggiornamento dati PowerPivot**  
  
 Quando viene eseguito l'aggiornamento dati, viene inviata una richiesta di connessione all'origine dati esterna utilizzando la stringa di connessione creata al momento dell'importazione iniziale dei dati. Il percorso del server, il nome del database e i parametri di autenticazione specificati in questa stringa di connessione vengono riutilizzati durante l'aggiornamento dati per accedere alle stesse origini dati. La stringa di connessione e la sua costruzione complessiva non possono essere modificate a scopo di aggiornamento dati. Durante l'aggiornamento dati vengono semplicemente riutilizzate inalterate. In alcuni casi, se si utilizza un'autenticazione non Windows per la connessione a un'origine dati, è possibile ignorare il nome utente e la password indicati nella stringa di connessione. Informazioni dettagliate su questo aspetto vengono fornite più avanti in questo argomento.  
  
 Per la maggior parte delle cartelle di lavoro, l'opzione di autenticazione predefinita per la connessione prevede l'utilizzo di connessioni trusted o della sicurezza integrata di Windows per ottenere stringhe di connessione contenenti `SSPI=IntegratedSecurity` o `SSPI=TrustedConnection`. Quando questa stringa di connessione viene utilizzata durante l'aggiornamento dati, l'account utilizzato per eseguire il processo di aggiornamento dati diventa l'utente corrente. Questo account deve quindi disporre delle autorizzazioni di lettura per tutte le origini dati esterne a cui si accede tramite una connessione trusted.  
  
 **L'account di aggiornamento dati automatico PowerPivot è stato abilitato?**  
  
 In caso di risposta affermativa, è necessario concedere a tale account le autorizzazioni di lettura per le origini dati a cui si accede durante l'aggiornamento dati. Il motivo per cui l'account richiede autorizzazioni di lettura è perché in una cartella di lavoro che utilizza le opzioni di autenticazione predefinite, l'account automatico sarà l'utente corrente durante l'aggiornamento dati. A meno che il proprietario della pianificazione non ignori le credenziali indicate nella stringa di connessione, questo account necessiterà delle autorizzazioni di lettura per tutte le origini dati utilizzate attivamente nell'organizzazione.  
  
 **Si intende utilizzare l'opzione 2 per consentire al proprietario della pianificazione di immettere un nome utente e una password di Windows?**  
  
 In genere, gli utenti che creano cartelle di lavoro di PowerPivot dispongono già di autorizzazioni sufficienti perché hanno già importato i dati. Se tali utenti configurano l'aggiornamento dati affinché venga eseguito con la loro identità utente di Windows, per il recupero dei dati durante l'aggiornamento verrà utilizzato il loro account utente di Windows che dispone già di diritti per il database. Le autorizzazioni esistenti dovrebbero essere sufficienti.  
  
 **Si intende utilizzare l'opzione 3 per l'utilizzo di un'applicazione di destinazione del servizio di archiviazione sicura per fornire un'identità utente per l'esecuzione dei processi di aggiornamento dati?**  
  
 Qualsiasi account utilizzato per l'esecuzione di un processo di aggiornamento dati deve disporre di autorizzazioni di lettura per gli stessi motivi descritti per l'account di aggiornamento dati automatico PowerPivot.  
  
 **Come controllare le stringhe di connessione per determinare se è possibile ignorare le credenziali utilizzate durante l'aggiornamento dati**  
  
 Come indicato in precedenza, è possibile sostituire il nome utente e la password al livello del processo di aggiornamento dati se la stringa di connessione utilizza un'autenticazione non Windows, ad esempio l'autenticazione di SQL Server. Le credenziali non Windows vengono passate alla stringa di connessione tramite i parametri Password e ID utente. Se la cartella di lavoro contiene una stringa di connessione con questi parametri, è possibile specificare un nome utente e una password diversi per aggiornare i dati da tale origine dati.  
  
 Nei passaggi successivi viene spiegato come determinare se una stringa di connessione consente di ignorare il nome utente e la password.  
  
1.  Aprire la cartella di lavoro in Excel.  
  
2.  Aprire la finestra di PowerPivot. In Excel fare clic su Finestra PowerPivot sulla barra multifunzione PowerPivot.  
  
3.  Fare clic su **progettazione**.  
  
4.  Fare clic su **connessioni esistenti**.  
  
     Tutte le connessioni utilizzate nella cartella di lavoro sono elencate in **connessioni dati PowerPivot**.  
  
5.  Selezionare la connessione e fare clic su **modifica**e quindi su **Avanzate**. La stringa di connessione si trova nella parte inferiore della pagina.  
  
 Se nella stringa di connessione viene visualizzato **Integrated Security = SSPI** , non è possibile eseguire l'override delle credenziali nella stringa di connessione. La connessione utilizzerà sempre l'utente corrente. Eventuali credenziali fornite verranno ignorate.  
  
 Se viene visualizzato **Mantieni sicurezza Info = False, password =\*\*\*\*\*\*\*\*\*\*\*, UserID =\<userlogin>**, sarà presente una stringa di connessione che accetterà le sostituzioni delle credenziali. Le credenziali contenute in una stringa di connessione, ad esempio ID utente e Password, non sono credenziali di Windows, ma account di accesso del database o altri account validi per l'origine dati di destinazione.  
  
 **Come ignorare le credenziali nella stringa di connessione**  
  
 Per ignorare le credenziali, è necessario specificare le credenziali dell'origine dati nella pianificazione dell'aggiornamento dati. L'amministratore può fornire un'applicazione di destinazione nel servizio di archiviazione sicura per il mapping delle credenziali utilizzate per accedere ai dati esterni. Il proprietario della pianificazione potrà quindi immettere l'ID dell'applicazione di destinazione nella pianificazione dell'aggiornamento dati che definirà. Per ulteriori informazioni sulla creazione di questa applicazione di destinazione, vedere [configurare le credenziali archiviate per l'aggiornamento dati PowerPivot &#40;PowerPivot per SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md).  
  
 In alternativa, il proprietario della pianificazione può digitare il set di credenziali utilizzate per la connessione alle origini dati durante l'aggiornamento dati. Nella figura seguente viene illustrata l'opzione dell'origine dati nella pagina di definizione della pianificazione.  
  
 ![SSAS_PowerPivotKJ_DataRefreshDSOptions](media/ssas-powerpivotkj-datarefreshdsoptions.gif "SSAS_PowerPivotKJ_DataRefreshDSOptions")  
  
 **Identificazione dei requisiti dell'accesso ai dati**  
  
 Come indicato nelle sezioni precedenti, l'account utilizzato per l'aggiornamento dati e la connessione alle origini dati esterne è spesso sempre lo stesso. Di conseguenza, l'account utilizzato per accedere alle origini dati esterne è determinato dalle opzioni impostate in questa parte della pagina di pianificazione dell'aggiornamento dati. Potrebbe trattarsi dell'account di aggiornamento dati automatico PowerPivot, dell'account Windows di un utente o dell'account archiviato in un'applicazione di destinazione predefinita.  
  
 ![SSAS_PowerpivotKJ_DataRefreshCreds](media/ssas-powerpivotkj-datarefreshcreds.gif "SSAS_PowerpivotKJ_DataRefreshCreds")  
  
 Nei casi in cui l'account utilizzato per l'esecuzione dell'aggiornamento dati sia diverso dall'account utilizzato per l'importazione dei dati, ad esempio l'account di aggiornamento dati automatico PowerPivot attraverso l'opzione 1 o altri set di credenziali archiviate attraverso l'opzione 3, è necessario creare un nuovo accesso del database per quell'account e concedere ad esso autorizzazioni di lettura per le origini dati esterne.  
  
 Dopo avere compreso quali account richiedono l'accesso ai dati, è possibile avviare il controllo delle autorizzazioni per le origini dati utilizzate con maggiore frequenza nelle cartelle di lavoro di PowerPivot. Iniziare da data warehouse o da database di report utilizzati attivamente, ma sollecitare anche l'input agli utenti PowerPivot più attivi per scoprire quali origini dati stanno utilizzando. Dopo avere ottenuto un elenco di origini dati, è possibile verificare ognuna di esse per assicurarsi che le autorizzazioni siano impostate correttamente.  
  
##  <a name="bkmk_upgradewrkbk"></a>Passaggio 7: abilitare l'aggiornamento della cartella di lavoro per l'aggiornamento dati  
 Per impostazione predefinita, le cartelle di lavoro create utilizzando la versione [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] di PowerPivot per Excel non possono essere configurate per l'aggiornamento dati pianificato in una versione [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] di PowerPivot per SharePoint. Se si ospitano versioni più e meno recenti delle cartelle di lavoro di PowerPivot nell'ambiente SharePoint, è necessario aggiornare qualsiasi cartella di lavoro di [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] prima di poterla pianificare per l'aggiornamento dati automatico nel server.  
  
##  <a name="bkmk_verify"></a>Passaggio 8: verificare la configurazione dell'aggiornamento dati  
 Per verificare l'aggiornamento dati, è necessario che la cartella di lavoro di PowerPivot sia pubblicata in un sito di SharePoint. È necessario disporre delle autorizzazioni di collaborazione per la cartella di lavoro e delle autorizzazioni necessarie per accedere a eventuali origini dati incluse nella pianificazione dell'aggiornamento dati.  
  
 Quando si crea la pianificazione, selezionare la casella di controllo **Aggiorna anche appena possibile** per eseguire immediatamente l'aggiornamento dati. È quindi possibile controllare la pagina della cronologia dell'aggiornamento dati di quella cartella di lavoro per assicurarsi che sia stato eseguito correttamente. Ricordare che il processo timer dell'aggiornamento dati PowerPivot viene eseguito ogni minuto. Dovrà trascorrere almeno questo tempo prima di ottenere la conferma del completamento dell'aggiornamento dati.  
  
 Provare tutte le opzioni relative alle credenziali che si intende supportare. Ad esempio, se è stato configurato l'account di aggiornamento dati automatico PowerPivot, verificare che l'aggiornamento dati possa essere completato utilizzando questa opzione. Per ulteriori informazioni sulla pianificazione e la visualizzazione delle informazioni sullo stato, vedere [pianificare un aggiornamento dati &#40;PowerPivot per SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md) e [visualizzare la cronologia dell'aggiornamento dati &#40;PowerPivot per SharePoint&#41;](power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md).  
  
 Se l'aggiornamento dati non riesce, vedere la pagina relativa all' [aggiornamento dati PowerPivot](https://go.microsoft.com/fwlink/?LinkID=223279) in TechNet Wiki per individuare le possibili soluzioni.  
  
##  <a name="bkmk_config"></a>Modificare le impostazioni di configurazione per l'aggiornamento dati  
 Ogni applicazione del servizio PowerPivot dispone di impostazioni di configurazione che influiscono sulle operazioni di aggiornamento dati. In questa sezione viene illustrato come modificare tali impostazioni.  
  
###  <a name="procIntervals"></a>Imposta "orario di ufficio" per determinare l'elaborazione degli orari di inattività  
 Gli utenti di SharePoint che pianificano le operazioni di aggiornamento dati possono specificare un primo orario di inizio per l'opzione "Dopo l'orario lavorativo". Questa operazione potrebbe essere utile se si desidera recuperare dati di transazioni aziendali accumulati durante la giornata lavorativa. In qualità di amministratore di farm, è possibile specificare l'intervallo di ore che meglio definisca la giornata lavorativa dell'organizzazione. Se si definisce un giorno lavorativo che va dalle 04:00 alle 20:00, l'elaborazione dell'aggiornamento dati, in base all'ora di inizio indicata nell'opzione "Dopo l'orario lavorativo", avrà inizio alle 20:01.  
  
 Le richieste di aggiornamento dei dati che vengono eseguite durante le ore successive a quelle lavorative vengono aggiunte alla coda nell'ordine in cui viene ricevuta la richiesta. Le singole richieste saranno elaborate quando le risorse server diventeranno disponibili.  
  
1.  In Gestione applicazioni di amministrazione centrale fare clic su **Gestisci applicazioni di servizio**.  
  
2.  Fare clic sul nome dell'applicazione di servizio PowerPivot. Verrà visualizzato il dashboard di gestione PowerPivot.  
  
3.  In azioni fare clic su **Configura impostazioni dell'applicazione di servizio** per aprire la pagina delle impostazioni dell'applicazione di servizio PowerPivot.  
  
4.  Nella sezione Aggiornamento dati, in Orario lavorativo, immettere un'ora di inizio e di fine che definisca il periodo di elaborazione dopo l'orario lavorativo.  
  
     Se non si desidera un periodo di elaborazione che vada oltre l'orario lavorativo definito, è possibile immettere lo stesso valore sia per Ora inizio che per Ora fine (ad esempio, 12:00 per entrambe). Tuttavia, si tenga presente che le pagine di definizione della pianificazione sui siti di SharePoint disporranno ancora di "Dopo l'orario lavorativo" come opzione. Gli utenti che selezionano quell'opzione in una farm che non dispone di alcun intervallo per l'elaborazione oltre l'orario lavorativo definito riceveranno errori relativi all'aggiornamento dei dati dal momento che l'avvio dei processi di elaborazione ha avuto esito negativo.  
  
5.  Fare clic su **OK**.  
  
###  <a name="usagehist"></a>Limite per quanto tempo viene mantenuta la cronologia dell'aggiornamento dati  
 La cronologia aggiornamento dati è un record dettagliato dei messaggi di operazione riuscita e di errore generati nel tempo per le operazioni di aggiornamento dati. Le informazioni sulla cronologia vengono raccolte e gestite tramite il sistema di raccolta dei dati sull'utilizzo nella farm. Di conseguenza, i limiti impostati sulla cronologia dati sull'utilizzo si applicano anche alla cronologia aggiornamento dati. Poiché i report relativi all'attività di utilizzo uniscono i dati provenienti dal sistema di PowerPivot, viene utilizzata una singola impostazione di cronologia per controllare il periodo di memorizzazione dei dati sia per la cronologia aggiornamento dati sia per tutti gli altri dati sull'utilizzo raccolti e archiviati.  
  
1.  In Gestione applicazioni di amministrazione centrale fare clic su **Gestisci applicazioni di servizio**.  
  
2.  Fare clic sul nome dell'applicazione di servizio PowerPivot. Verrà visualizzato il dashboard di gestione PowerPivot.  
  
3.  In azioni fare clic su **Configura impostazioni dell'applicazione di servizio** per aprire la pagina delle impostazioni dell'applicazione di servizio PowerPivot.  
  
4.  Nella sezione Raccolta dati su utilizzo, in Cronologia dati su utilizzo digitare per quanti giorni si desidera mantenere un record dell'attività di aggiornamento dati per ogni cartella di lavoro.  
  
     Il valore predefinito è 365 giorni. Il valore minimo è 1 giorno mentre quello massimo è 5000 giorni. Un valore pari a 0 consente di specificare un periodo di memorizzazione illimitato, ovvero i dati non verranno mai eliminati. Non è disponibile alcuna impostazione per la disabilitazione della cronologia.  
  
5.  Fare clic su **OK**.  
  
 Le informazioni sulla cronologia sono rese disponibili agli utenti di SharePoint quando scelgono l'opzione Gestisci aggiornamento dati in una cartella di lavoro che dispone di una cronologia aggiornamento dati. Queste informazioni vengono utilizzate anche nel dashboard di gestione PowerPivot utilizzato dagli amministratori di farm per gestire le operazioni del servizio PowerPivot. Per altre informazioni, vedere [visualizzare la cronologia dell'aggiornamento dati &#40;PowerPivot per SharePoint&#41;](power-pivot-sharepoint/view-data-refresh-history-power-pivot-for-sharepoint.md).  
  
 L'archiviazione fisica a lungo termine di dati di cronologia è nel database dell'applicazione del servizio PowerPivot per l'applicazione del servizio PowerPivot. Per ulteriori informazioni sul modo in cui i dati di utilizzo vengono raccolti e archiviati, vedere [raccolta dati di utilizzo di PowerPivot](power-pivot-sharepoint/power-pivot-usage-data-collection.md).  
  
##  <a name="configTimerJob"></a>Ripianificare il processo timer di aggiornamento dati PowerPivot  
 L'aggiornamento dei dati pianificato viene attivato da un processo timer di aggiornamento dati PowerPivot che consente di analizzare le informazioni sulla pianificazione nel database dell'applicazione del servizio PowerPivot ogni minuto. Quando viene pianificato l'inizio dell'aggiornamento dati, tramite il processo timer la richiesta viene aggiunta a una coda di elaborazione su un server PowerPivot disponibile.  
  
 È possibile aumentare la durata delle analisi come tecnica di ottimizzazione delle prestazioni. Inoltre è possibile disabilitare il processo timer per arrestare temporaneamente le operazioni di aggiornamento dati durante la risoluzione di problemi.  
  
 L'impostazione predefinita è un minuto, vale a dire il valore minimo che è possibile specificare. Si consiglia l'applicazione di questo valore in quanto fornisce il risultato migliore in termini di stime per le pianificazioni in esecuzione in orari arbitrari durante tutto il giorno. Ad esempio, se un utente pianifica l'aggiornamento dati per le 16.15 e il processo timer analizza le pianificazioni ogni minuto, la richiesta di aggiornamento dati pianificata sarà rilevata alle 16.15 e l'elaborazione inizierà nell'arco di pochi minuti dopo tale orario.  
  
 Se l'intervallo di analisi viene aumentato in modo che l'esecuzione avvenga meno frequentemente (ad esempio, una volta al giorno a mezzanotte), tutte le operazioni di aggiornamento dati la cui esecuzione è stata pianificata per tale intervallo verranno aggiunte contemporaneamente alla coda di elaborazione, con il rischio di sovraccaricare il server e sottrarre risorse del sistema alle altre applicazioni. A seconda del numero degli aggiornamenti pianificati, la coda di elaborazione per le operazioni di aggiornamento dati potrebbe aumentare al punto tale da non poter essere in grado di completare tutti i processi. Questo potrebbe comportare l'eliminazione delle richieste di aggiornamento dati alla fine della coda se rientrano nel successivo intervallo di elaborazione.  
  
 Se l'hardware supporta questa funzionalità, è possibile limitare il problema specificando ulteriori processori per l'esecuzione in parallelo di più processi di aggiornamento dati. Per altre informazioni, vedere [configurare l'aggiornamento dati dedicato o l'elaborazione solo Query &#40;PowerPivot per SharePoint&#41;](configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint.md). Per ulteriori informazioni sul modo in cui le richieste di aggiornamento dei dati vengono individuate, aggiunte a una coda ed elaborate, vedere [aggiornamento dati PowerPivot](power-pivot-sharepoint/power-pivot-data-refresh.md).  
  
1.  In Amministrazione centrale fare clic su **Monitoraggio**.  
  
2.  Fare clic su **Verifica definizioni processi**.  
  
3.  Selezionare il **processo timer di aggiornamento dati PowerPivot**.  
  
4.  Modificare la frequenza della pianificazione per modificare quella relativa alle analisi delle informazioni sulla pianificazione degli aggiornamenti eseguite tramite il processo timer.  
  
##  <a name="bkmk_disableDR"></a>Disabilitare il processo timer di aggiornamento dati  
 Il processo timer di aggiornamento dati PowerPivot è un processo timer a livello di farm abilitato o disabilitato per tutte le istanze del server PowerPivot nella farm. Non è associato a un'applicazione Web o del servizio PowerPivot specifica. Non è possibile disabilitarlo su alcuni server per forzare l'elaborazione dell'aggiornamento dei dati in altri server nella farm.  
  
 Se si disabilita il processo timer di aggiornamento dati PowerPivot, le richieste già nella coda verranno elaborate, ma non verrà aggiunta alcuna nuova richiesta fino alla riabilitazione del processo. Le richieste pianificate in precedenza non vengono elaborate.  
  
 La disabilitazione del processo timer non ha alcun effetto sulla disponibilità delle funzionalità nelle pagine dell'applicazione. Non esiste alcun modo per rimuovere o nascondere la funzionalità di aggiornamento dati nelle applicazioni Web. Gli utenti che dispongono di autorizzazioni di collaborazione o di livello superiore saranno ancora in grado di creare nuove pianificazioni per le operazioni di aggiornamento dati, anche se il processo timer viene disabilitato in modo permanente.  
  
## <a name="see-also"></a>Vedere anche  
 [Pianificare un aggiornamento dati &#40;PowerPivot per SharePoint&#41;](schedule-a-data-refresh-powerpivot-for-sharepoint.md)   
 [Configurare l'aggiornamento dati dedicato o l'elaborazione solo query &#40;PowerPivot per SharePoint&#41;](configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint.md)   
 [Configurare l'account di aggiornamento dati automatico PowerPivot &#40;PowerPivot per SharePoint&#41;](configure-unattended-data-refresh-account-powerpivot-sharepoint.md)   
 [Configurare le credenziali archiviate per l'aggiornamento dati PowerPivot &#40;PowerPivot per SharePoint&#41;](configure-stored-credentials-data-refresh-powerpivot-sharepoint.md)  
  
  
