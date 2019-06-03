---
title: Guida dell'Installazione guidata | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
f1_keywords:
- instance configuration, Setup
helpviewer_keywords:
- Instance Name page [SQL Server Installation Wizard]
- SQL Server Installation Wizard, Instance Name page
ms.assetid: 5bf822fc-6dec-4806-a153-e200af28e9a5
author: MashaMSFT
ms.author: mathoma
manager: craigg
robots: noindex,nofollow
ms.openlocfilehash: 06a8b0b4a3e692ca1eaef89e8e7114b41bf650a1
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/21/2019
ms.locfileid: "65993793"
---
# <a name="installation-wizard-help"></a>Guida dell'Installazione guidata
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questo articolo descrive alcune pagine di configurazione della procedura di installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. 

## <a name="instance-configuration"></a>Configurazione dell'istanza
Utilizzare la pagina **Configurazione dell'istanza** dell'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per specificare se creare un'istanza predefinita oppure un'istanza denominata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è già installata, verrà creata un'istanza predefinita a meno che non si specifichi un'istanza denominata.  
  
Ogni istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è costituita da un set distinto di servizi con impostazioni specifiche per le regole di confronto e le altre opzioni. La struttura della directory, la struttura del Registro di sistema e i nomi dei servizi riflettono il nome dell'istanza e un ID di istanza specifico creato durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Un'istanza può essere l'istanza predefinita oppure un'istanza denominata. Il nome dell'istanza predefinita è MSSQLSERVER. Non è necessario che un client specifichi il nome dell'istanza per stabilire una connessione. Un'istanza denominata è determinata dall'utente durante l'installazione. È possibile installare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] come istanza denominata senza prima installare l'istanza predefinita. Indipendentemente dalla versione, l'istanza predefinita può essere costituita solo da un'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per volta.  
  
> [!NOTE]  
> Con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep è possibile specificare il nome dell'istanza quando si completa un'istanza predisposta nella pagina **Configurazione dell'istanza**. È possibile scegliere di configurare l'istanza predisposta che si sta completando come istanza predefinita se non è presente alcuna istanza predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sul computer.  
  
### <a name="multiple-instances"></a>Istanze multiple  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta più istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un singolo server o processore, ma solo un'istanza può costituire l'istanza predefinita, mentre tutte le altre istanze devono essere istanze denominate. Un computer può eseguire più istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] simultaneamente e ciascuna di esse viene eseguita in modo indipendente dalle altre.  
  
 Per ulteriori informazioni, vedere [Maximum Capacity Specifications for SQL Server](../maximum-capacity-specifications-for-sql-server.md).  
  
### <a name="options"></a>Opzioni  
 Solo istanze del cluster di failover: specificare il nome di rete del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Questo nome identifica l'istanza del cluster di failover nella rete.  
  
 Istanza predefinita o denominata: nel determinare se installare un'istanza predefinita o denominata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tenere presenti le informazioni seguenti:  
  
-   Se si intende installare una singola istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in un server di database, l'istanza deve essere predefinita.  
  
-   Utilizzare un'istanza denominata nei casi in cui si prevede di installare più istanze nello stesso computer. Un server può contenere una sola istanza predefinita.  
  
-   In qualsiasi applicazione che prevede l'installazione di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] , questo deve essere installato come istanza denominata. In questo modo è possibile ridurre al minimo i conflitti quando più applicazioni sono installate nello stesso computer.  
  
 **Istanza predefinita**  
 Selezionare questa opzione per installare un'istanza predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Un computer può ospitare una sola istanza predefinita. Tutte le altre istanze devono essere denominate. Se, tuttavia, è installata un'istanza predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è possibile aggiungere un'istanza predefinita di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] nello stesso computer.  
  
 **Istanza denominata**  
 Selezionare questa opzione per creare una nuova istanza denominata. Quando si assegna il nome a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], tenere presenti le considerazioni seguenti:  
  
-   Per i nomi delle istanze non viene fatta distinzione tra maiuscole e minuscole.  
  
-   I nomi delle istanze non possono iniziare né terminare con un carattere di sottolineatura (_).  
  
-   I nomi delle istanze non possono contenere il termine "Default" o altre parole chiave riservate. Se nel nome di un'istanza viene utilizzata una parola chiave riservata, si verificherà un errore di installazione. Per altre informazioni, vedere [Parole chiave riservate &#40;Transact-SQL&#41;](../../t-sql/language-elements/reserved-keywords-transact-sql.md).  
  
-   Se si specifica MSSQLServer per il nome di istanza, verrà creata un'istanza predefinita.  
  
-   Un'installazione di [!INCLUDE[ssGeminiLong](../../includes/ssgeminilong-md.md)] viene sempre eseguita come un'istanza denominata di '[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]'. Non è possibile specificare un nome di istanza diverso per questo ruolo caratteristica.  
  
-   I nomi delle istanze devono essere costituiti al massimo da 16 caratteri.  
  
-   Il primo carattere del nome dell'istanza deve essere una lettera. Le lettere consentite sono quelle definite dallo standard Unicode 2.0 e includono i caratteri latini a-z, A-Z e i caratteri corrispondenti a lettere di altre lingue.  
  
-   I caratteri successivi possono essere costituiti dalle lettere definite dallo standard Unicode 2.0, dai numeri decimali inclusi negli script Latino di base o in altri script nazionali, il simbolo del dollaro ($) o un carattere di sottolineatura (_).  
  
