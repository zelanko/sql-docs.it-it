---
title: Specificare le credenziali e le informazioni sulla connessione per le origini dati del report | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- no credentials option [Reporting Services]
- impersonation [Reporting Services]
- user impersonation [Reporting Services]
- Windows authentication [Reporting Services]
- data sources [Reporting Services], security
- connection strings [Reporting Services]
- unattended report processing [Reporting Services]
- reports [Reporting Services], security
- remote data sources [Reporting Services]
- credentials [Reporting Services]
- authentication [Reporting Services]
- external data sources [Reporting Services]
- prompted credentials [Reporting Services]
- multiple connections
- stored credentials [Reporting Services]
- security [Reporting Services], data sources
- Windows integrated security [Reporting Services]
ms.assetid: fee1a663-a313-424a-aed2-5082bfd114b3
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 2d1e804282459972b21303cf795a9c3a88ea93d5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66107043"
---
# <a name="specify-credential-and-connection-information-for-report-data-sources"></a>Specificare le credenziali e le informazioni sulla connessione per le origini dati del report
  Un server di report utilizza credenziali per connettersi a origini dei dati esterne che forniscono contenuto ai report o informazioni sui destinatari alle sottoscrizioni guidate dai dati. È possibile specificare credenziali che utilizzano l'autenticazione di Windows, l'autenticazione del database, l'autenticazione personalizzata o che non utilizzano alcuna autenticazione. Quando si invia una richiesta di connessione in rete, il server di report rappresenterà un account utente o l'account di esecuzione automatica. Per altre informazioni sul contesto di protezione in cui viene eseguita una richiesta di connessione, vedere [Configurazione dell'origine dei dati e connessioni di rete](#DataSourceConfigurationConnections) più avanti in questo argomento.  
  
> [!NOTE]  
>  Le credenziali vengono inoltre utilizzate per autenticare gli utenti che accedono a un server di report. Le informazioni relative all'autenticazione di utenti per l'accesso a un server di report sono disponibili in un altro argomento.  
  
 La connessione a un'origine dei dati esterna viene definita quando si crea il report. Può essere gestita separatamente dopo la pubblicazione del report. È possibile specificare una stringa di connessione statica oppure un'espressione che consente agli utenti di selezionare un'origine dei dati da un elenco dinamico. Per ulteriori informazioni su come specificare un tipo di origine dati e una stringa di connessione, vedere [connessioni dati, origini dati e stringhe di connessione in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md).  
  
## <a name="using-remote-data-sources"></a>Utilizzo di origini dati remote  
 Se il report recupera dati da un server di database remoto, verificare gli elementi seguenti:  
  
-   Le credenziali fornite al server di database devono essere valide. Se si utilizzano le credenziali utente di Windows, verificare che l'utente disponga delle autorizzazioni per il server e il database.  
  
-   Le porte utilizzate dal server di database devono essere aperte. Se si accede ai database relazionali di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in computer esterni o se il database del server di report si trova in un'istanza esterna di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è necessario aprire le porte 1433 e 1434 nel computer esterno. Assicurarsi di riavviare il server dopo avere aperto porte. Per altre informazioni, vedere [Configurazione di Windows Firewall per l'accesso al Motore di database](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md).  
  
-   Le connessioni remote devono essere attivate. Se si accede ai database relazionali SQL Server in computer esterni, per verificare che le connessioni remote su TCP siano abilitate è possibile utilizzare lo strumento Gestione configurazione SQL Server.  
  
## <a name="ways-to-specify-credentials-for-connecting-to-remote-data-sources"></a>Modalità per specificare le credenziali per la connessione a origini dati remote  
 Le origini dei dati che forniscono contenuto ai report si trovano in genere in server remoti. Per recuperare dati per un report, un server di report deve connettersi al server tramite un set di credenziali fornite in anticipo o ottenute in fase di esecuzione. Quando si configura un'origine dei dati, è possibile specificare le credenziali nei modi seguenti:  
  
-   Richiedere all'utente le credenziali.  
  
-   Archiviare le credenziali.  
  
-   Utilizzare la sicurezza integrata di Windows.  
  
-   Utilizzare l'impostazione Nessuna credenziale.  
  
 I tipi di connessione supportati variano in base al tipo di ambiente di rete. Se, ad esempio, è abilitato il protocollo Kerberos versione 5 è possibile utilizzare le caratteristiche di delega e rappresentazione disponibili con l'autenticazione di Windows per supportare connessioni tra più server. Se la rete non supporta queste caratteristiche di sicurezza, sarà necessario utilizzare soluzioni che tengano in considerazione i vincoli di connessione. Se delega e rappresentazione non sono attivate, le credenziali di Windows possono essere inviate attraverso una connessione del computer prima che scadano. La connessione utente da un computer client a un computer del server di report viene considerata la prima connessione. Se l'utente apre un report che recupera dati da un server remoto, il tentativo di accesso viene considerato una seconda connessione e ha esito negativo se è stata specificata la sicurezza integrata quando la delega non è attivata.  
  
 Se sono richieste più connessioni per completare un round trip dal computer client a un'origine dei dati del report esterna, scegliere tra le strategie seguenti per consentire le connessioni.  
  
