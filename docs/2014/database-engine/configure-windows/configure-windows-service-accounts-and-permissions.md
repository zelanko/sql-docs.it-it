---
title: Configurare account di servizio e autorizzazioni di Windows | Microsoft Docs
ms.custom: ''
ms.date: 01/28/2020
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- startup service states [SQL Server]
- Setup [SQL Server], user accounts
- Windows permissions [SQL Server]
- modifying user accounts
- default accounts
- domains [SQL Server], user accounts
- startup accounts [SQL Server]
- system accounts [SQL Server]
- services [SQL Server], permissions
- ACL (access control list)
- local system accounts [SQL Server]
- instance-aware services [SQL Server]
- permissions [SQL Server], services
- SQL Server Agent service, user accounts
- Windows NT permissions [SQL Server]
- user accounts [SQL Server]
- identifying instance-unaware services [SQL Server]
- installing SQL Server, user accounts
- disabled startup state [SQL Server]
- user accounts [SQL Server], users
- Local Service account [SQL Server]
- SQL Server Installation Wizard
- instance-unaware services [SQL Server]
- services [SQL Server], configuring at installation
- Windows accounts [SQL Server]
- SQL Server services, user accounts
- user accounts [SQL Server], services
- MSSQLServer
- identifying instance-aware services [SQL Server]
- services [SQL Server], accounts
- access control lists
- optional accounts [SQL Server]
- service accounts [SQL Server]
- accounts [SQL Server], services
- built-in system accounts [SQL Server]
- automatic startup state
- domains [SQL Server]
- manual startup state [SQL Server]
- accounts [SQL Server], user
ms.assetid: 309b9dac-0b3a-4617-85ef-c4519ce9d014
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d2a30aee98be8d15d15cf44113b89d66ca449091
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "76929454"
---
# <a name="configure-windows-service-accounts-and-permissions"></a>Configurare account di servizio e autorizzazioni di Windows
  Ogni servizio in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rappresenta un processo o un set di processi destinato a gestire l'autenticazione delle operazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con Windows. Nel presente argomento viene fornita la descrizione della configurazione predefinita dei servizi disponibili in questa versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e delle opzioni di configurazione per i servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che è possibile impostare durante e dopo l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
##  <a name="Top"></a>Contenuto  
 L'argomento è suddiviso nelle sezioni seguenti:  
  