-   Nei nomi di istanza non sono consentiti spazi interni o altri caratteri speciali. La barra rovesciata (\\), la virgola (,) i due punti (:), il punto e virgola (;), la virgoletta singola ('), la e commerciale (&), il segno meno (-) e la chiocciola (@) rappresentano altri caratteri non consentiti.  
  
     Nei nomi di istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è possibile utilizzare solo i caratteri indicati come validi nella tabella codici corrente di Windows. Se viene utilizzato un carattere Unicode non supportato, si verificherà un errore di installazione.  
  
 **Istanze e funzionalità rilevate**  
 È possibile visualizzare un elenco dei componenti e delle istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installati sul computer su cui viene eseguito il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **ID istanza** : per impostazione predefinita, come ID istanza viene usato il nome dell'istanza. Tale nome viene utilizzato per identificare le directory di installazione e le chiavi del Registro di sistema per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si tratta del caso delle istanze predefinite e delle istanze denominate. Per un'istanza predefinita, il nome di istanza e l'ID istanza sono MSSQLSERVER. Per usare un ID istanza non predefinito, specificarlo nel campo **ID istanza** .  
  
> [!IMPORTANT]  
>  Con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep, l'ID istanza visualizzato in questa pagina è quello specificato durante il passaggio relativo alla preparazione dell'immagine del processo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] SysPrep. Non sarà possibile specificare un ID istanza diverso durante il passaggio relativo al completamento dell'immagine.  
  
> [!NOTE]  
>  Gli ID delle istanze che iniziano con un carattere di sottolineatura (_) o che contengono il simbolo del cancelletto (#) o del dollaro ($) non sono supportati.  
  
 Per altre informazioni sulle directory, sui percorsi dei file e sulla denominazione degli ID delle istanze, vedere [Percorsi dei file per le istanze predefinite e denominate di SQL Server](file-locations-for-default-and-named-instances-of-sql-server.md).  
  
 Tutti i componenti di un'istanza specifica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono gestiti come unità. Tutti i Service Pack e gli aggiornamenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verranno applicati a ogni componente di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Tutti i componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che condividono lo stesso nome di istanza devono soddisfare i criteri seguenti:  
  
-   **Stessa versione**   
-   **Stessa edizione**    
-   **Stesse impostazioni della lingua**    
-   **Stesso stato del cluster**    
-   **Stesso sistema operativo**  
  
  
    > [!NOTE]  
    > [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] non riesce a interagire con i cluster.  


## <a name="analysis-services-configuration---account-provisioning"></a>Configurazione di Analysis Services - Provisioning account
  Utilizzare questa pagina per impostare la modalità server e per concedere le autorizzazioni amministrative a utenti o servizi che richiedono l'accesso illimitato ad [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Durante l'installazione non viene aggiunto automaticamente il gruppo locale BUILTIN\Administrators di Windows al ruolo di amministratore del server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dell'istanza che viene installata. Se si desidera aggiungere il gruppo Administrators locale al ruolo di amministratore del server, è necessario specificare in modo esplicito tale gruppo.  
  
 Se si installa [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], accertarsi di concedere le autorizzazioni amministrative agli amministratori di farm SharePoint o agli amministratori di servizi responsabili di una distribuzione server di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] in una farm [!INCLUDE[SPS2010](../../includes/sps2010-md.md)].  
  
### <a name="options"></a>Opzioni  
 **Modalità server** : specifica il tipo di database di Analysis Services che è possibile distribuire nel server. Le modalità del server vengono determinate durante l'installazione e non possono essere modificate successivamente. Le modalità si escludono a vicenda, ovvero saranno necessarie due istanze di Analysis Services, ciascuna configurata per una modalità diversa, in modo da supportare sia la soluzione OLAP classico che quella per il modello tabulare.  
  
 **Specifica amministratori**: è necessario specificare almeno un amministratore del server per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Gli utenti o i gruppi specificati diventeranno membri del ruolo di amministratore del server dell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che viene installata e devono essere account utente di dominio Windows nello stesso dominio del computer in cui viene installato il software.  
  
> [!NOTE]  
>  Controllo account utente è una caratteristica di sicurezza di Windows che richiede a un amministratore di approvare in modo specifico azioni o applicazioni amministrative prima di poterle eseguire. Poiché Controllo account utente è attivato per impostazione predefinita, verrà richiesto di consentire operazioni specifiche che necessitano di privilegi elevati. È possibile configurare Controllo account utente per modificare il comportamento predefinito oppure è possibile personalizzarlo per programmi specifici. Per altre informazioni sul controllo dell'account utente e sulla relativa configurazione, vedere [User Account Control Step by Step Guide](https://go.microsoft.com/fwlink/?linkid=196350) (Guida dettagliata sul controllo dell'account utente in Windows) e [User Account Control (Wikipedia)](https://go.microsoft.com/fwlink/?linkid=196351).  
  
### <a name="see-also"></a>Vedere anche  
 [Configurare gli account del servizio &#40;Analysis Services&#41;](../../analysis-services/instances/configure-service-accounts-analysis-services.md) [Configurare account di servizio e autorizzazioni di Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)  

 ## <a name="analysis-services-configuration---data-directories"></a>Configurazione di Analysis Services - Directory dati
  Le directory predefinite della tabella seguente sono configurabili dall'utente durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. L'autorizzazione per accedere a questi file viene concessa agli amministratori locali e ai membri del gruppo di sicurezza SQLServerMSASUser$\<istanza> creato e di cui viene effettuato il provisioning durante l'installazione.  
  
### <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
  
|Descrizione|Directory predefinita|Indicazioni|  
|-----------------|-----------------------|---------------------|  
|Directory radice dati|C:\Programmi\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Data\ |Assicurarsi che la cartella \Programmi\Microsoft SQL Server\ sia protetta con autorizzazioni limitate. Le prestazioni di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dipendono, in molte configurazioni, dalle prestazioni del sottosistema di archiviazione in cui si trova la directory dei dati. Posizionare tale directory nel sottosistema di archiviazione collegato al sistema in grado di garantire le prestazioni più elevate. Per le installazioni del cluster di failover, assicurarsi che le directory dei dati vengano posizionate nel disco condiviso.|  
|Directory file di log|C:\Programmi\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Log\ |Si tratta della directory per i file di log di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e include il log FlightRecorder. Se si aumenta la durata dell'Utilità Traccia eventi, assicurarsi che la directory dei log disponga di spazio sufficiente.|  
|Directory temporanea|C:\Programmi\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Temp\ |Posizionare la directory temporanea nel sottosistema di archiviazione a elevate prestazioni.|  
|Directory di backup|C:\Programmi\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Backup\ |Si tratta della directory dei file di backup predefiniti di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Per le installazioni di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint, si tratta anche della posizione in cui i servizi di sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] memorizzano nella cache i file di dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].<br /><br /> Verificare che vengano impostate le autorizzazioni appropriate in modo da impedire la perdita di dati e che il gruppo di utenti per il servizio [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] disponga delle autorizzazioni adeguate per la scrittura nella directory di backup. Non è supportato l'utilizzo di un'unità di cui è stato eseguito il mapping per le directory di backup.|  
  