-   Attivare le caratteristiche di rappresentazione e di delega nel dominio in modo che le credenziali possono essere delegate ad altri computer senza alcuna limitazione.  
  
-   Utilizzare credenziali archiviate o credenziali fornite dall'utente per l'esecuzione di query nelle origini dei dati esterne. Le credenziali possono essere un account di dominio di Windows o un account di accesso al database.  
  
### <a name="prompted-credentials"></a>Credenziali fornite dall'utente  
 Quando si configura una connessione dell'origine dati del report per utilizzare le credenziali su richiesta, ogni utente che accede al report deve immettere un nome utente e una password per recuperare i dati. Questo approccio è consigliato per i report contenenti dati riservati. Le credenziali su richiesta possono essere utilizzate solo su report eseguiti su richiesta. Le credenziali fornite dall'utente possono essere un account di dominio di Windows o un account di accesso al database. Per usare l'autenticazione di Windows, è necessario selezionare **Usa come credenziali di Windows per la connessione all'origine dei dati**. In caso contrario, il server di report passa le credenziali al server di database per l'autenticazione utente. Se il server di database non è in grado di autenticare le credenziali fornite dall'utente, la connessione non verrà stabilita.  
  
### <a name="windows-integrated-security"></a>Sicurezza integrata di Windows  
 Quando si usa l'opzione **Sicurezza integrata di Windows** , il server di report passa il token di sicurezza dell'utente che accede al report al server che ospita l'origine dati esterna. In questo caso, all'utente non viene richiesto di digitare un nome utente o una password. Questo approccio è consigliato se le caratteristiche di rappresentazione e delega sono attivate. In caso contrario, è consigliabile utilizzare questo approccio solo se tutti i server cui si desidera accedere si trovano nello stesso computer.  
  
### <a name="stored-credentials"></a>Credenziali archiviate  
 È possibile archiviare le credenziali utilizzate per accedere a un'origine dei dati esterna. Le credenziali vengono archiviate con la crittografia reversibile nel database del server di report. È possibile specificare un solo set di credenziali archiviate per ogni origine dei dati utilizzata in un report. Le credenziali specificate recuperano gli stessi dati per i diversi utenti che eseguono il report.  
  
 L'utilizzo di credenziali archiviate è consigliabile come parte di una strategia per l'accesso a server di database remoti. Le credenziali archiviate sono necessarie se si desidera supportare le sottoscrizioni oppure impostare una pianificazione per la generazione della cronologia dei report o per gli aggiornamenti degli snapshot dei report. Un report eseguito come processo in background viene eseguito automaticamente dal server di report. Poiché non è impostato alcun contesto utente, per connettersi a un'origine dei dati il server di report deve recuperare le informazioni sulle credenziali dal database del server di report.  
  
 La password e il nome utente specificati possono essere credenziali di Windows o un account di accesso al database. Se si specificano le credenziali di Windows, il server di report le passa a Windows per l'autenticazione successiva. In caso contrario, le credenziali vengono passate al server di database per l'autenticazione.  
  
#### <a name="how-to-grant-allow-log-on-locally-permissions-to-domain-user-accounts"></a>Modalità di concessione delle autorizzazioni "Consenti accesso locale" agli account utente di dominio  
 Se si utilizzano credenziali archiviate per connettersi a un'origine dati esterna, l'account utente di dominio di Windows deve disporre dell'autorizzazione per l'accesso locale. Questa autorizzazione consente al server di report di rappresentare l'utente sul server di report stesso e di inviare la richiesta all'origine dati esterna in qualità dell'utente rappresentato.  
  
 Per concedere questa autorizzazione, effettuare le operazioni seguenti:  
  
1.  Nel computer del server di report, in **Strumenti di amministrazione**aprire **Criteri di sicurezza locali**.  
  
2.  In **Impostazioni sicurezza**espandere **Criteri locali**, quindi fare clic su **Assegnazione diritti utente**.  
  
3.  Nel riquadro dei dettagli fare clic con il pulsante destro del mouse su **Consenti accesso locale** e quindi scegliere **Proprietà**.  
  
4.  Fare clic su **Aggiungi utente o gruppo**.  
  
5.  Fare clic su **Percorsi**, specificare un dominio o un altro percorso in cui eseguire la ricerca e quindi scegliere **OK**.  
  
6.  Immettere l'account di Windows per il quale si desidera consentire l'accesso interattivo e quindi scegliere **OK**.  
  
7.  Nella finestra di dialogo **Allow log on locally Properties** (Proprietà - Consenti accesso locale) fare clic su **OK**.  
  
8.  Verificare che all'account selezionato non siano assegnate anche autorizzazioni di negazione:  
  
    1.  Fare clic con il pulsante destro del mouse su **Nega accesso locale** e quindi scegliere **Proprietà**.  
  
    2.  Se l'account è incluso nell'elenco, selezionarlo e quindi fare clic su **Rimuovi**.  
  