-   [Servizi installati tramite SQL Server](#Service_Details)  
  
-   [Proprietà e configurazione del servizio](#Serv_Prop)  
  
    -   [Account di servizio predefiniti](#Default_Accts)  
  
        -   [Modifica delle proprietà dell'account](#Changing_Accounts)  
  
    -   [Nuovi tipi di account disponibili con Windows 7 e Windows Server 2008 R2](#New_Accounts)  
  
    -   [Avvio automatico](#Auto_Start)  
  
    -   [Configurazione dei servizi durante l'installazione automatica](#Configure_services)  
  
    -   [Porta del firewall](#Firewall)  
  
-   [Autorizzazioni del servizio](#Serv_Perm)  
  
    -   [Configurazione del servizio e controllo di accesso](#Serv_SID)  
  
    -   [Privilegi e diritti di Windows](#Windows)  
  
    -   [Autorizzazioni del file system concesse a SQL Server SID per servizio o gruppi di Windows locali](#Reviewing_ACLs)  
  
    -   [Autorizzazione del file system concessa ad altri account utente o gruppi di Windows](#File_System_Other)  
  
    -   [Autorizzazioni del file System correlate a posizioni del disco insolite](#Unusual_Locations)  
  
    -   [Esame di considerazioni aggiuntive](#Review_additional_considerations)  
  
    -   [Autorizzazioni del registro di sistema](#Registry)  
  
    -   [WMI](#WMI)  
  
    -   [Named Pipe](#Pipes)  
  
-   [Provisioning](#Provisioning)  
  
    -   [Provisioning di motore di database](#DE_Prov)  
  
        -   [Entità di Windows](#Win_Principals)  
  
        -   [Account sa](#sa)  
  
        -   [SQL Server e privilegi di accesso SID per servizio](#Logins)  
  
        -   [Accesso SQL Server Agent e privilegi](#Agent)  
  
        -   [Istanza di HADRON e del cluster di failover di SQL e privilegi](#Hadron)  
  
        -   [Writer SQL e privilegi](#Writer)  
  
        -   [WMI di SQL e privilegi](#SQLWMI)  
  
    -   [Provisioning di SSAS](#SSAS)  
  
    -   [Provisioning di SSRS](#SSRS)  
  
-   [Aggiornamento da versioni precedenti](#Upgrade)  
  
-   [Appendice](#Appendix)  
  
    -   [Descrizione degli account del servizio](#Serv_Accts)  
  
    -   [Identificazione di servizi specifici dell'istanza e non compatibili con l'istanza](#Identify_instance_aware_and_unaware)  
  
    -   [Nomi dei servizi localizzati](#Localized_service_names)  
  
##  <a name="Service_Details"></a>Servizi installati da[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
 A seconda dei componenti selezionati, durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono installati i servizi seguenti:  
  
-   Servizi di database: il servizio per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] il relazionale [!INCLUDE[ssDE](../../includes/ssde-md.md)]. ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ** Il file eseguibile è \<MSSQLPATH>\MSSQL\Binn\sqlservr.exe.  
  
-   Agent: consente l'esecuzione di processi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il monitoraggio, la generazione di avvisi e l'automazione di alcune attività amministrative. ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ** Il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent è presente ma disabilitato nelle istanze di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]. Il file eseguibile è \<MSSQLPATH>\MSSQL\Binn\sqlagent.exe.  
  
-   **[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]**-Fornisce Online Analytical Processing (OLAP) e data mining funzionalità per business intelligence applicazioni. Il file eseguibile è \<MSSQLPATH>\OLAP\Bin\msmdsrv.exe.  
  
-   **[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]**-Gestisce, esegue, crea, pianifica e recapita report. Il file eseguibile è \<MSSQLPATH>\Reporting Services\ReportServer\Bin\ReportingServicesService.exe.  
  
-   **[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]**: Fornisce il supporto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] gestione per l'archiviazione e l'esecuzione di pacchetti. Il percorso dell'eseguibile è \<MSSQLPATH> \120\dts\binn\msdtssrvr.exe  
  
-   Browser: servizio di risoluzione dei nomi che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornisce informazioni di connessione per i computer client. ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ** Il percorso dell'eseguibile è c:\Programmi (x86)\Microsoft SQL Server\90\Shared\sqlbrowser.exe  
  
-   **Ricerca full-text** : consente di creare rapidamente indici full-text sul contenuto e sulle proprietà dei dati strutturati e semistrutturati nelle per fornire filtri dei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]documenti e suddivisione in parole per.  
  
-   **Writer SQL** : consente alle applicazioni di backup e ripristino di operare nel Framework servizio Copia Shadow del volume (VSS).  
  
-   Riesecuzione distribuita controller: fornisce un'orchestrazione di riproduzione della traccia tra più computer riesecuzione distribuita client. ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **  
  
-   Riesecuzione distribuita client: uno o più computer riesecuzione distribuita client che interagiscono con un controller di riesecuzione distribuita per simulare carichi di lavoro simultanei su un' [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]istanza del. ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **  
  
##  <a name="Serv_Prop"></a>Proprietà e configurazione del servizio  
 Gli account di avvio usati per avviare ed eseguire [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono essere [account utenti di dominio](#Domain_User), [account utenti locali](#Local_User), [account dei servizi gestiti](#MSA), [account virtuali](#VA_Desc)oppure [account di sistema predefiniti](#Local_Service). Per essere avviato ed eseguito, ogni servizio in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve disporre di un account di avvio configurato durante l'installazione.  
  
 In questa sezione sono descritti gli account che possono essere configurati per avviare servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], i valori predefiniti usati dal programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], il concetto di SID per servizio, le opzioni di avvio e la configurazione del firewall.  
  
-   [Account di servizio predefiniti](#Default_Accts)  
  
-   [Avvio automatico](#Auto_Start)  
  
-   [Configurazione del servizio StartupType](#Configure_services)  
  
-   [Porta del firewall](#Firewall)  
  
###  <a name="Default_Accts"></a>Account di servizio predefiniti  
 Nella tabella sono vengono elencati gli account di servizio predefiniti usati dall'installazione quando si istallano tutti i componenti. Gli account predefiniti elencati sono gli account consigliati, ad eccezione dei casi indicati.  
  
 **Server autonomo o controller di dominio**  
  
|Componente|[!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]|Windows 7 e [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] R2 e versioni successive|  
|---------------|------------------------------------|----------------------------------------------------------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)]|[NETWORK SERVICE](#Network_Service)|[Account virtuale](#VA_Desc)<sup>*</sup>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Agente|[NETWORK SERVICE](#Network_Service)|[Account virtuale](#VA_Desc)<sup>*</sup>|  
|[!INCLUDE[ssAS](../../includes/ssas-md.md)]|[NETWORK SERVICE](#Network_Service)|[Account virtuale](#VA_Desc)<sup>*</sup>|  
|[!INCLUDE[ssIS](../../includes/ssis-md.md)]|[NETWORK SERVICE](#Network_Service)|[Account virtuale](#VA_Desc)<sup>*</sup>|  
|[!INCLUDE[ssRS](../../includes/ssrs.md)]|[NETWORK SERVICE](#Network_Service)|[Account virtuale](#VA_Desc)<sup>*</sup>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Controller Riesecuzione distribuita|[NETWORK SERVICE](#Network_Service)|[Account virtuale](#VA_Desc)<sup>*</sup>|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Client di Riesecuzione distribuita|[NETWORK SERVICE](#Network_Service)|[Account virtuale](#VA_Desc)<sup>*</sup>|  
|Utilità di avvio FD (ricerca full-text)|[SERVIZIO LOCALE](#Local_Service)|[Account virtuale](#VA_Desc)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Browser|[SERVIZIO LOCALE](#Local_Service)|[SERVIZIO LOCALE](#Local_Service)|  
|
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VSS Writer|[SISTEMA LOCALE](#Local_System)|[SISTEMA LOCALE](#Local_System)|  
  
 <sup>*</sup>Quando sono necessarie risorse esterne [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al computer, [!INCLUDE[msCoName](../../includes/msconame-md.md)] consiglia di usare un account del servizio gestito (MSA), configurato con i privilegi minimi necessari.  
  
 **SQL Server istanza del cluster di failover**  
  
|Componente|[!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]|[!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)]R2|  
|---------------|------------------------------------|---------------------------------------|  
|[!INCLUDE[ssDE](../../includes/ssde-md.md)]|No. Fornire un account [utente di dominio](#Domain_User) .|Fornire un account [utente di dominio](#Domain_User) .|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Agente|No. Fornire un account [utente di dominio](#Domain_User) .|Fornire un account [utente di dominio](#Domain_User) .|  
|[!INCLUDE[ssAS](../../includes/ssas-md.md)]|No. Fornire un account [utente di dominio](#Domain_User) .|Fornire un account [utente di dominio](#Domain_User) .|  
|[!INCLUDE[ssIS](../../includes/ssis-md.md)]|[NETWORK SERVICE](#Network_Service)|[Account virtuale](#VA_Desc)|  
|[!INCLUDE[ssRS](../../includes/ssrs.md)]|[NETWORK SERVICE](#Network_Service)|[Account virtuale](#VA_Desc)|  
|Utilità di avvio FD (ricerca full-text)|[SERVIZIO LOCALE](#Local_Service)|[Account virtuale](#VA_Desc)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Browser|[SERVIZIO LOCALE](#Local_Service)|[SERVIZIO LOCALE](#Local_Service)|  
|
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VSS Writer|[SISTEMA LOCALE](#Local_System)|[SISTEMA LOCALE](#Local_System)|  
  
####  <a name="Changing_Accounts"></a>Modifica delle proprietà dell'account  
  
> [!IMPORTANT]
>  -   Usare sempre strumenti [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ad esempio Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , per modificare l'account usato dai servizi [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent oppure per modificare la password per l'account. Oltre alla modifica del nome dell'account, Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente di eseguire operazioni di configurazione aggiuntive, quali l'aggiornamento dell'archivio di sicurezza locale di Windows, tramite cui viene protetta la chiave master del servizio per il [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Altri strumenti, ad esempio Gestione controllo servizi di Windows, consentono di modificare il nome dell'account, ma non tutte le impostazioni necessarie.  
> -   Per le istanze di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] che vengono distribuite in una farm di SharePoint, usare sempre Amministrazione centrale SharePoint per modificare gli account server per le applicazioni [!INCLUDE[ssGeminiMTS](../../includes/ssgeminimts-md.md)] e il [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)]. Quando si usa Amministrazione centrale, le impostazioni e le autorizzazioni associate vengono aggiornate per l'uso delle nuove informazioni sull'account.  
> -   Per modificare le opzioni di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , usare il relativo strumento di configurazione.  
  
###  <a name="New_Accounts"></a>Nuovi tipi di account disponibili con Windows 7 e Windows Server 2008 R2  
 Windows 7 e Windows Server 2008 R2 offrono due nuovi tipi di account del servizio denominati account del servizio gestito e account virtuali. Tali account sono progettati per offrire ad applicazioni importanti, come [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , l'isolamento dei relativi account, in modo che non sia più necessario che un amministratore amministri manualmente il nome dell'entità servizio e le credenziali per questi account. Inoltre, grazie a questi account, la gestione a lungo termine di utenti di account di servizio, di password e di nomi SPN è più semplice.  
  
-   <a name="MSA"></a> **Account del servizio gestiti**  
  
     Un account del servizio gestito è un tipo di account di dominio creato e gestito dal controller di dominio. Viene assegnato al computer di un singolo membro per l'esecuzione di un servizio e la password viene gestita automaticamente dal controller di dominio. Non è possibile usare un account del servizio gestito per accedere a un computer, tuttavia tale account può essere usato da un computer per l'avvio di un servizio Windows. Un account del servizio gestito consente di registrare un nome dell'entità servizio (SPN) con Active Directory Un MSA è denominato con un **$** suffisso, ad esempio **DOMAIN\ACCOUNTNAME $**. Quando si specifica un account del servizio gestito, lasciare la password vuota. Dal momento che un account del servizio gestito viene assegnato a un singolo computer, non può essere usato in nodi diversi di un cluster Windows.  
  
    > [!NOTE]  
    >  Questo tipo di account deve essere creato in Active Directory dall'amministratore di dominio prima che possa essere usato dal programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per i servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
    
-  <a name="GMSA"></a>**Account del servizio gestito del gruppo**  
  
     Un account del servizio gestito di gruppo è un account del servizio gestito per più server. Windows gestisce un account del servizio per i servizi in esecuzione in un gruppo di server. Active Directory aggiorna automaticamente la password dell'account del servizio gestito di gruppo senza riavviare i servizi. È possibile configurare servizi di SQL Server per l'uso di un'entità di account del servizio gestito di gruppo. A partire da SQL Server 2014, SQL Server supporta gli account del servizio gestito di gruppo in Windows Server 2012 R2 e versioni successive per istanze autonome, istanze del cluster di failover e gruppi di disponibilità.  
  
    Per usare un account del servizio gestito di gruppo per SQL Server 2014 o versioni successive, il sistema operativo deve essere Windows Server 2012 R2 o versioni successive. I server con Windows Server 2012 R2 richiedono l'applicazione di [KB 2998082](https://support.microsoft.com/kb/2998082) in modo che i servizi possano accedere senza interruzioni immediatamente dopo una modifica della password.  
  
    Per altre informazioni, vedere [Account dei servizi gestiti di gruppo](https://technet.microsoft.com/library/hh831782.aspx)  
      
    > [!NOTE]  
    >  L'account del servizio gestito di gruppo deve essere creato in Active Directory dall'amministratore di dominio prima che possa essere usato dal programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per i servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . 
  
-   <a name="VA_Desc"></a>**Account virtuali**  
  
     Gli account virtuali a partire da Windows Server 2008 R2 e Windows 7 sono *account locali gestiti* che forniscono le funzionalità seguenti per semplificare l'amministrazione dei servizi. L'account virtuale è gestito automaticamente e consente di accedere alla rete in un ambiente di dominio. Se durante [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] l'installazione viene utilizzato il valore predefinito per gli account del servizio, viene utilizzato un account virtuale che utilizza il nome dell'istanza come nome del servizio, nel formato **NT Service\\**_\<ServiceName>_. I servizi eseguiti come account virtuali accedono alle risorse di rete usando le credenziali dell'account del computer nel formato _<domain_name>_ **\\** _<computer_name>_ **$**.  Quando si specifica un account virtuale per avviare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], lasciare vuoto il campo della password. Se tramite l'account virtuale non è possibile registrare il nome dell'entità servizio (SPN), registrarlo manualmente. Per altre informazioni sulla registrazione manuale di un SPN, vedere [Registrazione manuale del nome SPN](register-a-service-principal-name-for-kerberos-connections.md#Manual).  
  
    > [!NOTE]  
    >  Non è possibile usare gli account virtuali per l'istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , poiché non dispongono dello stesso SID in ogni nodo del cluster.  
  
     Nella tabella seguente sono elencati esempi di nomi di account virtuali.  
  
    |Service|Nome dell'account virtuale|  
    |-------------|--------------------------|  
    |Istanza predefinita del servizio [!INCLUDE[ssDE](../../includes/ssde-md.md)]|**NT SERVICE\MSSQLSERVER**|  
    |Istanza denominata di un servizio [!INCLUDE[ssDE](../../includes/ssde-md.md)] denominato **PAYROLL**|**NT SERVICE\MSSQL $ PAYROLL**|  
    |
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent nell'istanza predefinita di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|**NT SERVICE\SQLSERVERAGENT**|  
    |[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Servizio Agent in un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] denominata **Payroll**|**NT SERVICE\SQLAGENT $ PAYROLL**|  
  
 Per altre informazioni sugli account dei servizi gestiti e sugli account virtuali, vedere la sezione **Concetti relativi agli account dei servizi gestiti e agli account virtuali** nella pagina [Guida dettagliata agli account di servizio](https://technet.microsoft.com/library/dd548356\(WS.10\).aspx) e la pagina relativa alle [domande frequenti sugli account dei servizi gestiti](https://technet.microsoft.com/library/ff641729\(WS.10\).aspx).  
  
 **Nota sulla sicurezza:** [!INCLUDE[ssNoteLowRights](../../includes/ssnotelowrights-md.md)] quando possibile, usare un account [MSA](#MSA) o un [account virtuale](#VA_Desc) . In alternativa, usare un account utente con privilegi limitati o un account di dominio specifico anziché un account condiviso per i servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , assegnando account distinti ai diversi servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Non concedere autorizzazioni aggiuntive all'account del servizio oppure ai gruppi di servizi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Le autorizzazioni verranno concesse mediante l'appartenenza a un gruppo o direttamente a un SID del servizio, se quest'ultimo è supportato.  
  
###  <a name="Auto_Start"></a>Avvio automatico  
 Oltre agli account utente, ogni servizio dispone di tre stati possibili di avvio controllabili dagli utenti:  
  
-   **Disabilitato** Il servizio è installato ma non è attualmente in esecuzione.  
  
-   **Manuale** Il servizio è installato ma verrà avviato solo quando ne sono necessarie funzionalità per un altro servizio o un'altra applicazione.  
  
-   **Automatico** Il servizio viene avviato automaticamente dal sistema operativo.  
  
 Lo stato di avvio viene selezionato durante l'installazione. Quando si installa un'istanza denominata, il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser deve essere impostato per l'avvio automatico.  
  
###  <a name="Configure_services"></a>Configurazione dei servizi durante l'installazione automatica  
 Nella tabella seguente vengono indicati i servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurabili durante l'installazione. Per le installazioni automatiche, è possibile usare le opzioni in un file di configurazione o al prompt dei comandi.  
  
|Nome del servizio SQL Server|Opzioni per le installazioni automatiche<sup>1</sup>|  
|-----------------------------|-------------------------------------------------------|  
|MSSQLSERVER|SQLSVCACCOUNT, SQLSVCPASSWORD, SQLSVCSTARTUPTYPE|  
|SQLServerAgent<sup>2</sup>|AGTSVCACCOUNT, AGTSVCPASSWORD, AGTSVCSTARTUPTYPE|  
|MSSQLServerOLAPService|ASSVCACCOUNT, ASSVCPASSWORD, ASSVCSTARTUPTYPE|  
|ReportServer|RSSVCACCOUNT, RSSVCPASSWORD, RSSVCSTARTUPTYPE|  
|[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|ISSVCACCOUNT, ISSVCPASSWORD, ISSVCSTARTUPTYPE|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Controller Riesecuzione distribuita|DRU_CTLR, CTLRSVCACCOUNT, CTLRSVCPASSWORD, CTLRSTARTUPTYPE, CTLRUSERS|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Client di Riesecuzione distribuita|DRU_CLT, CLTSVCACCOUNT, CLTSVCPASSWORD, CLTSTARTUPTYPE, CLTCTLRNAME, CLTWORKINGDIR, CLTRESULTDIR|  
  
 <sup>1</sup> Per ulteriori informazioni e una sintassi di esempio per le installazioni automatiche, vedere [Install SQL Server 2014 dal prompt dei comandi](../install-windows/install-sql-server-from-the-command-prompt.md).  
  
 <sup>2</sup> Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servizio Agent è disabilitato nelle istanze [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] e with Advanced Services.  
  
###  <a name="Firewall"></a>Porta del firewall  
 Nella maggior parte dei casi, al momento dell'installazione iniziale, è possibile connettersi al [!INCLUDE[ssDE](../../includes/ssde-md.md)] mediante strumenti quali [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] installati nello stesso computer di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. L'installazione di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non consente di aprire porte in Windows Firewall. Connessioni da altri computer potrebbero non essere possibili finché il [!INCLUDE[ssDE](../../includes/ssde-md.md)] non è configurato per essere in ascolto su una porta TCP e la porta appropriata non viene aperta per le connessioni in Windows Firewall. Per altre informazioni, vedere [Configurare Windows Firewall per consentire l'accesso a SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
##  <a name="Serv_Perm"></a>Autorizzazioni del servizio  
 In questa sezione vengono descritte le autorizzazioni configurate dal programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per i SID per servizio dei servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   [Configurazione del servizio e controllo di accesso](#Serv_SID)  
  
-   [Privilegi e diritti di Windows](#Windows)  
  
-   [Autorizzazioni del file system concesse a SQL Server SID per servizio o gruppi di Windows locali SQL Server](#Reviewing_ACLs)  
  
-   [Autorizzazioni del file system concesse ad altri account utente o gruppi di Windows](#File_System_Other)  
  
-   [Autorizzazioni del file System correlate a posizioni del disco insolite](#Unusual_Locations)  
  
-   [Esame di considerazioni aggiuntive](#Review_additional_considerations)  
  
-   [Autorizzazioni del registro di sistema](#Registry)  
  
-   [WMI](#WMI)  
  
-   [Named Pipe](#Pipes)  
  
###  <a name="Serv_SID"></a>Configurazione del servizio e controllo di accesso  
 
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] abilita SID per servizio per ognuno dei servizi in modo da fornire isolamento e protezione avanzata dei servizi. Il SID per servizio deriva dal nome del servizio ed è univoco per il servizio. Ad esempio, un nome di SID del servizio [!INCLUDE[ssDE](../../includes/ssde-md.md)] per il servizio potrebbe essere **NT SERVICE\MSSQL $**_\<NomeIstanza>_. Attraverso l'isolamento, è possibile accedere a oggetti specifici anche se non vengono eseguiti in un account con privilegi elevati e senza indebolire la sicurezza dell'oggetto. Mediante una voce di controllo di accesso contenente un SID del servizio, un servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può limitare l'accesso alle proprie risorse.  
  
> [!NOTE]  
>  In Windows 7, [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] R2 e versioni successive il SID per servizio può essere l'account virtuale usato dal servizio.  
  
 Per la maggior parte dei componenti, l'elenco di controllo di accesso (ACL) per l'account per servizio viene configurato direttamente da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , pertanto è possibile modificare l'account di servizio senza dover ripetere il processo ACL per le risorse.  
  
 Quando si installa [!INCLUDE[ssAS](../../includes/ssas-md.md)], vengono creati un SID per servizio per il servizio [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Viene creato un gruppo di Windows locale, denominato nel formato **SQLServerMSASUser $**_computer_name_**$**_instance_name_. Al nome SID per servizio **NT SERVICE\MSSQLServerOLAPService** viene concessa l'appartenenza al gruppo locale di Windows e a tale gruppo vengono concesse le autorizzazioni appropriate nell'elenco ACL. Se l'account usato per avviare il servizio [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene modificato, tramite Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devono essere modificate alcune autorizzazioni di Windows, ad esempio il diritto di accedere come servizio. Le autorizzazioni assegnate al gruppo locale di Windows saranno tuttavia ancora disponibili senza alcun aggiornamento, perché il SID per servizio non è stato modificato. Questo metodo consente di rinominare il servizio [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] durante gli aggiornamenti.  
  
 Durante l'installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tramite il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] vengono creati gruppi locali di Windows per [!INCLUDE[ssAS](../../includes/ssas-md.md)] e il servizio Browser [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per tali servizi, in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene configurato l'elenco ACL per i gruppi locali di Windows.  
  
 A seconda della configurazione del servizio, l'account del servizio o il SID del servizio viene aggiunto come membro del gruppo di servizi durante l'installazione o l'aggiornamento.  
  
###  <a name="Windows"></a>Privilegi e diritti di Windows  
 L'account assegnato per l'avvio di un servizio deve disporre delle **autorizzazioni di avvio, arresto e pausa** per il servizio, che verranno assegnate automaticamente dal programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  Installare innanzitutto gli strumenti di amministrazione remota del server (RSAT). Per informazioni vedere la pagina relativa agli [strumenti di amministrazione remota del server per Windows 7](https://www.microsoft.com/download/details.aspx?id=7887).  
  
 Nella tabella seguente vengono mostrate le autorizzazioni richieste dal programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per i SID per servizio o per i gruppi locali di Windows usati dai componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Servizio|Autorizzazioni concesse dal programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|  
|---------------------------------------|------------------------------------------------------------|  
|**[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]:**<br /><br /> Tutti i diritti vengono concessi al SID per servizio. Istanza predefinita: **NT SERVICE\MSSQLSERVER**. Istanza denominata: **NT SERVICE\MSSQL$** NomeIstanza.|**Accesso come servizio** (SeServiceLogonRight)<br /><br /> **Sostituire un token a livello di processo** (SeAssignPrimaryTokenPrivilege)<br /><br /> **Ignora controllo incrociato** (SeChangeNotifyPrivilege)<br /><br /> **Regolazione delle quote di memoria per un processo** (SeIncreaseQuotaPrivilege)<br /><br /> Autorizzazione all'avvio del writer SQL<br /><br /> Autorizzazione di lettura del servizio Registro eventi<br /><br /> Autorizzazione di lettura del servizio RPC (Remote Procedure Call)|  
|Agente: <sup>1</sup> ** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **<br /><br /> Tutti i diritti vengono concessi al SID per servizio. Istanza predefinita: **NT Service\SQLSERVERAGENT**. Istanza denominata: **NT Service\SQLAGENT$**_NomeIstanza_).|**Accesso come servizio** (SeServiceLogonRight)<br /><br /> **Sostituire un token a livello di processo** (SeAssignPrimaryTokenPrivilege)<br /><br /> **Ignora controllo incrociato** (SeChangeNotifyPrivilege)<br /><br /> **Regolazione delle quote di memoria per un processo** (SeIncreaseQuotaPrivilege)|  
|**[!INCLUDE[ssAS](../../includes/ssas-md.md)]:**<br /><br /> Tutti i diritti vengono concessi a un gruppo locale di Windows. Istanza predefinita: **SQLServerMSASUser$**_NomeComputer_**$MSSQLSERVER**. Istanza denominata: **SQLServerMSASUser $**_nomecomputer_**$**_NomeIstanza_. [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)]istanza: **SQLServerMSASUser $**_nomecomputer_**$**_PowerPivot_.|**Accesso come servizio** (SeServiceLogonRight)<br /><br /> Solo per tabulare:<br /><br /> **Aumentare un working set di processo** (SeIncreaseWorkingSetPrivilege)<br /><br /> **Regolazione delle quote di memoria per un processo** (SeIncreaseQuotaSizePrivilege)<br /><br /> **Lock Pages in Memory** (SeLockMemoryPrivilege): questo è necessario solo quando il paging è disattivato completamente.<br /><br /> Solo per installazioni di cluster di failover:<br /><br /> **Aumento della priorità di pianificazione** (SeIncreaseBasePriorityPrivilege)|  
|**[!INCLUDE[ssRS](../../includes/ssrs.md)]:**<br /><br /> Tutti i diritti vengono concessi al SID per servizio. Istanza predefinita: **NT SERVICE\ReportServer**. Istanza denominata: **NT Service\\**_NomeIstanza_).|**Accesso come servizio** (SeServiceLogonRight)|  
|**[!INCLUDE[ssIS](../../includes/ssis-md.md)]:**<br /><br /> Tutti i diritti vengono concessi al SID per servizio. Istanza predefinita e istanza denominata: **NT SERVICE\MsDtsServer120**. 
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] non ha un processo separato per un'istanza denominata).|**Accesso come servizio** (SeServiceLogonRight)<br /><br /> Autorizzazione di scrittura sul registro eventi applicazioni<br /><br /> **Ignora controllo incrociato** (SeChangeNotifyPrivilege)<br /><br /> **Rappresenta un client dopo l'autenticazione** (SeImpersonatePrivilege)|  
|**Ricerca full-text:**<br /><br /> Tutti i diritti vengono concessi al SID per servizio. Istanza predefinita: **NT Service\MSSQLFDLauncher**. Istanza denominata: **NT Service\ MSSQLFDLauncher$**_NomeIstanza_.|**Accesso come servizio** (SeServiceLogonRight)<br /><br /> **Regolazione delle quote di memoria per un processo** (SeIncreaseQuotaPrivilege)<br /><br /> **Ignora controllo incrociato** (SeChangeNotifyPrivilege)|  
|**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Browser:**<br /><br /> Tutti i diritti vengono concessi a un gruppo locale di Windows. Istanza predefinita o denominata: **SQLServer2005SQLBrowserUser**_$ComputerName_. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser non dispone di un processo separato per un'istanza denominata.|**Accesso come servizio** (SeServiceLogonRight)|  
|**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]VSS Writer:**<br /><br /> Tutti i diritti vengono concessi al SID per servizio. Istanza predefinita o denominata: **NT Service\SQLWriter**. 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VSS Writer non usa un processo separato per un'istanza denominata.|Il servizio SQLWriter è in esecuzione con l'account LOCAL SYSTEM che dispone di tutte le autorizzazioni necessarie. Il programma di installazione di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non controlla né concede le autorizzazioni per questo servizio.|  
|**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Controller Riesecuzione distribuita:**|**Accesso come servizio** (SeServiceLogonRight)|  
|**[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Client di Riesecuzione distribuita:**|**Accesso come servizio** (SeServiceLogonRight)|  
  
 <sup>1</sup> Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servizio Agent è disabilitato nelle istanze [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]di.  
  
###  <a name="Reviewing_ACLs"></a>Autorizzazioni del file system concesse a SQL Server SID per servizio o gruppi di Windows locali  
 Gli account del servizio di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devono disporre dell'accesso alle risorse. Gli elenchi di controllo di accesso sono impostati per il SID per servizio o per il gruppo locale di Windows.  
  
> [!IMPORTANT]  
>  Per le installazioni di cluster di failover, le risorse presenti in dischi condivisi devono essere impostate su un elenco di controllo di accesso per un account locale.  
  
 Nella tabella seguente sono indicati gli elenchi di controllo di accesso impostati dal programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Account del servizio per|File e cartelle|Accesso|  
|-------------------------|-----------------------|------------|  
|MSSQLServer|Instid\MSSQL\backup|Controllo completo|  
||Instid\MSSQL\binn|Lettura, Esecuzione|  
||Instid\MSSQL\data|Controllo completo|  
||Instid\MSSQL\FTData|Controllo completo|  
||Instid\MSSQL\Install|Lettura, Esecuzione|  
||Instid\MSSQL\Log|Controllo completo|  
||Instid\MSSQL\Repldata|Controllo completo|  
||120\shared|Lettura, Esecuzione|  
||Instid\MSSQL\Template Data (solo[!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] )|Lettura|  
|SQLServerAgent<sup>1</sup>|Instid\MSSQL\binn|Controllo completo|  
||Instid\MSSQL\binn|Controllo completo|  
||Instid\MSSQL\Log|Lettura, Scrittura, Eliminazione, Esecuzione|  
||120\com|Lettura, Esecuzione|  
||120\shared|Lettura, Esecuzione|  
||120\shared\Errordumps|Lettura, Scrittura|  
||ServerName\EventLog|Controllo completo|  
|FTS|Instid\MSSQL\FTData|Controllo completo|  
||Instid\MSSQL\FTRef|Lettura, Esecuzione|  
||120\shared|Lettura, Esecuzione|  
||120\shared\Errordumps|Lettura, Scrittura|  
||Instid\MSSQL\Install|Lettura, Esecuzione|  
||Instid\MSSQL\jobs|Lettura, Scrittura|  
|MSSQLServerOLAPService|120\shared\ASConfig|Controllo completo|  
||Instid\OLAP|Lettura, Esecuzione|  
||Instid\Olap\Data|Controllo completo|  
||Instid\Olap\Log|Lettura, Scrittura|  
||Instid\OLAP\Backup|Lettura, Scrittura|  
||Instid\OLAP\Temp|Lettura, Scrittura|  
||120\shared\Errordumps|Lettura, Scrittura|  
|ReportServer|Instid\Reporting Services\Log Files|Lettura, Scrittura, Eliminazione|  
||Instid\Reporting Services\ReportServer|Lettura, Esecuzione|  
||Services\ReportServer\global.asax Instid\Reporting|Controllo completo|  
||Services\ReportServer\rsreportserver.config Instid\Reporting|Lettura|  
||Instid\Reporting Services\reportManager|Lettura, Esecuzione|  
||Instid\Reporting Services\RSTempfiles|Lettura, Scrittura, Esecuzione, Eliminazione|  
||120\shared|Lettura, Esecuzione|  
||120\shared\Errordumps|Lettura, Scrittura|  
|MSDTSServer100|120\dts\binn\MsDtsSrvr.ini.xml|Lettura|  
||120\dts\binn|Lettura, Esecuzione|  
||120\shared|Lettura, Esecuzione|  
||120\shared\Errordumps|Lettura, Scrittura|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Browser|120\shared\ASConfig|Lettura|  
||120\shared|Lettura, Esecuzione|  
||120\shared\Errordumps|Lettura, Scrittura|  
|SQLWriter|N/D (eseguito come sistema locale)||  
|Utente|Instid\MSSQL\binn|Lettura, Esecuzione|  
||Instid\Reporting Services\ReportServer|Lettura, Esecuzione, Visualizzazione contenuto cartella|  
||Services\ReportServer\global.asax Instid\Reporting|Lettura|  
||Instid\Reporting Services\reportManager|Lettura, Esecuzione|  
||Instid\Reporting Services\ReportManager\pages|Lettura|  
||Instid\Reporting Services\ReportManager\Styles|Lettura|  
||120\dts|Lettura, Esecuzione|  
||120\tools|Lettura, Esecuzione|  
||100\tools|Lettura, Esecuzione|  
||90\tools|Lettura, Esecuzione|  
||80\tools|Lettura, Esecuzione|  
||120\sdk|Lettura|  
||Microsoft SQL Server\120\Setup Bootstrap|Lettura, Esecuzione|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Controller Riesecuzione distribuita|
  \<ToolsDir>\DReplayController\Log\ (directory vuota)|Lettura, Esecuzione, Visualizzazione contenuto cartella|  
||
  \<ToolsDir>\DReplayController\DReplayController.exe|Lettura, Esecuzione, Visualizzazione contenuto cartella|  
||
  \<ToolsDir>\DReplayController\resources\|Lettura, Esecuzione, Visualizzazione contenuto cartella|  
||
  \<ToolsDir>\DReplayController\\{all dlls}|Lettura, Esecuzione, Visualizzazione contenuto cartella|  
||
  \<ToolsDir>\DReplayController\DReplayController.config|Lettura, Esecuzione, Visualizzazione contenuto cartella|  
||
  \<ToolsDir>\DReplayController\IRTemplate.tdf|Lettura, Esecuzione, Visualizzazione contenuto cartella|  
||
  \<ToolsDir>\DReplayController\IRDefinition.xml|Lettura, Esecuzione, Visualizzazione contenuto cartella|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Client di Riesecuzione distribuita|
  \<ToolsDir>\DReplayClient\Log\|Lettura, Esecuzione, Visualizzazione contenuto cartella|  
||
  \<ToolsDir>\DReplayClient\DReplayClient.exe|Lettura, Esecuzione, Visualizzazione contenuto cartella|  
||
  \<ToolsDir>\DReplayClient\resources\|Lettura, Esecuzione, Visualizzazione contenuto cartella|  
||
  \<ToolsDir>\DReplayClient\ (all dlls)|Lettura, Esecuzione, Visualizzazione contenuto cartella|  
||
  \<ToolsDir>\DReplayClient\DReplayClient.config|Lettura, Esecuzione, Visualizzazione contenuto cartella|  
||
  \<ToolsDir>\DReplayClient\IRTemplate.tdf|Lettura, Esecuzione, Visualizzazione contenuto cartella|  
||
  \<ToolsDir>\DReplayClient\IRDefinition.xml|Lettura, Esecuzione, Visualizzazione contenuto cartella|  
  
 <sup>1</sup> Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] servizio Agent è disabilitato nelle istanze [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] e with Advanced Services.  
  
 Se i file di database vengono archiviati in un percorso definito dall'utente, è necessario concedere l'accesso del SID per servizio al percorso in questione. Per altre informazioni sulla concessione di autorizzazioni del file system a un SID per servizio, vedere [Configurare le autorizzazioni del file system per l'accesso al motore di database](configure-file-system-permissions-for-database-engine-access.md).  
  
###  <a name="File_System_Other"></a>Autorizzazioni del file system concesse ad altri account utente o gruppi di Windows  
 Potrebbe essere necessario concedere alcune autorizzazioni relative al controllo dell'accesso ad account predefiniti o ad altri account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Nella tabella seguente sono inclusi gli elenchi di controllo di accesso aggiuntivi impostati dal programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Componente richiedente|Account|Risorsa|Autorizzazioni|  
|--------------------------|-------------|--------------|-----------------|  
|MSSQLServer|Performance Log Users|Instid\MSSQL\binn|Visualizzazione contenuto cartella|  
||Performance Monitor Users|Instid\MSSQL\binn|Visualizzazione contenuto cartella|  
||Performance Log Users, Performance Monitor Users|\WINNT\system32\sqlctr120.dll|Lettura, Esecuzione|  
||Solo Amministratore|\\\\.\root\Microsoft\SqlServer\ServerEvents\\<sql_instance_name><sup>1</sup>|Controllo completo|  
||Administrators, Sistema|\tools\binn\schemas\sqlserver\2004\07\showplan|Controllo completo|  
||Utenti|\tools\binn\schemas\sqlserver\2004\07\showplan|Lettura, Esecuzione|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Account del servizio Windows ReportServer|installare>\Reporting Services\LogFiles * \< *|Elimina<br /><br /> READ_CONTROL<br /><br /> SYNCHRONIZE<br /><br /> FILE_GENERIC_READ<br /><br /> FILE_GENERIC_WRITE<br /><br /> FILE_READ_DATA<br /><br /> FILE_WRITE_DATA<br /><br /> FILE_APPEND_DATA<br /><br /> FILE_READ_EA<br /><br /> FILE_WRITE_EA<br /><br /> FILE_READ_ATTRIBUTES<br /><br /> FILE_WRITE_ATTRIBUTES|  
||Account del servizio Windows ReportServer, Everyone|installare>\Reporting Services\ReportManager, * \<installare>* \Reporting Services\ReportManager\Pages\\\*. * \< * \*\\\* *, \<installare>* \Reporting Services\ReportManager\Styles. \* *, \<installare>* \Reporting Services\ReportManager\ webctrl_client \ 1_0\\*.\*|Lettura, Esecuzione|  
||Account del servizio Windows ReportServer|installare>\Reporting Services\ReportServer * \< *|Lettura|  
||Account del servizio Windows ReportServer|installare>\Reporting Services\ReportServer\global.asax * \< *|Full|  
||Tutti|installare>\Reporting Services\ReportServer\global.asax * \< *|READ_CONTROL<br /><br /> FILE_READ_DATA<br /><br /> FILE_READ_EA<br /><br /> FILE_READ_ATTRIBUTES|  
||Account servizi Windows ReportServer|installare>\Reporting Services\ReportServer\RSReportServer.config * \< *|Elimina<br /><br /> READ_CONTROL<br /><br /> SYNCHRONIZE<br /><br /> FILE_GENERIC_READ<br /><br /> FILE_GENERIC_WRITE<br /><br /> FILE_READ_DATA<br /><br /> FILE_WRITE_DATA<br /><br /> FILE_APPEND_DATA<br /><br /> FILE_READ_EA<br /><br /> FILE_WRITE_EA<br /><br /> FILE_READ_ATTRIBUTES<br /><br /> FILE_WRITE_ATTRIBUTES|  
||Tutti|Chiavi del server di report (hive Instid)|Richiedi valore<br /><br /> Enumera sottochiavi<br /><br /> Notifica<br /><br /> Controllo in lettura|  
||Utente di Servizi terminali|Chiavi del server di report (hive Instid)|Richiedi valore<br /><br /> Imposta valore<br /><br /> Creazione sottochiave<br /><br /> Enumerazione sottochiavi<br /><br /> Notifica<br /><br /> Delete<br /><br /> Controllo in lettura|  
||Power Users|Chiavi del server di report (hive Instid)|Richiedi valore<br /><br /> Imposta valore<br /><br /> Creazione sottochiave<br /><br /> Enumera sottochiavi<br /><br /> Notifica<br /><br /> Delete<br /><br /> Controllo in lettura|  
  
 <sup>1</sup> Si tratta dello spazio dei nomi del provider WMI.  
  
###  <a name="Unusual_Locations"></a>Autorizzazioni del file System correlate a posizioni del disco insolite  
 L'unità predefinita dei percorsi di installazione è **systemdrive**, in genere l'unità C quando vengono installati database tempdb o utente  
  
 **Unità non predefinita**  
  
 In caso di installazione in un'unità locale diversa dall'unità predefinita, il SID per servizio deve disporre dell'accesso al percorso dei file. L'installazione di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] eseguirà il provisioning dell'accesso necessario.  
  
 **Condivisione di rete**  
  
 Quando i database vengono installati in una condivisione di rete, l'account del servizio deve disporre dell'accesso al percorso dei file dei database utente e tempdb. Il provisioning dell'accesso a una condivisione di rete viene effettuato tramite il programma di installazione di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . L'utente deve effettuare il provisioning dell'accesso a un percorso del database tempdb per l'account del servizio prima di eseguire l'installazione. Inoltre deve effettuare il provisioning dell'accesso al percorso del database utente prima della creazione del database.  
  
> [!NOTE]  
>  Gli account virtuali non possono essere autenticati a un percorso remoto. Per tutti gli account virtuali viene usata l'autorizzazione dell'account del computer. Eseguire il provisioning dell'account del computer nel formato _<domain_name>_ **\\** _<computer_name>_ **$**.  
  
###  <a name="Review_additional_considerations"></a>Esame di considerazioni aggiuntive  
 Nella tabella seguente sono indicate le autorizzazioni necessarie per disporre di funzionalità aggiuntive dei servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
|Servizio/Applicazione|Funzionalità|Autorizzazione necessaria|  
|--------------------------|-------------------|-------------------------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]MSSQLSERVER|Scrittura in uno slot di posta elettronica utilizzando xp_sendmail.|Autorizzazioni di scrittura in rete.|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]MSSQLSERVER|Eseguire xp_cmdshell per un utente diverso dall'amministratore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|Funzionamento come parte del sistema operativo e sostituzione di un token a livello di processo.|  
|
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent (MSSQLSERVER)|Uso della funzionalità di riavvio automatico.|È necessario essere membri del gruppo locale Administrators.|  
|Ottimizzazione guidata[!INCLUDE[ssDE](../../includes/ssde-md.md)]|Ottimizza i database per ottenere prestazioni ottimali delle query.|Un utente che dispone di credenziali amministrative deve inizializzare l'applicazione al primo utilizzo. In seguito all'inizializzazione, gli utenti dbo possono utilizzare Ottimizzazione guidata [!INCLUDE[ssDE](../../includes/ssde-md.md)] per ottimizzare solo le tabelle di loro proprietà. Per altre informazioni, vedere l'argomento relativo all'inizializzazione dell'Ottimizzazione guidata [!INCLUDE[ssDE](../../includes/ssde-md.md)] al primo utilizzo nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
  
> [!IMPORTANT]  
>  Prima di aggiornare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], abilitare l'autenticazione di Windows per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e verificare la configurazione predefinita richiesta, ovvero che l'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent sia un membro del gruppo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]sysadmin.  
  
###  <a name="Registry"></a>Autorizzazioni del registro di sistema  
 L'hive del Registro di sistema viene creato in **HKLM\Software\Microsoft\Microsoft SQL Server\\**_<ID_istanza>_ per i componenti specifici dell'istanza. Ad esempio  
  
-   **HKLM\Software\Microsoft\Microsoft SQL Server\MSSQL12.Istanza**  
  
-   **HKLM\Software\Microsoft\Microsoft SQL Server\MSASSQL12.Istanza**  
  
-   **HKLM\Software\Microsoft\Microsoft SQL Server\MSSQL.120**  
  
 Nel Registro di sistema viene inoltre gestito un mapping degli ID istanza ai nomi delle istanze. Il mapping degli ID istanza in base ai nomi delle istanze è gestito nel modo seguente:  
  
-   **[HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\Instance Names\SQL] "NomeIstanza"="MSSQL12"**  
  
-   **[HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\Instance Names\OLAP] "NomeIstanza"="MSASSQL12"**  
  
-   **[HKEY_LOCAL_MACHINE\Software\Microsoft\Microsoft SQL Server\Instance Names\RS] "NomeIstanza"="MSRSSQL12"**  
  
###  <a name="WMI"></a>WMI  
 Tramite Strumentazione gestione Windows (WMI) deve essere possibile eseguire la connessione al [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Per il supporto necessario, viene effettuato il provisioning del SID per servizio del provider WMI di Windows (**NT SERVICE\winmgmt**) nel [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 Per il provider WMI di SQL sono necessarie le autorizzazioni seguenti:  
  
-   Appartenenza ai ruoli predefiniti dei database **db_ddladmin** o **db_owner** nel database msdb.  
  
-   Autorizzazione **CREATE DDL Event Notification** nel server.  
  
-   Autorizzazione **Create Trace Event Notification** nel [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
-   Autorizzazione **View any database** a livello di server.  
  
     L'installazione di[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea uno spazio dei nomi WMI di SQL e concede l'autorizzazione di lettura al SID del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
###  <a name="Pipes"></a>Named pipe  
 In tutte le installazioni, il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornisce l'accesso al [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] tramite il protocollo Shared Memory, una named pipe locale.  
  
##  <a name="Provisioning"></a>Provisioning  
 In questa sezione viene descritto il provisioning degli account nei vari componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   [Provisioning di motore di database](#DE_Prov)  
  
    -   [Entità di Windows](#Win_Principals)  
  
    -   [Account sa](#sa)  
  
    -   [SQL Server e privilegi di accesso SID per servizio](#Logins)  
  
    -   [Accesso SQL Server Agent e privilegi](#Agent)  
  
    -   [Istanza di HADRON e del cluster di failover di SQL e privilegi](#Hadron)  
  
    -   [Writer SQL e privilegi](#Writer)  
  
    -   [WMI di SQL e privilegi](#SQLWMI)  
  
-   [Provisioning di SSAS](#SSAS)  
  
-   [Provisioning di SSRS](#SSRS)  
  
###  <a name="DE_Prov"></a>Provisioning di motore di database  
 Gli account seguenti vengono aggiunti come account di accesso nel [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
####  <a name="Win_Principals"></a>Entità di Windows  
 Durante l'installazione, tramite il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene richiesta la denominazione di almeno un account utente come membro del ruolo predefinito del server **sysadmin** .  
  
####  <a name="sa"></a>Account sa  
 L'account **SA** è sempre presente come account di accesso del [!INCLUDE[ssDE](../../includes/ssde-md.md)] ed è un membro del ruolo predefinito del server **sysadmin** . Quando il [!INCLUDE[ssDE](../../includes/ssde-md.md)] viene installato usando solo l'autenticazione di Windows, ovvero quando l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non è abilitata, l'account di accesso **SA** è presente ma è disabilitato. Per informazioni sull'abilitazione dell'account **sa** , vedere [Modifica della modalità di autenticazione del server](change-server-authentication-mode.md).  
  
####  <a name="Logins"></a>SQL Server e privilegi di accesso SID per servizio  
 Il provisioning del SID per servizio del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene effettuato come account di accesso del [!INCLUDE[ssDE](../../includes/ssde-md.md)] . L'account di accesso del SID per servizio è un membro del ruolo predefinito del server **sysadmin** .  
  
####  <a name="Agent"></a>Accesso SQL Server Agent e privilegi  
 Il provisioning del SID per servizio del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent viene effettuato come account di accesso del [!INCLUDE[ssDE](../../includes/ssde-md.md)] . L'account di accesso del SID per servizio è un membro del ruolo predefinito del server **sysadmin** .  
  
####  <a name="Hadron"></a>[!INCLUDE[ssHADRc](../../includes/sshadrc-md.md)] istanza del cluster di failover di SQL e privilegi  
 Quando si installa il [!INCLUDE[ssDE](../../includes/ssde-md.md)] come istanza di [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] o del cluster di failover di SQL (FCI di SQL), viene effettuato il provisioning di **LOCAL SYSTEM** nel [!INCLUDE[ssDE](../../includes/ssde-md.md)]. All'account di accesso **LOCAL SYSTEM** vengono concesse le autorizzazioni **ALTER ANY AVAILABILITY** (per [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]) e **VIEW SERVER STATE** (per FCI di SQL).  
  
####  <a name="Writer"></a>Writer SQL e privilegi  
 Il provisioning del SID per servizio del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] VSS Writer viene effettuato come account di accesso del [!INCLUDE[ssDE](../../includes/ssde-md.md)] . L'account di accesso del SID per servizio è un membro del ruolo predefinito del server **sysadmin** .  
  
####  <a name="SQLWMI"></a>WMI di SQL e privilegi  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Il programma di installazione effettua il provisioning dell'account **NT SERVICE\winmgmt** come account di [!INCLUDE[ssDE](../../includes/ssde-md.md)] accesso e lo aggiunge al ruolo predefinito del server **sysadmin** .  
  
#### <a name="ssrs-provisioning"></a>Provisioning di SSRS  
 Il provisioning dell'account specificato durante l'installazione viene effettuato come membro del ruolo del database **RSExecRole** . Per altre informazioni, vedere [Configurare l'account del servizio del server di report &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md).  
  
###  <a name="SSAS"></a>Provisioning di SSAS  
 I requisiti dell'account del servizio[!INCLUDE[ssAS](../../includes/ssas-md.md)] variano a seconda della modalità di distribuzione del server. Se si installa [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)], tramite il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verrà richiesto di configurare il servizio [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] da eseguire con un account di dominio. Gli account di dominio sono necessari per supportare la funzionalità dell'account gestito compilato in SharePoint. Per questo motivo, il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non fornisce un account del servizio predefinito, ad esempio un account virtuale, per un'installazione di [!INCLUDE[ssGeminiShort](../../includes/ssgeminishort-md.md)] . Per altre informazioni sul provisioning di PowerPivot per SharePoint, vedere [Configurare gli account del servizio PowerPivot](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts).  
  
 Per tutte le altre installazioni autonome di [!INCLUDE[ssAS](../../includes/ssas-md.md)] , è possibile effettuare il provisioning del servizio da eseguire con un account di dominio, un account di sistema predefinito, un account gestito o un account virtuale. Per altre informazioni sul provisioning degli account, vedere [Configurare gli account del servizio &#40;Analysis Services&#41;](https://docs.microsoft.com/analysis-services/instances/configure-service-accounts-analysis-services).  
  
 Per le installazioni cluster, è necessario specificare un account di dominio o un account di sistema predefinito. Per i cluster di failover di [!INCLUDE[ssAS](../../includes/ssas-md.md)] non sono supportati account gestiti, né account virtuali.  
  
 Per tutte le installazioni di [!INCLUDE[ssAS](../../includes/ssas-md.md)] è necessario specificare un amministratore di sistema dell'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Il provisioning dei privilegi di amministratore viene effettuato nel ruolo **Server** di Analysis Services.  
  
###  <a name="SSRS"></a>Provisioning di SSRS  
 Il provisioning dell'account specificato durante l'installazione viene effettuato nel [!INCLUDE[ssDE](../../includes/ssde-md.md)] come membro del ruolo del database **RSExecRole** . Per altre informazioni, vedere [Configurare l'account del servizio del server di report &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-the-report-server-service-account-ssrs-configuration-manager.md).  
  
##  <a name="Upgrade"></a>Aggiornamento da versioni precedenti  
 In questa sezione sono descritte le modifiche apportate durante l'aggiornamento da una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] richiede [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] R2 SP1, Windows Server 2012, Windows 8.0, Windows Server 2012 R2 o Windows 8.1. Qualsiasi versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in esecuzione in una versione meno recente del sistema operativo deve disporre del sistema operativo aggiornato prima dell'aggiornamento a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Durante l'aggiornamento di [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], la configurazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verrà eseguita dal programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel modo seguente.  
  
    -   Il [!INCLUDE[ssDE](../../includes/ssde-md.md)] viene eseguito con il contesto di sicurezza del SID per servizio. Al SID per servizio è concesso l'accesso alle cartelle file dell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (ad esempio DATA) e alle chiavi del Registro di sistema di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
    -   Il SID per servizio del [!INCLUDE[ssDE](../../includes/ssde-md.md)] viene sottoposto a provisioning in [!INCLUDE[ssDE](../../includes/ssde-md.md)] come membro del ruolo predefinito del server **sysadmin** .  
  
    -   I SID per servizio vengono aggiunti ai gruppi locali di Windows di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], solo se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è un'istanza del cluster di failover.  
  
    -   Le risorse di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] continuano a essere sottoposte a provisioning ai gruppi locali di Windows di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
    -   Il gruppo Windows locale per i servizi viene rinominato da **SQLServer2005MSSQLUser$**_<nome_computer>_**$**_<nome_istanza>_ a **SQLServerMSSQLUser$**_<nome_computer>_**$**_<nome_istanza>_. I percorsi dei file per database migrati disporranno di voci di controllo di accesso per i gruppi locali di Windows. I percorsi dei file di nuovi database disporranno di voci di controllo di accesso per il SID per servizio.  
  
-   Durante l'aggiornamento da [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mantiene le voci di controllo di accesso per il SID per servizio [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
-   Per un'istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , verrà mantenuta la voce di controllo di accesso per l'account di dominio configurato per il servizio.  
  
##  <a name="Appendix"></a>Appendice  
 In questa sezione sono fornite informazioni aggiuntive sui servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   [Descrizione degli account del servizio](#Serv_Accts)  
  
-   [Identificazione di servizi specifici dell'istanza e non compatibili con l'istanza](#Identify_instance_aware_and_unaware)  
  
-   [Nomi dei servizi localizzati](#Localized_service_names)  
  
###  <a name="Serv_Accts"></a>Descrizione degli account del servizio  
 L'account del servizio è l'account usato per avviare un servizio Windows, ad esempio il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
####  <a name="Any_OS"></a>Account disponibili con qualsiasi sistema operativo  
 Oltre ai nuovi account [del servizio gestito](#MSA) e [account virtuali](#VA_Desc) descritti precedentemente, è possibile usare gli account seguenti.  
  
 <a name="Domain_User"></a>**Account utente di dominio**  
  
 Se tramite il servizio si deve interagire con i servizi di rete, accedere a risorse di dominio come condivisioni di file o se sono usate connessioni server collegate ad altri computer che eseguono [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile usare un account di dominio con privilegi minimi. Molte attività tra server possono essere eseguite solo con un account utente di dominio. Questo account deve essere creato in precedenza dall'amministrazione del dominio nell'ambiente.  
  
> [!NOTE]  
>  Se si configura l'applicazione per usare un account di dominio, è possibile isolare i privilegi per l'applicazione, ma è necessario gestire manualmente le password o creare una soluzione personalizzata per tale gestione. In molte applicazioni server viene usata questa strategia per migliorare la sicurezza. Tuttavia, tale strategia richiede attività complesse e amministrazione aggiuntiva. In queste distribuzioni, gli amministratori dei servizi impiegano molto tempo in attività di manutenzione quale la gestione di password del servizio e di nomi dell'entità servizio, necessari per l'autenticazione Kerberos. Inoltre, queste attività di manutenzione possono interrompere il servizio.  
  
 <a name="Local_User"></a>**Account utente locali**  
  
 Se il computer non fa parte di un dominio, è consigliabile usare un account utente locale senza le autorizzazioni di amministratore di Windows.  
  
 <a name="Local_Service"></a>**Account servizio locale**  
  
 L'account Servizio locale è un account predefinito che dispone dello stesso livello di accesso a risorse e oggetti dei membri del gruppo Users. Questo accesso limitato permette di proteggere il sistema nel caso in cui singoli servizi o processi risultino danneggiati. I servizi eseguiti come account Servizio locale possono accedere alle risorse di rete come sessione Null senza credenziali. L'account Servizio locale non è supportato per i servizi [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Servizio locale non è supportato come account che esegue tali servizi, dal momento che si tratta di un servizio condiviso e qualsiasi altro servizio in esecuzione nel servizio locale deve disporre dell'accesso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]come amministratore di sistema. Il nome effettivo dell'account è **NT AUTHORITY\LOCAL SERVICE**.  
  
 <a name="Network_Service"></a>**Account servizio di rete**  
  
 Servizio di rete è un account predefinito che dispone di un livello di accesso più elevato a risorse e oggetti rispetto ai membri del gruppo Users. I servizi eseguiti con l'account servizio di rete accedono alle risorse di rete utilizzando le credenziali dell'account del computer nel formato _<domain_name>_ **\\** _<computer_name>_ **$**. Il nome effettivo dell'account è **NT AUTHORITY\NETWORK SERVICE**.  
  
 <a name="Local_System"></a>**Account sistema locale**  
  
 L'account di sistema locale è un account predefinito con privilegi molto elevati. Dispone di privilegi estesi sul sistema locale e opera come il computer sulla rete. Il nome effettivo dell'account è **NT AUTHORITY\SYSTEM**.  
  
###  <a name="Identify_instance_aware_and_unaware"></a>Identificazione di servizi specifici dell'istanza e non compatibili con l'istanza  
 I servizi specifici dell'istanza sono associati a un'istanza specifica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]e dispongono di hive del Registro di sistema propri. È possibile installare più copie di servizi specifici dell'istanza eseguendo il programma di installazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per ciascun componente o servizio. I servizi non specifici dell'istanza vengono condivisi tra tutte le istanze installate di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Tali servizi non sono associati a un'istanza specifica, vengono installati solo una volta e non possono essere installati in modalità side-by-side.  
  
 Tra i servizi specifici dell'istanza disponibili in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono inclusi i seguenti:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Agente  
  
     Il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent è disabilitato nelle istanze di [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] e [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] with Advanced Services.  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]<sup>1</sup>  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   Ricerca full-text  
  
 Tra i servizi non specifici dell'istanza disponibili in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono inclusi i seguenti:  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Browser  
  
-   Writer SQL  
  
 <sup>1</sup> Analysis Services in modalità integrata SharePoint viene eseguito come ' PowerPivot ' come una singola istanza denominata. Il nome dell'istanza è fisso. Non è possibile specificare un nome diverso. È possibile installare una sola istanza di Analysis Services in esecuzione come 'PowerPivot' in ciascun server fisico.  
  
###  <a name="Localized_service_names"></a>Nomi dei servizi localizzati  
 Nella tabella seguente sono illustrati i nomi dei servizi visualizzati dalle versioni localizzate di Windows.  
  
|Linguaggio|Nome del servizio locale|Nome del servizio di rete|Nome del sistema locale|Nome del gruppo amministrativo|  
|--------------|----------------------------|------------------------------|---------------------------|--------------------------|  
|Inglese<br /><br /> Cinese semplificato<br /><br /> Cinese tradizionale<br /><br /> Coreano<br /><br /> Giapponese|NT AUTHORITY\LOCAL SERVICE|NT AUTHORITY\NETWORK SERVICE|NT AUTHORITY\SYSTEM|BUILTIN\Administrators|  
|Tedesco|NT-AUTORITÄT\LOKALER DIENST|NT-AUTORITÄT\NETZWERKDIENST|NT-AUTORITÄT\SYSTEM|VORDEFINIERT\Administratoren|  
|Francese|AUTORITE NT\SERVICE LOCAL|AUTORITE NT\SERVICE RÉSEAU|AUTORITE NT\SYSTEM|BUILTIN\Administrators|  
|Italiano|NT AUTHORITY\SERVIZIO LOCALE|NT AUTHORITY\SERVIZIO DI RETE|NT AUTHORITY\SYSTEM|BUILTIN\Administrators|  
|Spagnolo|NT AUTHORITY\SERVICIO LOC|NT AUTHORITY\SERVICIO DE RED|NT AUTHORITY\SYSTEM|BUILTIN\Administradores|  
|Russo|NT AUTHORITY\LOCAL SERVICE|NT AUTHORITY\NETWORK SERVICE|NT AUTHORITY\SYSTEM|BUILTIN\Администраторы|  
  
## <a name="related-content"></a>Contenuto correlato  
 [Considerazioni sulla sicurezza per un'installazione di SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
 [Percorsi dei file per le istanze predefinite e denominate di SQL Server](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)  
  
 [Installazione di Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