### <a name="notes"></a>Note  
  
-   Le istanze di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] distribuite in una farm di SharePoint archiviano i file dell'applicazione, i file di dati e le proprietà nei database del contenuto e delle applicazioni di servizio.  
  
-   Quando si aggiungono funzionalità a un'installazione esistente, non è possibile modificare il percorso di una caratteristica installata in precedenza, né specificare il percorso di una nuova caratteristica.  

-   Potrebbe essere necessario configurare software di scansione, ad esempio applicazioni antivirus e antispyware, per escludere le cartelle e i tipi di file di SQL Server. Per altre informazioni, vedere questo articolo del supporto: [Come scegliere il software antivirus in esecuzione su computer che eseguono SQL Server](https://support.microsoft.com/kb/309422)
  
-   Se si specificano directory di installazione non predefinite, verificare che le cartelle di installazione siano univoche per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nessuna delle directory presenti in questa finestra di dialogo deve essere condivisa con le directory di altre istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Anche i componenti [!INCLUDE[ssDE](../../includes/ssde-md.md)] e [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] all'interno di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devono essere installati in directory separate.  
  
-   Non è possibile installare file di programma e file di dati nelle situazioni seguenti:  
  
    -   In un'unità disco rimovibile  
  
    -   In un file system che utilizza la compressione  
  
    -   In una directory in cui si trovano i file di sistema  
  
### <a name="see-also"></a>Vedere anche  
 Per altre informazioni sulle directory, sui percorsi dei file e sulla denominazione degli ID delle istanze, vedere [Percorsi dei file per le istanze predefinite e denominate di SQL Server](file-locations-for-default-and-named-instances-of-sql-server.md).  
  

### <a name="analysis-services-configuration---data-directories"></a>Configurazione di Analysis Services - Directory dati
  Le directory predefinite della tabella seguente sono configurabili dall'utente durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. L'autorizzazione per accedere a questi file viene concessa agli amministratori locali e ai membri del gruppo di sicurezza SQLServerMSASUser$\<istanza> creato e di cui viene effettuato il provisioning durante l'installazione.  
  
#### <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
  
|Descrizione|Directory predefinita|Indicazioni|  
|-----------------|-----------------------|---------------------|  
|Directory radice dati |C:\Programmi\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Data |Assicurarsi che la cartella \Programmi\Microsoft SQL Server\ sia protetta con autorizzazioni limitate. Le prestazioni di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] dipendono, in molte configurazioni, dalle prestazioni del sottosistema di archiviazione in cui si trova la directory dei dati. Posizionare tale directory nel sottosistema di archiviazione collegato al sistema in grado di garantire le prestazioni più elevate. Per le installazioni del cluster di failover, assicurarsi che le directory dei dati vengano posizionate nel disco condiviso.|  
|Directory file di log|C:\Programmi\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Log |Si tratta della directory per i file di log di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e include il log FlightRecorder. Se si aumenta la durata dell'Utilità Traccia eventi, assicurarsi che la directory dei log disponga di spazio sufficiente.|  
|Directory temporanea|C:\Programmi\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Temp |Posizionare la directory temporanea nel sottosistema di archiviazione a elevate prestazioni.|  
|Directory di backup|C:\Programmi\Microsoft SQL Server\MSAS*nn*.\<InstanceID>\OLAP\Backup |Si tratta della directory dei file di backup predefiniti di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Per le installazioni di [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] per SharePoint, si tratta anche della posizione in cui i servizi di sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] memorizzano nella cache i file di dati [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)].<br /><br /> Verificare che vengano impostate le autorizzazioni appropriate in modo da impedire la perdita di dati e che il gruppo di utenti per il servizio [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] disponga delle autorizzazioni adeguate per la scrittura nella directory di backup. Non è supportato l'utilizzo di un'unità di cui è stato eseguito il mapping per le directory di backup.|  
  
#### <a name="notes"></a>Note  
  
-   Le istanze di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] distribuite in una farm di SharePoint archiviano i file dell'applicazione, i file di dati e le proprietà nei database del contenuto e delle applicazioni di servizio.  
  
-   Quando si aggiungono funzionalità a un'installazione esistente, non è possibile modificare il percorso di una caratteristica installata in precedenza, né specificare il percorso di una nuova caratteristica.  