#### <a name="using-impersonation-with-stored-credentials"></a>Utilizzo della rappresentazione con le credenziali archiviate  
 È inoltre possibile utilizzare le credenziali per rappresentare l'identità di un altro utente. Per i database di SQL Server, l'uso delle opzioni di rappresentazione comporta l'impostazione della funzione [SETUSER](/sql/t-sql/statements/setuser-transact-sql) .  
  
> [!IMPORTANT]  
>  Non utilizzare la rappresentazione per i report che supportano le sottoscrizioni o che utilizzano pianificazioni per generare la cronologia dei report o aggiornare gli snapshot dell'esecuzione dei report.  
  
### <a name="no-credentials"></a>Connessioni senza credenziali  
 È possibile configurare una connessione a un'origine dei dati in modo che non utilizzi alcuna credenziale. È consigliabile utilizzare sempre le credenziali per accedere alle origini dei dati. Si potrebbe tuttavia scegliere di eseguire un report senza credenziali nei casi seguenti:  
  
-   Per l'origine dei dati remota non sono necessarie credenziali.  
  
-   Le credenziali vengono passate nella stringa di connessione (opzione consigliata solo per connessioni protette).  
  
-   Il report è un sottoreport che utilizza le credenziali del report padre.  
  
 In queste situazioni il server di report si connette a un'origine dei dati remota tramite l'account di esecuzione automatica che è necessario definire a priori. Poiché il server di report non si connette a un server remoto tramite le relative credenziali del servizio, è necessario specificare un account che il server di report può utilizzare per eseguire la connessione. Per altre informazioni sulla creazione di questo account, vedere [Configurare l'account di esecuzione automatica &#40;Gestione configurazione SSRS&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md).  
  
##  <a name="data-source-configuration-and-network-connections"></a><a name="DataSourceConfigurationConnections"></a> Configurazione dell'origine dei dati e connessioni di rete  
 Nella tabella seguente viene illustrato come vengono eseguite le connessioni per combinazioni specifiche di tipi di credenziali ed estensioni per l'elaborazione dati. Se si usa un'estensione per l'elaborazione dati personalizzata, vedere [Specificare le connessioni per le estensioni per l'elaborazione dati personalizzate](specify-connections-for-custom-data-processing-extensions.md).  
  
|**Type**|**Contesto per la connessione di rete**|**Tipi di origine dei dati**<br /><br /> **(SQL Server, Oracle, ODBC, OLE DB, Analysis Services, XML, SAP NetWeaver BI, Hyperion Essbase)**|  
|--------------|----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------|  
|sicurezza integrata|Rappresenta l'utente corrente|Per tutti i tipi di origine dei dati, la connessione viene eseguita tramite l'account utente corrente.|  
|Credenziali di Windows|Rappresenta l'utente specificato|Per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle, ODBC e OLE DB la connessione viene eseguita tramite l'account utente rappresentato.|  
|Credenziali di database|Rappresenta l'account di esecuzione automatica o l'account del servizio.<br /><br /> (Reporting Services rimuove le autorizzazioni di amministratore quando la richiesta di connessione viene inviata tramite l'identità del servizio).|Per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle, ODBC e OLE DB:<br /><br /> Il nome utente e la password vengono accodati alla stringa di connessione.<br /><br /> Per [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]:<br /><br /> La connessione ha esito positivo se viene utilizzato il protocollo TCP/IP, in caso contrario ha esito negativo.<br /><br /> Per XML:<br /><br /> La connessione sul server di report ha esito negativo se vengono utilizzate le credenziali del database.|  
|nessuno|Rappresenta l'account di esecuzione automatica.|Per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Oracle, ODBC e OLE DB:<br /><br /> Vengono utilizzate le credenziali definite nella stringa di connessione. La connessione ha esito negativo sul server di report se l'account di esecuzione automatica non è definito.<br /><br /> Per [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]:<br /><br /> La connessione ha sempre esito negativo se non vengono specificate credenziali, anche se l'account di esecuzione automatica è stato definito.<br /><br /> Per XML:<br /><br /> La connessione viene eseguita come utente anonimo se l'account di esecuzione automatica è definito; in caso contrario, la connessione ha esito negativo.|  
  
## <a name="setting-credentials-programmatically"></a>Impostazione di credenziali a livello di programmazione  
 È possibile impostare le credenziali tramite codice per controllare l'accesso ai report e al server di report. Per altre informazioni, vedere [Origini dati e metodi di connessione](../report-server-web-service/methods/data-sources-and-connection-methods.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Origini dati supportate da Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md)   
 [Connessioni dati, origini dati e stringhe di connessione in Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md)   
 [Gestione delle origini dati del report](../../integration-services/connection-manager/data-sources.md)   
 [Gestione report &#40;modalità nativa SSRS&#41;](../report-manager-ssrs-native-mode.md)   
 [Creare, eliminare o modificare un'origine dati condivisa &#40;Gestione report&#41;](../create-delete-or-modify-a-shared-data-source-report-manager.md)   
 [Configurare le proprietà delle origini dati per un report &#40;Gestione report&#41;](configure-data-source-properties-for-a-report-report-manager.md)  
  
  
