---
title: Configurare IIS per la sincronizzazione Web | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- IIS server configuration [SQL Server replication]
- websync.log
- Web synchronization, IIS servers
ms.assetid: d651186e-c9ca-4864-a444-2cd6943b8e35
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: ece2cb8575ae7cf4d20f4e27b848970ade4a27ca
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67903197"
---
# <a name="configure-iis-for-web-synchronization"></a>Configurazione di IIS per la sincronizzazione Web
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Le procedure descritte in questo argomento rappresentano il secondo passaggio nella configurazione della sincronizzazione Web per la replica di tipo merge. Questo passaggio è successivo all'abilitazione di una pubblicazione per la sincronizzazione Web. Per una panoramica del processo di configurazione, vedere [Configura sincronizzazione Web](../../relational-databases/replication/configure-web-synchronization.md). Al termine delle procedure indicate in questo argomento, procedere al terzo passaggio, che consiste nella configurazione di una sottoscrizione per l'utilizzo della sincronizzazione Web. Questo terzo passaggio è descritto negli argomenti seguenti:  
  
-   [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]: [Procedura: Configurare una sottoscrizione per l'usare la sincronizzazione Web \(SQL Server Management Studio\)](https://msdn.microsoft.com/library/ms345214.aspx)  
  
-   Programmazione [!INCLUDE[tsql](../../includes/tsql-md.md)] della replica: [Procedura: Configurare una sottoscrizione per l'usare la sincronizzazione Web (Programmazione Transact-SQL della replica)](https://msdn.microsoft.com/library/ms345206.aspx)  
  
-   RMO: [Procedura: Configurare una sottoscrizione per l'usare la sincronizzazione Web (Programmazione RMO)](https://msdn.microsoft.com/library/ms345207.aspx)  
  
 Nella sincronizzazione Web viene utilizzato un computer che esegue [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS) per sincronizzare le sottoscrizioni pull con le pubblicazioni di tipo merge. Sono supportate le versioni 5.0, 6.0 e 7.0 di IIS. La Configurazione guidata sincronizzazione Web non è supportata in IIS versione 7.0.  
  
> [!IMPORTANT]  
>  Verificare che nell'applicazione venga utilizzato solo [!INCLUDE[dnprdnlong](../../includes/dnprdnlong-md.md)] o versione successiva e che le versioni precedenti di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] non siano installate sul server IIS. Le versioni precedenti di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] possono causare errori tra cui: "Formato di messaggio non valido durante la sincronizzazione Web. Verificare che i componenti di replica siano configurati correttamente nel server Web".  
  
> [!CAUTION]  
>  Non utilizzare contemporaneamente sia WebSync sia percorsi alternativi della cartella snapshot.  
  
 Per utilizzare la sincronizzazione Web, è necessario configurare IIS eseguendo la procedura seguente. Ogni passaggio è descritto in dettaglio in questo argomento.  
  
1.  Configurare SSL (Secure Sockets Layer). L'utilizzo di SSL è obbligatorio per la comunicazione tra IIS e tutti i Sottoscrittori.  
  
2.  Installare i componenti di connettività di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel computer che esegue IIS tramite l'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Installare i componenti di connettività diation Wizard. Se si intende utilizzare la procedura di configurazione guidata della sincronizzazione Web citata nel passaggio 3, è necessario installare anche [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] nel computer che esegue IIS.  
  
3.  Configurare il computer che esegue IIS per la sincronizzazione Web. È possibile configurare manualmente il computer oppure utilizzare la procedura di configurazione guidata della sincronizzazione Web. È consigliabile utilizzare la procedura guidata.  
  
    > [!NOTE]  
    >  Se nel computer con IIS viene eseguita una versione a 64 bit di Windows, è necessario eseguire il comando seguente per garantire la corretta configurazione del server per le applicazioni ISAPI. Per ulteriori informazioni, vedere la documentazione di IIS.  
  
    ```  
    cscript %SystemDrive%\inetpub\AdminScripts\adsutil.vbs set w3svc/AppPools/Enable32bitAppOnWin64 1  
    ```  
  
4.  Impostare le autorizzazioni appropriate per Listener per la replica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
5.  Eseguire la sincronizzazione Web in modalità diagnostica per testare la connessione al computer che esegue IIS e verificare la corretta installazione del certificato SSL (Secure Sockets Layer).  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="configuring-secure-sockets-layer"></a>Configurazione di SSL (Secure Sockets Layer)  
 Per configurare SSL, specificare un certificato che il computer che esegue IIS deve utilizzare. La sincronizzazione Web per la replica di tipo merge supporta l'utilizzo di certificati server ma non di certificati client. Per configurare IIS per la distribuzione, è innanzitutto necessario ottenere un certificato da un'autorità di certificazione. Un'autorità di certificazione è un'entità responsabile di determinare e garantire l'autenticità delle chiavi di crittografia pubbliche appartenenti a utenti, computer o altre autorità di certificazione. Per ulteriori informazioni sui certificati, vedere la documentazione di IIS. Dopo l'installazione del certificato, è necessario associare il certificato al sito Web utilizzato nella sincronizzazione Web.  
  
#### <a name="to-specify-a-certificate-for-deployment"></a>Per specificare un certificato per la distribuzione  
  
1.  Accedere come amministratore al computer che esegue IIS.  
  
2.  Avviare **Gestione Internet Information Services (IIS)** :  
  
    1.  Fare clic sul pulsante **Start**e quindi scegliere **Esegui**.  
  
    2.  Digitare **inetmgr** nella casella **Apri**e quindi fare clic su **OK**.  
  
3.  Eseguire la Gestione guidata certificati IIS:  
  
    1.  In **Gestione Internet Information Services (IIS)** espandere il nodo **computer locale** e quindi la cartella **Siti Web** .  
  
    2.  Fare clic con il pulsante destro del mouse su **Sito Web predefinito**e quindi scegliere **Proprietà**.  
  
    3.  Nella scheda **Sicurezza directory** della finestra di dialogo **Proprietà - Sito Web predefinito** fare clic su **Certificato server**.  
  
    4.  Completare la Gestione guidata certificati server Web.  
  
4.  Fare clic su **OK**.  
  
 Se non è possibile ottenere un certificato server da un'autorità di certificazione, è possibile specificare un certificato per l'esecuzione di test. Per configurare IIS 6.0 per l'esecuzione di test, installare un certificato mediante l'utilità SelfSSL disponibile nel Resource Kit di IIS 6.0. È possibile scaricare gli strumenti dall' [Area download Microsoft](https://go.microsoft.com/fwlink/?LinkId=30958). Per IIS 5.0, visitare il sito [Supporto Tecnico Microsoft](https://go.microsoft.com/fwlink/?LinkId=46229).  
  
> [!NOTE]  
>  Affinché un sito Web possa utilizzare SSL, è necessario che a tale sito sia associato un certificato. SelfSSL associa automaticamente il certificato al sito Web predefinito. Se si dispone già di un certificato oppure si installa successivamente un certificato di un'autorità di certificazione, è necessario associare tale certificato in modo esplicito al sito Web utilizzato nella sincronizzazione Web. Assicurarsi che al sito Web utilizzato per la sincronizzazione delle sottoscrizioni sia associato un solo certificato. Se sono associati più certificati, il Sottoscrittore utilizzerà il primo sito Web disponibile.  
  
#### <a name="to-specify-a-certificate-for-testing-in-iis-60"></a>Per specificare un certificato per l'esecuzione di test in IIS 6.0  
  
1.  Accedere come amministratore al computer che esegue IIS.  
  
2.  Scaricare e installare SelfSSL. Per impostazione predefinita, l'applicazione viene installata in \<*unità*>:\Programmi\IIS Resources\SelfSSL. I collegamenti all'applicazione e alla documentazione vengono copiati in \<*unità*>:\Documents and Settings\All Users\Menu Start\Programmi\IIS Resources\SelfSSL.  
  
3.  Eseguire SelfSSL:  
  
    -   Per eseguire SelfSSL con i valori predefiniti per tutti i parametri, individuare la directory di installazione dell'applicazione e fare doppio clic su SelfSSL.exe.  
  
        > [!NOTE]  
        >  Per impostazione predefinita, il certificato installato da SelfSSL ha una validità di sette giorni.  
  
    -   Per specificare valori per uno o più parametri, fare clic sul menu **Start**e quindi scegliere **Esegui**. Immettere **cmd** nella casella **Apri**e quindi fare clic su **OK**. Individuare la directory di installazione di SelfSSL, digitare `SelfSSL`e quindi specificare i valori per uno o più parametri. Per un elenco di parametri, digitare `SelfSSL -?`.  
  
## <a name="installing-connectivity-components-and-sql-server-management-studio"></a>Installazione di componenti di connettività e SQL Server Management Studio  
  
#### <a name="to-install-sql-server-connectivity-components-and-sql-server-management-studio"></a>Per installare i componenti di connettività di SQL Server e SQL Server Management Studio  
  
1.  Accedere come amministratore al computer che esegue IIS.  
  
2.  Dal disco di installazione di [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] avviare l'Installazione guidata di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per altre informazioni sull'uso di questa procedura guidata, vedere [Installare SQL Server 2016 dall'Installazione guidata &#40;programma di installazione&#41;](../../database-engine/install-windows/install-sql-server-from-the-installation-wizard-setup.md).  
  
3.  Nella pagina **Selezione funzionalità** selezionare **Connettività strumenti client**.  
  
4.  Se si intende utilizzare la Configurazione guidata sincronizzazione Web, selezionare **Strumenti di gestione - Di base**.  
  
5.  Completare la procedura guidata e quindi riavviare il computer.  
  
    > [!NOTE]  
    >  È possibile installare componenti aggiuntivi, ma per la sincronizzazione Web sono necessari soltanto i componenti di connettività.  
  
## <a name="configuring-the-computer-that-is-running-iis-by-using-the-configure-web-synchronization-wizard"></a>Configurazione del computer che esegue IIS utilizzando la procedura di configurazione guidata della sincronizzazione Web  
 Configurare il server IIS mediante la procedura di configurazione guidata della sincronizzazione Web o manualmente. Sebbene sia consigliabile utilizzare la procedura guidata, nella prossima sezione verranno illustrati i passaggi necessari per la configurazione manuale. La Configurazione guidata sincronizzazione Web, disponibile in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] , può essere utilizzata solo per le pubblicazioni create in un server di pubblicazione che esegue [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]o è stato aggiornato a [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Non può essere utilizzata per le pubblicazioni in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Può essere utilizzata con le sottoscrizioni in [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive e [!INCLUDE[ssEWnoversion](../../includes/ssewnoversion-md.md)] 3.0 e versioni successive.  
  
 La configurazione presenta le funzionalità seguenti:  
  
-   Utilizza il sito Web predefinito in IIS. È comunque possibile utilizzare un altro sito Web. Per ulteriori informazioni sulla creazione di siti Web, vedere la documentazione di IIS.  
  
    > [!NOTE]  
    >  Il sito Web specificato garantisce l'accesso ai componenti utilizzati nella sincronizzazione Web e consente l'accesso ad altri dati o ad altre pagine Web solo se configurato a tale scopo.  
  
-   Crea una directory virtuale e gli alias associati. L'alias viene utilizzato per l'accesso ai componenti della sincronizzazione Web. Ad esempio, se l'indirizzo IIS è `https://server.domain.com` e si specifica l'alias 'websync1', l'indirizzo per l'accesso al componente replisapi.dll sarà `https://server.domain.com/websync1/replisapi.dll`.  
  
-   Utilizza l'autenticazione di base. È consigliabile utilizzare l'autenticazione di base poiché consente di eseguire IIS e il server di pubblicazione/distribuzione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in computer separati (configurazione consigliata) senza la delega Kerberos. L'utilizzo di SSL con l'autenticazione di base assicura la crittografia degli account di accesso, delle password e di tutti i dati in transito. SSL è necessario indipendentemente dal tipo di autenticazione utilizzato. Per altre informazioni sulle procedure consigliate per la sincronizzazione Web, vedere la sezione "Procedure consigliate per la sicurezza nella sincronizzazione Web" in [Configurare la sincronizzazione Web](../../relational-databases/replication/configure-web-synchronization.md).  
  
#### <a name="to-configure-the-computer-that-is-running-iis-by-using-the-configure-web-synchronization-wizard"></a>Per configurare il computer che esegue IIS utilizzando la procedura di configurazione guidata della sincronizzazione Web  
  
1.  Nel computer che esegue IIS avviare [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
2.  Connettersi al server di pubblicazione e quindi espandere il nodo del server.  
  
3.  Espandere la cartella **Pubblicazioni locali** , fare clic con il pulsante destro del mouse sulla pubblicazione e quindi scegliere **Configura sincronizzazione Web**.  
  
4.  Nella pagina **Tipo di Sottoscrittore** della Configurazione guidata sincronizzazione Web selezionare **SQL Server**.  
  
5.  Nella pagina **Web Server** :  
  
    1.  Selezionare l'istanza di IIS che eseguirà la sincronizzazione delle sottoscrizioni.  
  
    2.  Selezionare **Crea una nuova directory virtuale**.  
  
    3.  Nel riquadro inferiore della pagina espandere l'istanza di IIS, quindi **Siti Web**e infine fare clic su **Sito Web predefinito**.  
  
6.  Nella pagina **Informazioni directory virtuale** :  
  
    1.  Nella casella **Alias** immettere un alias per la directory virtuale.  
  
    2.  Nella casella **Percorso** immettere un percorso per la directory virtuale. Ad esempio, se è stato immesso **websync1** nella casella **Alias** , immettere **C:\Inetpub\wwwroot\websync1** nella casella **Percorso** . Fare clic su **Avanti**.  
  
    3.  In entrambe le finestre di dialogo fare clic su **Sì**. In questo modo viene specificato che si intende creare una nuova cartella e copiare la DLL ISAPI (Internet Server API) di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . .  
  
7.  Nella pagina **Accesso autenticato** :  
  
    1.  Assicurarsi che le opzioni **Autenticazione integrata di Windows** e **Autenticazione del digest per server di dominio Windows** siano deselezionate.  
  
    2.  Selezionare **Autenticazione di base**.  
  
    3.  Nelle caselle **Dominio predefinito** e **Area autenticazione** immettere il dominio del computer che esegue IIS.  
  
8.  Nella pagina **Accesso alla directory** :  
  
    1.  Fare clic su **Aggiungi**e quindi nella finestra di dialogo **Seleziona Utenti o gruppi** aggiungere gli account che verranno utilizzati dai Sottoscrittori per le connessioni al server IIS. Si tratta degli account che verranno specificati nella pagina **Informazioni server Web** della Creazione guidata nuova sottoscrizione oppure come valore per il parametro [sp_addmergepullsubscription_agent](../../relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql.md) *@internet_login* .  
  
9. Nella pagina **Accesso alla condivisione snapshot** immettere la condivisione snapshot. In questa condivisione vengono impostate le autorizzazioni appropriate affinché i Sottoscrittori possano accedere ai file di snapshot. Per altre informazioni sulle autorizzazioni per la condivisione, vedere [Proteggere la cartella snapshot](../../relational-databases/replication/security/secure-the-snapshot-folder.md).  
  
10. Nella pagina **Completamento procedura guidata** fare clic su **Fine**.  
  
     In caso di errore, ad esempio un errore di rete durante il tentativo di configurazione di un computer remoto che esegue IIS, verrà eseguito il rollback di tutte le azioni completate e tutte le restanti azioni verranno annullate. Se non può essere eseguito il rollback di un'azione completata, nella pagina finale della procedura guidata verrà segnalato l' **esito positivo** e verrà mantenuto il commit delle azioni completate.  
  
11. Se nel computer con IIS è in esecuzione una versione a 64 bit di Windows, è necessario copiare replisapi.dll nella directory appropriata:  
  
    1.  Fare clic sul pulsante **Start**e quindi scegliere **Esegui**. Immettere **iisreset** nella casella **Apri**e quindi fare clic su **OK**.  
  
    2.  Dopo l'arresto e il riavvio di IIS, copiare il file replisapi.dll da [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]COM\replisapi nella directory specificata nel passaggio 6b.  
  
    3.  Fare clic sul pulsante **Start**e quindi scegliere **Esegui**. Immettere **cmd** nella casella **Apri**e quindi fare clic su **OK**.  
  
    4.  Nella directory specificata al passaggio 6b eseguire il comando seguente:  
  
         **regsvr32 replisapi.dll**  
  
## <a name="manually-configuring-the-computer-that-is-running-iis"></a>Configurazione manuale del computer che esegue IIS  
 Per configurare manualmente il computer che esegue IIS, è necessario installare e configurare Listener per la replica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e quindi configurare l'autorizzazione per i Sottoscrittori che si connetteranno a IIS.  
  
#### <a name="to-install-and-configure-the-sql-server-replication-listener"></a>Per installare e configurare Listener per la replica di SQL Server  
  
1.  Creare una directory di file nel computer che esegue IIS per contenere replisapi.dll. Sebbene sia possibile creare la directory in un percorso qualsiasi, è consigliabile crearla nella directory \<*unità*>:\Inetpub. Ad esempio, creare la directory \<*unità*>:\Inetpub\SQLReplication\\.  
  
    > [!IMPORTANT]  
    >  È consigliabile creare questa directory in una partizione del file system NTFS anziché in un file system FAT. Quando si utilizza il file system NTFS, è possibile utilizzare le autorizzazioni di tale file system per controllare esattamente gli utenti che possono accedere alla replica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  Copiare replisapi.dll dalla directory [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]com\ alla directory di file creata nel passaggio 1.  
  
3.  Registrare replisapi.dll:  
  
    1.  Fare clic sul pulsante **Start**e quindi scegliere **Esegui**. Immettere **cmd** nella casella **Apri**e quindi fare clic su **OK**.  
  
    2.  Nella directory creata al passaggio 1 eseguire il comando seguente:  
  
         **regsvr32 replisapi.dll**  
  
4.  Creare un nuovo sito Web per la replica oppure utilizzare un sito esistente. I componenti di replica accederanno al sito Web durante la sincronizzazione. Per ulteriori informazioni sulla creazione di siti Web, vedere la documentazione di IIS.  
  
5.  Creare una directory virtuale in IIS. È consigliabile creare la directory virtuale nel sito Web creato nel passaggio 4 ed eseguirne il mapping alla directory creata nel passaggio 1. Per ulteriori informazioni sulla creazione di directory virtuali, vedere la documentazione di IIS. È consigliabile applicare le massime restrizioni nell'assegnazione delle autorizzazioni per questa directory. È necessario selezionare le autorizzazioni **Lettura** ed **Esecuzione** ma è possibile deselezionare le autorizzazioni **Esecuzione script**, **Scrittura**ed **Esplorazione** .  
  
6.  Configurare IIS in modo da consentire l'esecuzione di replisapi.dll. Le autorizzazioni assegnate nel passaggio 4 sono sufficienti per le versioni precedenti di IIS, ma IIS 6.0 richiede l'abilitazione delle estensioni ISAPI (Internet Server API). Per ulteriori informazioni, vedere le sezioni relative alla configurazione di estensioni ISAPI e all'abilitazione e disabilitazione di contenuto dinamico nella documentazione di IIS 6.0.  
  
#### <a name="to-configure-iis-authentication"></a>Per configurare l'autenticazione di IIS  
  
-   Quando i Sottoscrittori si connettono a IIS, è necessario che vengano autenticati da IIS affinché possano accedere a risorse e processi. IIS offre tre tipi di autenticazione: anonima, di base e integrata. L'autenticazione può essere applicata all'intero sito Web oppure alla directory virtuale creata.  
  
     È consigliabile utilizzare l'autenticazione di base con SSL. SSL è necessario indipendentemente dal tipo di autenticazione utilizzato. Per ulteriori informazioni sulla configurazione dell'autenticazione, vedere la documentazione di IIS.  
  
## <a name="setting-permissions-for-the-sql-server-replication-listener"></a>Impostazione delle autorizzazioni per Listener per la replica di SQL Server  
 Quando un Sottoscrittore si connette al computer che esegue IIS, viene autenticato mediante il tipo di autenticazione specificato durante la configurazione di IIS. Dopo l'autenticazione del Sottoscrittore, IIS controlla se il Sottoscrittore è autorizzato a richiamare la replica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per controllare gli utenti autorizzati a richiamare le replica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è necessario impostare le autorizzazioni per replisapi.dll. La corretta configurazione delle autorizzazioni è fondamentale per impedire l'accesso non autorizzato alla replica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Per configurare le autorizzazioni minime per l'account utilizzato per l'esecuzione di Listener per la replica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , completare la procedura seguente. I passaggi della procedura sono validi per [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)] con IIS 6.0.  
  
 Oltre a eseguire la procedura seguente, assicurarsi che gli account di accesso necessari siano inclusi nell'elenco di accesso alla pubblicazione. Per altre informazioni sull'elenco di acceso alla pubblicazione, vedere [Proteggere il server di pubblicazione](../../relational-databases/replication/security/secure-the-publisher.md).  
  
#### <a name="to-configure-the-account-and-permissions"></a>Per configurare l'account e le autorizzazioni  
  
1.  Creare un account locale nel computer che esegue IIS:  
  
    1.  Fare clic con il pulsante destro del mouse su **Risorse del computer**e quindi scegliere **Gestione**.  
  
    2.  In **Gestione computer**espandere **Utenti e gruppi locali**.  
  
    3.  Fare clic con il pulsante destro del mouse su **Utenti**e quindi scegliere **Nuovo utente**.  
  
    4.  Immettere un nome utente e una password complessa.  
  
    5.  Fare clic su **Crea**e quindi su **Chiudi**.  
  
2.  Aggiungere l'account al gruppo IIS_WPG:  
  
    1.  In **Gestione computer**espandere **Utenti e gruppi locali**e quindi fare clic su **Gruppi**.  
  
    2.  Fare clic con il pulsante destro del mouse su **IIS_WPG**e quindi scegliere **Aggiungi al gruppo**.  
  
    3.  Nella finestra di dialogo **Proprietà - IIS_WPG** fare clic su **Aggiungi**.  
  
    4.  Nella finestra di dialogo **Seleziona Utenti** aggiungere l'account creato nel passaggio 1.  
  
    5.  Assicurarsi che nel campo **Da questo percorso** sia presente il nome del computer locale e non di un dominio. Se il nome non corrisponde a un computer locale, fare clic su **Percorsi**. Nella finestra di dialogo **Percorsi** selezionare il computer locale e quindi fare clic su **OK**.  
  
    6.  Nelle finestre di dialogo **Seleziona Utenti** e **Proprietà - IIS_WPG** fare clic su **OK**.  
  
3.  Concedere all'account le autorizzazioni minime per la cartella contenente replisapi.dll:  
  
    1.  Fare clic con il pulsante destro del mouse sulla cartella creata per replisapi.dll e quindi scegliere **Condivisione e sicurezza**.  
  
    2.  Nella scheda **Sicurezza** fare clic su **Aggiungi**.  
  
    3.  Nella finestra di dialogo **Seleziona Utenti** aggiungere l'account creato nel passaggio 1.  
  
    4.  Assicurarsi che nel campo **Da questo percorso** sia presente il nome del computer locale e non di un dominio. Se il nome non corrisponde a un computer locale, fare clic su **Percorsi**. Nella finestra di dialogo **Percorsi** selezionare il computer locale e quindi fare clic su **OK**.  
  
    5.  Assicurarsi che all'account siano concesse soltanto le autorizzazioni **Lettura**, **Lettura ed esecuzione** e **Visualizzazione contenuto cartella**.  
  
    6.  Selezionare gli utenti o i gruppi che non necessitano dell'accesso alla directory e quindi fare clic su **Rimuovi**.  
  
    7.  Fare clic su **OK**.  
  
4.  Creare un pool di applicazioni in **Gestione Internet Information Services (IIS)** :  
  
    1.  Fare clic sul pulsante **Start**e quindi scegliere **Esegui**.  
  
    2.  Digitare **inetmgr** nella casella **Apri**e quindi fare clic su **OK**.  
  
    3.  In **Gestione Internet Information Services (IIS)** espandere il nodo **computer locale** .  
  
    4.  Fare clic con il pulsante destro del mouse su **Pool di applicazioni**, scegliere **Nuovo** e quindi **Pool di applicazioni**.  
  
    5.  Immettere un nome per il pool nel campo **ID pool di applicazioni** e quindi fare clic su **OK**.  
  
5.  Associare l'account al pool di applicazioni:  
  
    1.  In **Gestione Internet Information Services (IIS)** espandere il nodo **computer locale** e quindi **Pool di applicazioni**.  
  
    2.  Fare clic con il pulsante destro del mouse sul pool di applicazioni creato e quindi scegliere **Proprietà**.  
  
    3.  Nella scheda **Identità\< della finestra di dialogo** Proprietà - **NomePoolApplicazioni>** fare clic su **Configurabile**.  
  
    4.  Nei campi **Nome utente** e **Password** immettere l'account e la password creati nel passaggio 1.  
  
    5.  Fare clic su **OK**.  
  
6.  Associare il pool di applicazioni alla directory virtuale utilizzata per la sincronizzazione Web:  
  
    1.  In **Gestione Internet Information Services (IIS)** espandere il nodo **computer locale** e quindi **Siti Web**.  
  
    2.  Espandere il sito Web utilizzato per la sincronizzazione Web, fare clic con il pulsante destro del mouse sulla directory virtuale creata per tale sincronizzazione e quindi scegliere **Proprietà**.  
  
    3.  Nella scheda **Directory virtuale** della finestra di dialogo **Proprietà - \<NomeDirectoryVirtuale>** selezionare il pool di applicazioni creato nel passaggio 5 nell'elenco a discesa **Pool di applicazioni**.  
  
    4.  Fare clic su **OK**.  
  
## <a name="testing-the-connection-to-replisapidll"></a>Test della connessione a replisapi.dll  
 Eseguire la sincronizzazione Web in modalità diagnostica per testare la connessione al computer che esegue IIS e verificare la corretta installazione del certificato SSL (Secure Sockets Layer). Per eseguire la sincronizzazione Web in modalità diagnostica, è necessario disporre dei privilegi di amministratore sul computer che esegue IIS.  
  
#### <a name="to-test-the-connection-to-replisapidll"></a>Per testare la connessione a replisapi.dll  
  
1.  Assicurarsi che le impostazioni per la rete LAN (Local Area Network) nel Sottoscrittore siano corrette:  
  
    1.  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer fare clic su **Opzioni Internet** dal menu **Strumenti**.  
  
    2.  Nella scheda **Connessioni** fare clic su **Impostazioni LAN**.  
  
    3.  Se nella rete LAN non viene utilizzato un server proxy, deselezionare **Rileva automaticamente impostazioni** e **Utilizza un server proxy server per le connessioni LAN**.  
  
    4.  Se viene utilizzato un server proxy, selezionare **Utilizza un server proxy server per le connessioni LAN** e **Ignora server proxy per indirizzi locali**.  
  
    5.  Fare clic su **OK**.  
  
2.  Nel Sottoscrittore, in Internet Explorer, connettersi al server in modalità diagnostica aggiungendo `?diag` alla fine dell'indirizzo di replisapi.dll. Ad esempio: `https://server.domain.com/directory/replisapi.dll?diag`.  
  
3.  Se il certificato specificato per IIS non viene riconosciuto dal sistema operativo Windows, viene visualizzata la finestra di dialogo **Avviso di sicurezza** . Questo avviso può essere visualizzato perché il certificato è un certificato di prova o è stato emesso da un'autorità di certificazione non riconosciuta da Windows.  
  
    > [!NOTE]  
    >  Se questa finestra di dialogo non viene visualizzata, verificare che il certificato per il server a cui si accede sia stato aggiunto all'archivio certificati nel Sottoscrittore come certificato attendibile. Per ulteriori informazioni sull'esportazione dei certificati, vedere la documentazione di IIS.  
  
    1.  Nella finestra di dialogo **Avviso di sicurezza** fare clic su **Visualizza certificato**.  
  
    2.  Nella scheda **Generale** della finestra di dialogo **Certificato** fare clic su **Installa certificato**.  
  
    3.  Completare l'Importazione guidata certificati, accettando le impostazioni predefinite.  
  
    4.  Nella finestra di dialogo **Avviso di sicurezza** fare clic su **Sì**.  
  
    5.  Nella finestra di dialogo di conferma dell'Importazione guidata certificati fare clic su **OK**.  
  
    6.  Chiudere la finestra di dialogo **Certificato** .  
  
    7.  Nella finestra di dialogo **Avviso di sicurezza** fare clic su **Sì**.  
  
    > [!NOTE]  
    >  I certificati vengono installati per gli utenti. Questo processo deve pertanto essere eseguito per ogni utente che eseguirà la sincronizzazione con IIS.  
  
4.  Nella finestra di dialogo **Connetti a \<NomeServer>** specificare l'account di accesso e la password che verranno usati dall'agente di merge per la connessione a IIS. Queste credenziali verranno inoltre specificate nella Creazione guidata nuova sottoscrizione.  
  
5.  Nella finestra di Internet Explorer denominata **Informazioni diagnostica SQL Websync**, verificare che il valore contenuto in ogni colonna **Stato** della pagina sia **SUCCESS**.  
  
6.  Assicurarsi che il certificato sia installato correttamente nel Sottoscrittore:  
  
    1.  Chiudere e riaprire Internet Explorer.  
  
    2.  Connettersi al server in modalità diagnostica. Se il certificato è stato installato correttamente, la finestra di dialogo **Avviso di sicurezza** non verrà visualizzata. Se la finestra di dialogo viene visualizzata, i tentativi dell'agente di merge di connettersi al computer che esegue IIS avranno esito negativo. È necessario verificare che il certificato per il server a cui si accede sia stato aggiunto all'archivio certificati del Sottoscrittore come certificato attendibile. Per ulteriori informazioni sull'esportazione dei certificati, vedere la documentazione di IIS.  
  
## <a name="see-also"></a>Vedere anche  
 [Configura sincronizzazione Web](../../relational-databases/replication/configure-web-synchronization.md)  
  
  