-   Potrebbe essere necessario configurare software di scansione, ad esempio applicazioni antivirus e antispyware, per escludere le cartelle e i tipi di file di SQL Server. Per altre informazioni, vedere questo articolo del supporto: [Come scegliere il software antivirus in esecuzione su computer che eseguono SQL Server](https://support.microsoft.com/kb/309422)
  
-   Se si specificano directory di installazione non predefinite, verificare che le cartelle di installazione siano univoche per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nessuna delle directory presenti in questa finestra di dialogo deve essere condivisa con le directory di altre istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Anche i componenti [!INCLUDE[ssDE](../../includes/ssde-md.md)] e [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] all'interno di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devono essere installati in directory separate.  
  
-   Non è possibile installare file di programma e file di dati nelle situazioni seguenti:  
  
    -   In un'unità disco rimovibile  
  
    -   In un file system che utilizza la compressione  
  
    -   In una directory in cui si trovano i file di sistema  
  
#### <a name="see-also"></a>Vedere anche  
 Per altre informazioni sulle directory, sui percorsi dei file e sulla denominazione degli ID delle istanze, vedere [Percorsi dei file per le istanze predefinite e denominate di SQL Server](file-locations-for-default-and-named-instances-of-sql-server.md).  
  
    
 [Autorizzazioni NTFS e di condivisione per un file server](https://go.microsoft.com/fwlink/?LinkID=206571) 

  
## <a name="serverconfig"></a> Configurazione del motore di database - Configurazione del server
  Utilizzare questa pagina per impostare la modalità di sicurezza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e aggiungere utenti o gruppi di Windows come amministratori del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
### <a name="considerations-for-running-includesscurrentincludessscurrent-mdmd"></a>Considerazioni sull'esecuzione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
 Nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]viene eseguito il provisioning del gruppo **BUILTIN\Administrators** come account di accesso nel [!INCLUDE[ssDE](../../includes/ssde-md.md)] e i membri del gruppo Administrators locale possono accedere usando le credenziali di amministratore. L'utilizzo di autorizzazioni elevate non è una procedura consigliata. In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] non viene eseguito il provisioning del gruppo **BUILTIN\Administrators** come account di accesso. Di conseguenza, è consigliabile creare un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per ogni utente amministrativo e aggiungere tale account al ruolo predefinito del server sysadmin durate l'installazione di una nuova istanza di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. È consigliabile eseguire questa operazione anche per gli account di Windows utilizzati per eseguire i processi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, inclusi i processi dell'agente di replica.  
  
### <a name="options"></a>Opzioni  
 **Modalità di sicurezza** : selezionare l'autenticazione di Windows o l'autenticazione mista per l'istallazione.  
  
 **Provisioning entità Windows** : nelle versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]il gruppo locale Builtin\Administrator di Windows era incluso nel ruolo del server sysadmin di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e consentiva agli amministratori di Windows di accedere in modo efficace all'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]il gruppo Builtin\Administrator non è disponibile nel ruolo del server sysadmin. Al contrario, è necessario eseguire in modo esplicito il provisioning degli amministratori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per le nuove installazioni durante l'esecuzione del programma di installazione.  
  
> [!IMPORTANT]  
>  È necessario eseguire il provisioning esplicito degli amministratori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per le nuove installazioni durante l'esecuzione del programma di installazione. Se non si completa questo passaggio, non sarà possibile procedere con l'installazione.  
  
 **Specifica amministratori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** : è necessario specificare almeno un'entità di Windows per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per aggiungere l'account usato per l'esecuzione del programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], fare clic sul pulsante **Utente corrente**. Per aggiungere o rimuovere account dall'elenco degli amministratori di sistema, fare clic su **Aggiungi** o **Rimuovi**, quindi modificare l'elenco di utenti, gruppi o computer con privilegi di amministratore per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Dopo avere modificato l'elenco, scegliere **OK**, quindi verificare l'elenco di amministratori nella finestra di dialogo di configurazione. Quando l'elenco è completo, scegliere **Avanti**.  
  
 Se si seleziona l'autenticazione Modalità mista, è necessario fornire credenziali di accesso per l'account amministratore di sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] predefinito.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)]  
  
 **Modalità di autenticazione di Windows**  
 Quando un utente si connette utilizzando un account utente di Windows, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il nome di account e la password vengono convalidati tramite il token dell'entità di Windows nel sistema operativo. Si tratta della modalità di autenticazione predefinita e garantisce maggiore protezione rispetto alla modalità mista. L'autenticazione di Windows, per la quale viene utilizzato il protocollo di sicurezza Kerberos, garantisce l'applicazione dei criteri password mediante convalida della complessità delle password, fornisce supporto per il blocco dell'account e supporta la scadenza delle password.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteStrongPass](../../includes/ssnotestrongpass-md.md)] Non impostare mai password vuote o vulnerabili.  
  
 **Modalità mista (autenticazione di Windows o autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])**  
 Consente agli utenti di connettersi tramite l'autenticazione di Windows o l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Gli utenti che utilizzano un account utente di Windows per la connessione possono utilizzare connessioni trusted convalidate da Windows.  
  
 Se è necessario selezionare l'autenticazione Modalità mista e utilizzare account di accesso SQL per le applicazioni legacy, sarà necessario impostare password complesse per tutti gli account di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  L'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è disponibile solo per la compatibilità con le versioni precedenti. [!INCLUDE[ssNoteWinAuthentication](../../includes/ssnotewinauthentication-md.md)]  
  
 **Immettere la password**  
 Immettere e confermare l'account di accesso dell'amministratore di sistema (sa). Le password rappresentano la prima forma di difesa contro eventuali intrusi, pertanto l'impostazione di password complesse costituisce una misura di sicurezza fondamentale per la sicurezza del sistema. Non impostare mai password dell'account "sa" vuote o vulnerabili.  
  
> [!NOTE]  
>  Le password di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono contenere da 1 a 128 caratteri, inclusa qualsiasi combinazione di lettere, simboli e numeri. Se si seleziona l'autenticazione Modalità mista, sarà necessario immettere una password dell'account sa complessa prima di passare alla pagina successiva dell'Installazione guidata.  
  
 **Linee guida per la creazione di password complesse**  
 Le password complesse non vengono decifrate facilmente, né da parte degli utenti né mediante l'utilizzo di programmi specifici. Le password complesse non prevedono l'utilizzo di termini o condizioni non consentite, quali:  
  
-   Condizione di spazio vuoto o NULL    
-   'Password'    
-   "Admin"    
-   "Administrator"    
-   "sa"    
-   'sysadmin'  
-   
 Una password complessa non può essere costituita dagli elementi seguenti associati al computer di installazione:  
  
-   Nome dell'utente attualmente connesso al computer.    
-   Nome del computer.  
  
 Una password complessa deve essere formata da più di otto caratteri e soddisfare almeno tre dei quattro criteri seguenti:  
  
-   Deve contenere lettere maiuscole.   
-   Deve contenere lettere minuscole.  
-   Deve contenere numeri.    
-   Deve contenere caratteri non alfanumerici, ad esempio #, % o ^.  
  
 Le password immesse in questa pagina devono soddisfare i requisiti relativi ai criteri password complessi. In presenza di qualsiasi componente di automazione in cui viene utilizzata l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , assicurarsi che la password soddisfi i requisiti relativi ai criteri password complessi.  
  
### <a name="related-content"></a>Contenuto correlato  
 Per ulteriori informazioni sulla scelta tra l'autenticazione di Windows e l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Scegliere una modalità di autenticazione](../../relational-databases/security/choose-an-authentication-mode.md).  
 
 
 Per altre informazioni sulla scelta di un account per l'esecuzione del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)], vedere [Configurare account di servizio e autorizzazioni di Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).
 
## <a name ="datadir"></a> Configurazione del motore di database - Directory dati
  Usare questa pagina per specificare il percorso di installazione per i file di dati e di programma di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]. A seconda del tipo di installazione possono essere supportati i tipi di archivio seguenti: disco locale, spazio di archiviazione condiviso o file server SMB.  
  
 Per specificare una condivisione file SMB come directory, è necessario immettere manualmente il percorso UNC supportato. La selezione di una condivisione file SMB non è supportata. Il formato di un percorso UNC supportato di una condivisione file SMB è \\\NomeServer\NomeCondivisione\\...  
  
### <a name="stand-alone-instance-of-includessnoversionincludesssnoversion-mdmd"></a>Istanza autonoma di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Nella tabella seguente vengono elencati i tipi di archivio supportati e le directory predefinite per un'istanza autonoma di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurabili dall'utente durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
  
|Descrizione|Tipo di archivio supportato|Directory predefinita|Indicazioni|  
|-----------------|----------------------------|-----------------------|---------------------|  
|Directory radice dati|Disco locale, file server SMB, archiviazione condivisa* |C:\Programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\ |Durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono configurati gli elenchi ACL per le directory di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e viene disattivata l'ereditarietà come parte della configurazione.|  
|Directory database utente|Disco locale, file server SMB, archiviazione condivisa*|C:\Programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data |Le procedure consigliate per le directory dei dati dell'utente dipendono dai requisiti del carico di lavoro e delle prestazioni.|  
|Directory log database utente|Disco locale, file server SMB, archiviazione condivisa*|C:\Programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data|Assicurarsi che nella directory del log sia disponibile una quantità di spazio adeguata.|  
|Directory di backup|Disco locale, file server SMB, archiviazione condivisa*|C:\Programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Backup|Impostare le autorizzazioni appropriate in modo da impedire la perdita di dati e assicurarsi che all'account utente per il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengano concesse autorizzazioni adeguate per la scrittura nella directory di backup. Non è supportato l'utilizzo di un'unità di cui è stato eseguito il mapping per le directory di backup.|  
  
 *Anche se i dischi condivisi sono supportati, è consigliabile non usarli per un'istanza autonoma di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="failover-cluster-instance-of-includessnoversionincludesssnoversion-mdmd"></a>Istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Nella tabella seguente vengono elencati i tipi di archivio supportati e le directory predefinite per un'istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurabili dall'utente durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Descrizione|Tipo di archivio supportato|Directory predefinita|Indicazioni|  
|-----------------|----------------------------|-----------------------|---------------------|  
|Directory radice dati|Spazio di archiviazione condiviso, file server SMB|\<Unità:>\Programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\\<br /><br /> Suggerimento: Se nella pagina **Selezione dischi cluster** è stato selezionato un disco condiviso, per impostazione predefinita verrà usato il primo disco condiviso. Se nella pagina **Selezione dischi cluster** non è stata effettuata alcuna selezione, questo campo sarà vuoto per impostazione predefinita.|Durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono configurati gli elenchi ACL per le directory di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e viene disattivata l'ereditarietà come parte della configurazione.|  
|Directory database utente|Spazio di archiviazione condiviso, file server SMB|\<Unità:>Programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data<br /><br /> Suggerimento: Se nella pagina **Selezione dischi cluster** è stato selezionato un disco condiviso, per impostazione predefinita verrà usato il primo disco condiviso. Se nella pagina **Selezione dischi cluster** non è stata effettuata alcuna selezione, questo campo sarà vuoto per impostazione predefinita.|Le procedure consigliate per le directory dei dati dell'utente dipendono dai requisiti del carico di lavoro e delle prestazioni.|  
|Directory log database utente|Spazio di archiviazione condiviso, file server SMB|\<Unità:>\Programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data<br /><br /> Suggerimento: Se nella pagina **Selezione dischi cluster** è stato selezionato un disco condiviso, per impostazione predefinita verrà usato il primo disco condiviso. Se nella pagina **Selezione dischi cluster** non è stata effettuata alcuna selezione, questo campo sarà vuoto per impostazione predefinita.|Assicurarsi che nella directory del log sia disponibile una quantità di spazio adeguata.|  
|Directory di backup|Disco locale, spazio di archiviazione condiviso, file server SMB|\<Unità:>\Programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Backup<br /><br /> Suggerimento: Se nella pagina **Selezione dischi cluster** è stato selezionato un disco condiviso, per impostazione predefinita verrà usato il primo disco condiviso. Se nella pagina **Selezione dischi cluster** non è stata effettuata alcuna selezione, questo campo sarà vuoto per impostazione predefinita.|Impostare le autorizzazioni appropriate in modo da impedire la perdita di dati e assicurarsi che all'account utente per il servizio SQL Server vengano concesse autorizzazioni adeguate per la scrittura nella directory di backup. Non è supportato l'utilizzo di un'unità di cui è stato eseguito il mapping per le directory di backup.|  
  
### <a name="security-considerations"></a>Considerazioni sulla sicurezza  
 Durante l'installazione vengono configurati gli elenchi ACL per le directory di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e viene disattivata l'ereditarietà come parte della configurazione.  
  
 Al file server SMB si applicano le indicazioni seguenti:  
  
-   L'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve essere un account di dominio se viene utilizzato un file server SMB.  
  
-   L'account utilizzato per installare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve disporre delle autorizzazioni FULL CONTROL NTFS nella cartella di condivisione file SMB utilizzata come directory dei dati.  
  
-   È necessario che all'account utilizzato per installare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] venga concesso il privilegio SeSecurityPrivilege nel file server SMB. Per concedere tale privilegio, utilizzare la console Criteri di sicurezza locale nel file server per aggiungere l'account di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ai criteri **Gestione file registro di controllo e di sicurezza** . Questa impostazione è disponibile nella sezione **Assegnazione diritti utente** in **Criteri locali** nella console **Criteri di sicurezza locali** .  
  
### <a name="notes"></a>Note  
  
-   Quando si aggiungono caratteristiche a un'installazione esistente, non è possibile modificare il percorso di una caratteristica installata in precedenza, né specificare il percorso di una nuova caratteristica.  
  
-   Se si specificano directory di installazione non predefinite, verificare che le cartelle di installazione siano univoche per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nessuna delle directory presenti in questa finestra di dialogo deve essere condivisa con le directory di altre istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Anche i componenti [!INCLUDE[ssDE](../../includes/ssde-md.md)] e [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] all'interno di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devono essere installati in directory separate.  
  
-   Non è possibile installare file di programma e file di dati nelle situazioni seguenti:  
  
    -   In un'unità disco rimovibile    
    -   In un file system che utilizza la compressione   
    -   In una directory in cui si trovano i file di sistema    
    -   In un'unità di rete di cui è stato eseguito il mapping in un'istanza del cluster di failover  
  
 
## <a name="a-nametempdba-database-engine-configuration---tempdb"></a><a name="tempdb"><a/> Configurazione del motore di database - TempDB
  Usare questa pagina per specificare posizione, dimensione, impostazioni di espansione e numero di file di log e di dati **tempdb** per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)][!INCLUDE[ssDE](../../includes/ssde-md.md)]. A seconda del tipo di installazione possono essere supportati i tipi di archivio seguenti: disco locale, spazio di archiviazione condiviso o file server SMB.  
  
 Per specificare una condivisione file SMB come directory, è necessario immettere manualmente il percorso UNC supportato. La selezione di una condivisione file SMB non è supportata. Il formato di un percorso UNC supportato di una condivisione file SMB è \\\NomeServer\NomeCondivisione\\...  
  
### <a name="data-and-log-directories-for--a-stand-alone-instance-of--includessnoversionincludesssnoversion-mdmd"></a>Directory di dati e log per un'istanza autonoma di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 La tabella seguente elenca i tipi di archivio supportati e le directory predefinite per le istanze autonome di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurabili dall'utente durante l'installazione.  
  
|Descrizione|Tipo di archivio supportato|Directory predefinita|Indicazioni|  
|-----------------|----------------------------|-----------------------|---------------------|  
|**Directory dati**|Disco locale, file server SMB, spazio di archiviazione condiviso* |C:\Programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data|Durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono configurati gli elenchi ACL per le directory di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e viene disattivata l'ereditarietà come parte della configurazione.<br /><br /> Le procedure consigliate per le directory dei dati del database **tempdb** dipendono dai requisiti del carico di lavoro e delle prestazioni. Specificare più cartelle o unità per distribuire i file di dati su più volumi.|  
|**Directory log**|Disco locale, file server SMB, spazio di archiviazione condiviso*|C:\Programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data|Assicurarsi che nella directory del log sia disponibile una quantità di spazio adeguata.|  
  
 *Anche se i dischi condivisi sono supportati, è consigliabile non usarli per un'istanza autonoma di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="data-and-log-directories-for-a-failover-cluster-instance-of-includessnoversionincludesssnoversion-mdmd"></a>Directory di dati e log per un'istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Nella tabella seguente vengono elencati i tipi di archivio supportati e le directory predefinite per un'istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurabili dall'utente durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Descrizione|Tipo di archivio supportato|Directory predefinita|Indicazioni|  
|-----------------|----------------------------|-----------------------|---------------------|  
|Directory dati**tempdb**|Disco locale, spazio di archiviazione condiviso, file server SMB|\<Unità:>\Programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\Data<br /><br /> Suggerimento: Se nella pagina **Selezione dischi cluster** è stato selezionato un disco condiviso, per impostazione predefinita verrà usato il primo disco condiviso. Se nella pagina **Selezione dischi cluster** non è stata effettuata alcuna selezione, questo campo sarà vuoto per impostazione predefinita.|Durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono configurati gli elenchi ACL per le directory di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e viene disattivata l'ereditarietà come parte della configurazione.<br /><br /> Assicurarsi che la directory (o le directory se vengono specificati più file) sia valida per tutti i nodi del cluster. Durante il failover, se le directory **tempdb** non sono disponibili sul nodo di destinazione del failover, la risorsa di SQL Server non verrà riportata online.|  
|Directory log**tempdb**|Disco locale, spazio di archiviazione condiviso, file server SMB|\<Unità:>\Programmi\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\MSSQL*nn*.\<InstanceID>\MSSQL\Data<br /><br /> Suggerimento: Se nella pagina **Selezione dischi cluster** è stato selezionato un disco condiviso, per impostazione predefinita verrà usato il primo disco condiviso. Se nella pagina **Selezione dischi cluster** non è stata effettuata alcuna selezione, questo campo sarà vuoto per impostazione predefinita.|Le procedure consigliate per le directory dei dati dell'utente dipendono dai requisiti del carico di lavoro e delle prestazioni.<br /><br /> Assicurarsi che la directory specificata sia valida per tutti i nodi del cluster. Durante il failover, se le directory **tempdb** non sono disponibili sul nodo di destinazione del failover, la risorsa di SQL Server non verrà riportata online.<br /><br /> Assicurarsi che nella directory del log sia disponibile una quantità di spazio adeguata.|  
  
### <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
 Configurare le impostazioni di **tempdb** in base alle proprie esigenze in termini di carico di lavoro e requisiti. Le impostazioni seguenti si applicano ai file di dati **tempdb** :  
  
-   **Numero di file** è il numero totale di file di dati **tempdb**. Il valore predefinito è minore di 8 o corrisponde al numero di core logici rilevato durante l'installazione. In generale, se il numero di processori logici è minore o uguale a 8, usare un numero di file di dati pari al numero dei processori logici. Se il numero di processori logici è maggiore di 8, usare 8 file di dati e, se la contesa persiste, aumentare il numero di file di dati per multipli di 4 (fino al numero di processori logici) fino a quando la contesa si riduce a livelli accettabili o modificare il carico di lavoro o codice. 
  
-   **Dimensioni iniziali (MB)** è la dimensione iniziale in MB per ogni file di dati **tempdb** . Il valore predefinito è 8 MB (4 MB per [!INCLUDE[ssexpress](../../includes/ssexpress_md.md)]). [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] introduce dimensioni iniziali massime dei file pari a 262.144 MB (256 GB). Le dimensioni iniziali massime dei file in [!INCLUDE[sssql15](../../includes/sssql15-md.md)] erano 1024 MB. Tutti i file di dati **tempdb** hanno le stesse dimensioni iniziali. Poiché il file **tempdb** viene ricreato a ogni avvio o failover di SQL Server, è necessario specificare una dimensione vicina al valore richiesto dal carico di lavoro per il normale funzionamento. Per ottimizzare ulteriormente la creazione di **tempdb** durante l'avvio, abilitare [Inizializzazione immediata dei file di database](../../relational-databases/databases/database-instant-file-initialization.md).  
  
-   **Dimensioni iniziali totali (MB)** è la dimensione complessiva di tutti i file di dati **tempdb** .  
  
-   **Aumento automatico (MB)** è la quantità di spazio in MB di cui aumenterà automaticamente ogni file di dati **tempdb** quando esaurirà lo spazio. In [!INCLUDE[sssql15](../../includes/sssql15-md.md)] e versioni successive tutti i file di dati aumentano contemporaneamente della quantità specificata in questa impostazione.  
  
-   **Aumento automatico totale (MB)** è la dimensione complessiva di ogni evento di aumento automatico.  
  
-   **Directory dati** mostra tutte le directory contenenti file di dati **tempdb** . Se sono presenti più directory, i file di dati sono collocati nella directory in base a un meccanismo di round robin. Se, ad esempio si creano 3 directory e si specificano 8 file di dati, i file di dati 1, 4 e 7 verranno creati nella prima directory. I file di dati 2, 5 e 8 verranno creati nella seconda directory. I file di dati 3 e 6 saranno nella terza directory.  
  
-   Per aggiungere directory, fare clic su **Aggiungi**.  
  
-   Per rimuovere una directory, selezionarla e fare clic su **Rimuovi**.  
  
 **File di log Tempdb** è il nome del file di log. Viene creato automaticamente. Le impostazioni seguenti si applicano solo ai file di dati **tempdb** :  
  
-   **Dimensioni iniziali (MB)** è la dimensione iniziale del file di log **tempdb** . Il valore predefinito è 8 MB (4 MB per [!INCLUDE[ssexpress](../../includes/ssexpress_md.md)]). [!INCLUDE[sssqlv14](../../includes/sssqlv14-md.md)] introduce dimensioni iniziali massime dei file pari a 262.144 MB (256 GB). Le dimensioni iniziali massime dei file in [!INCLUDE[sssql15](../../includes/sssql15-md.md)] erano 1024 MB. Poiché il file **tempdb** viene ricreato a ogni avvio o failover di SQL Server, è necessario specificare una dimensione vicina al valore richiesto dal carico di lavoro per il normale funzionamento. Per ottimizzare ulteriormente la creazione di **tempdb** durante l'avvio, abilitare [Inizializzazione immediata dei file di database](../../relational-databases/databases/database-instant-file-initialization.md).  
  
-   **Nota: Tempdb** usa la registrazione minima. Non è possibile eseguire il backup del log di **tempdb** . Il database viene ricreato a ogni avvio di SQL Server o in caso di failover di un'istanza del cluster.  
  
-   **Aumento automatico (MB)** indica l'incremento delle dimensioni del log di **tempdb** in megabyte.  Il valore predefinito di 64 MB crea il numero ottimale di file di log virtuali durante l'inizializzazione.  
  
-   **Nota: i file di log Tempdb** non usano l'inizializzazione immediata dei file.  
  
-   **Directory log** è la directory in cui vengono creati i file di log di **tempdb** . È presente una sola directory log di **tempdb** .  
  
### <a name="security-considerations"></a>Considerazioni sulla sicurezza  
 Durante l'installazione vengono configurati gli elenchi ACL per le directory di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e viene disattivata l'ereditarietà come parte della configurazione.  

 Al file server SMB si applicano le indicazioni seguenti:  
  
-   L'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve essere un account di dominio se viene utilizzato un file server SMB.  
  
-   L'account utilizzato per installare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve disporre delle autorizzazioni FULL CONTROL NTFS nella cartella di condivisione file SMB utilizzata come directory dei dati.  
  
-   È necessario che all'account utilizzato per installare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] venga concesso il privilegio SeSecurityPrivilege nel file server SMB. Per concedere tale privilegio, utilizzare la console Criteri di sicurezza locale nel file server per aggiungere l'account di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ai criteri **Gestione file registro di controllo e di sicurezza** . Questa impostazione è disponibile nella sezione **Assegnazione diritti utente** in **Criteri locali** nella console **Criteri di sicurezza locali** .  
  
### <a name="notes"></a>Note  
  
-   Se si specificano directory di installazione non predefinite, verificare che le cartelle di installazione siano univoche per l'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Nessuna delle directory presenti in questa finestra di dialogo deve essere condivisa con le directory di altre istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Anche i componenti [!INCLUDE[ssDE](../../includes/ssde-md.md)] e [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] all'interno di un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devono essere installati in directory separate.  
  
### <a name="see-also"></a>Vedere anche  
 [Configurare account di servizio e autorizzazioni di Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   
 [Autorizzazioni NTFS e di condivisione per un file server](https://go.microsoft.com/fwlink/?LinkID=206571)  

<!--
The MaxDOP setting only applies to SQL Server 2019 and greater
-->

::: moniker range=">=sql-server-ver15||=sqlallproducts-allversions"
## <a name="database-engine-configuration---maxdop"></a>Configurazione del motore di database - MaxDOP
Max degree of parallelism (MaxDOP) determina il numero massimo di processori che una singola istruzione può usare. SQL Server 2019 introduce la configurazione di questa opzione durante l'installazione e rileva automaticamente l'impostazione MaxDOP consigliata per il server in base al numero di core. Il valore massimo predefinito è 8.  

È possibile configurare manualmente questa impostazione qui e modificarla dopo l'installazione. Per altre informazioni, vedere [Max degree of parallelism](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md).
::: moniker-end


## <a name="database-engine-configuration---filestream"></a>Configurazione del Motore di database - Filestream
  Utilizzare questa pagina per abilitare FILESTREAM per l'installazione corrente di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. FILESTREAM integra il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] con un file system NTFS archiviando dati BLOB (Binary Large Object) binari **varbinary(max)** come file nel file system. [!INCLUDE[tsql](../../includes/tsql-md.md)] offre istruzioni che consentono di inserire, aggiornare ed eseguire query, ricerche e back up dei dati FILESTREAM. Le interfacce del file system Win32 forniscono accesso ai dati tramite flusso.  
  
### <a name="uielement-list"></a>Elenco degli elementi di interfaccia  
 **Abilita FILESTREAM per l'accesso Transact-SQL**  
 Selezionare questa opzione per abilitare FILESTREAM per l'accesso [!INCLUDE[tsql](../../includes/tsql-md.md)] . È necessario che questo controllo sia selezionato affinché le altre opzioni di controllo siano disponibili.  
  
 **Abilita FILESTREAM per l'accesso tramite il flusso di I/O dei file**  
 Selezionare questa opzione per abilitare l'accesso tramite flusso Win32 per FILESTREAM.  
  
 **Nome condivisione di Windows**  
 Utilizzare questo controllo per immettere il nome della condivisione di Windows in cui verranno archiviati i dati FILESTREAM.  
  
 **Consenti ai client remoti l'accesso tramite flusso ai dati FILESTREAM**  
 Selezionare questo controllo per consentire ai client remoti di accedere ai dati FILESTREAM nel server corrente.  
  
### <a name="see-also"></a>Vedere anche  
 [Abilitare e configurare FILESTREAM](../../relational-databases/blob/enable-and-configure-filestream.md)   
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  


## <a name="database-engine-configuration---user-instance"></a>Configurazione del Motore di database – Istanze utente
Utilizzare la pagina **Istanze utente** per generare un'istanza distinta del [!INCLUDE[ssDE](../../includes/ssde-md.md)] per gli utenti che non dispongono di autorizzazioni di amministratore, nonché per aggiungere utenti al ruolo di amministratore.  
  
### <a name="option"></a>Opzione  
 Attiva istanze utente  
 Per impostazione predefinita questa opzione è abilitata. Per disabilitare la funzionalità di attivazione delle istanze utente, deselezionare la casella di controllo.  
  
 L'istanza utente, nota anche come istanza figlio o client, è un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] generata dall'istanza padre (l'istanza primaria eseguita come servizio, ad esempio [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]) per conto di un utente. L'istanza utente viene eseguita come processo utente nel contesto di sicurezza di tale utente. L'istanza utente è isolata dall'istanza padre e da qualsiasi altra istanza che viene eseguita nel computer. Questa caratteristica è nota anche come RANU (Run As Normal User).  
  
> [!NOTE]  
>  Per gli account di accesso di cui è stato eseguito il provisioning come membri del ruolo predefinito del server **sysadmin** in fase di configurazione, viene effettuato il provisioning come amministratori nel database dei modelli. Gli account rimarranno membri del ruolo predefinito del server **sysadmin** nell'istanza utente, a meno che non vengano rimossi  
  
 Aggiungi utente al ruolo di amministratore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 Per impostazione predefinita, questa opzione non è abilitata. Per aggiungere l'utente dell'installazione corrente al ruolo di amministratore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , selezionare la casella di controllo.  
  
 Gli utenti di [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] che sono membri di BUILTIN\Administrators non vengono automaticamente aggiunti al ruolo predefinito del server sysadmin quando si connettono a [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. Solo gli utenti di [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)] aggiunti esplicitamente a un ruolo di amministratore a livello di server possono amministrare [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. Tutti i membri del gruppo Built-In\Users possono connettersi all'istanza di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] , ma dispongono di autorizzazioni limitate per l'esecuzione delle operazioni relative al database. Agli utenti che ereditano i privilegi di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] dai gruppi BUILTIN\Administrators e Built-In\Users delle versioni precedenti di Windows devono pertanto essere concessi esplicitamente privilegi amministrativi nelle istanze di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] in esecuzione in [!INCLUDE[wiprlhext](../../includes/wiprlhext-md.md)].  
  
 Per apportare modifiche ai ruoli utente al termine del programma di installazione, utilizzare lo strumento Configurazione superficie di attacco (SQLSAC.exe) di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] . Per aggiornare l'elenco degli utenti nel ruolo di amministratore di sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , fare clic sul collegamento **Aggiungi nuovo amministratore** .  
  
 Verificare che il campo **Utente a cui concedere i privilegi** contenga DomainName\UserName dell'utente le cui autorizzazioni devono essere aggiornate. Nell'elenco delle istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] incluso nel riquadro **Privilegi disponibili** selezionare il ruolo da aggiornare e quindi fare clic sulla freccia a destra. Per aggiungere l'utente a tutti i ruoli disponibili per tutte le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , fare clic sulla doppia freccia a destra.  
  
 Al termine delle selezioni, [!INCLUDE[clickOK](../../includes/clickok-md.md)] per implementare le modifiche apportate. Per chiudere lo strumento senza apportare alcuna modifica, fare clic su **Annulla**.  
  
  
