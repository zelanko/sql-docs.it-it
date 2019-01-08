---
title: Configurare IIS 7 per la sincronizzazione Web | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- IIS 7 server configuration [SQL Server replication]
- Web synchronization, IIS 7 servers
ms.assetid: c201fe2c-0a76-44e5-a233-05e14cd224a6
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 539b47ebbd8f4a2374849c0b1d5244d187cdd3df
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52819333"
---
# <a name="configure-iis-7-for-web-synchronization"></a>Configurare IIS 7 per la sincronizzazione Web
  Le procedure di questo argomento illustrano il processo di configurazione manuale di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Information Services (IIS) versione 7 e successive per l'uso con la sincronizzazione Web per la replica di tipo merge. 
  
 La configurazione di IIS 7 è il primo di tre passaggi necessari per abilitare la sincronizzazione Web.  
  
 Per una panoramica del processo di configurazione, vedere [Configurare la sincronizzazione Web](configure-web-synchronization.md).  
  
> [!IMPORTANT]  
>  Verificare che nell'applicazione venga utilizzato solo [!INCLUDE[dnprdnlong](../../includes/dnprdnlong-md.md)] o versione successiva e che le versioni precedenti di [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] non siano installate sul server IIS. Le versioni precedenti del [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] possono causare errori, ad esempio: "Formato di messaggio non valido durante la sincronizzazione Web. Verificare che i componenti di replica siano configurati correttamente nel server Web".  
  
 Per utilizzare la sincronizzazione Web, è necessario configurare IIS 7 completando i passaggi seguenti. Ogni passaggio è descritto in dettaglio in questo argomento.  
  
1.  Installare e configurare il listener per la replica di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nel computer in cui viene eseguito IIS.  
  
2.  Configurare SSL (Secure Sockets Layer). L'utilizzo di SSL è obbligatorio per la comunicazione tra IIS e tutti i Sottoscrittori.  
  
3.  Configurare l'autenticazione IIS.  
  
4.  Configurare un account e impostare le autorizzazioni per il listener per la replica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="installing-the-sql-server-replication-listener"></a>Installazione del listener per la replica di SQL Server  

La sincronizzazione Web è supportata in IIS a partire dalla versione 5.0. La Configurazione guidata sincronizzazione Web di IIS versione 5 e 6 non è disponibile con IIS versione 7.0 e successive. **A partire da SQL Server 2012, per usare il componente di sincronizzazione Web nel server IIS, è necessario installare SQL Server con la replica. Ad esempio, è possibile installare l'edizione gratuita SQL Server Express.**
  
#### <a name="to-install-and-configure-the-sql-server-replication-listener"></a>Per installare e configurare Listener per la replica di SQL Server  
  
1. Installare la replica di SQL Server nel computer IIS.

2.  Creare una nuova directory di file per replisapi.dll nel computer che esegue IIS. Sebbene sia possibile creare la directory in un percorso qualsiasi, è consigliabile crearla nella directory \<*unità*>:\Inetpub. Ad esempio, creare la directory \<*unità*>:\Inetpub\SQLReplication\\.  
  
3.  Copiare replisapi.dll dalla directory [!INCLUDE[ssInstallPathVar](../../includes/ssinstallpathvar-md.md)]com\ alla directory di file creata nel passaggio 1.  
  
4.  Registrare replisapi.dll:  
  
    1.  Fare clic sul pulsante **Start**e quindi scegliere **Esegui**. Nel **aperto** immettere `cmd`, quindi fare clic su **OK**.  
  
    2.  Nella directory creata nel passaggio 1 eseguire il comando riportato di seguito:  
  
         `regsvr32 replisapi.dll`  
  
5.  Creare un nuovo sito Web per la replica oppure utilizzare un sito esistente. I componenti di replica accederanno al sito Web durante la sincronizzazione. Nelle procedure di questo argomento si presuppone l'utilizzo del sito Web predefinito. Per ulteriori informazioni sulla creazione di siti Web, vedere la documentazione di IIS.  
  
6.  Creare una directory virtuale in IIS. È consigliabile creare la directory virtuale nel sito Web creato nel passaggio 4 ed eseguirne il mapping alla directory creata nel passaggio 1. È consigliabile applicare le massime restrizioni nell'assegnazione delle autorizzazioni per questa directory. È necessario selezionare almeno autorizzazioni **Lettura** ed **Esecuzione** .  
  
    1.  In **Gestione Internet Information Services (IIS)**, nel riquadro **Connessioni** fare clic con il pulsante destro del mouse su **Sito Web predefinito**, quindi selezionare **Aggiungi directory virtuale**.  
  
    2.  Per la **Alias**, immettere `SQLReplication`.  
  
    3.  In **Percorso fisico** immettere **\<unità>:\Inetpub\SQLReplication\\** e quindi fare clic su **OK**.  
  
7.  Configurare IIS in modo da consentire l'esecuzione di replisapi.dll.  
  
    1.  In **Gestione Internet Information Services (IIS)** fare clic su **Sito Web predefinito**.  
  
    2.  Nel riquadro centrale fare clic su **Mapping gestori**.  
  
    3.  Nel riquadro **Azioni** fare clic su **Aggiungi mapping moduli**.  
  
    4.  Per la **richiedere** percorso, immettere `replisapi.dll`.  
  
    5.  Nell'elenco a discesa **Modulo** selezionare **IsapiModule**.  
  
    6.  In **Eseguibile** immettere **\<unità>: \Inetpub\SQLReplication\replisapi.dll**.  
  
    7.  Per la **Name**, immettere `Replisapi`.  
  
    8.  Fare clic sul pulsante **Restrizioni richieste** , fare clic sulla scheda **Accesso** , quindi scegliere **Esegui**.  
  
    9. Per chiudere la finestra di dialogo **Restrizioni richieste** , fare clic su **OK** , quindi fare nuovamente clic su **OK** per chiudere la finestra di dialogo **Aggiungi mapping moduli** . Quando viene richiesto di consentire l'estensione ISAPI, fare clic su **Sì** per aggiungere l'estensione.  
  
    10. Verificare che Replisapi.dll sia elencato sotto i mapping dei gestori contrassegnati come **Abilitato** . Se si trova nell'elenco **Disabilitato** , fare clic con il pulsante destro del mouse sulla voce Replisapi, quindi scegliere **Modifica autorizzazioni funzionalità**. Selezionare la casella **Esegui** , quindi fare clic su **OK**.  
  
## <a name="configuring-iis-authentication"></a>Configurazione dell'autenticazione IIS  
 Quando i computer Sottoscrittori si connettono a IIS, è necessario che vengano autenticati da IIS per poter accedere a risorse e processi. L'autenticazione può essere applicata all'intero sito Web oppure alla directory virtuale creata.  
  
 È consigliabile utilizzare l'autenticazione di base con SSL. SSL è necessario indipendentemente dal tipo di autenticazione utilizzato.  
  
 È consigliabile utilizzare l'autenticazione di base con SSL. SSL è necessario indipendentemente dal tipo di autenticazione utilizzato.  
  
#### <a name="to-configure-iis-authentication"></a>Per configurare l'autenticazione IIS  
  
1.  In **Gestione Internet Information Services (IIS)** fare clic su **Sito Web predefinito**.  
  
2.  Nel riquadro centrale fare doppio clic su **Autenticazione**.  
  
3.  Fare clic con il pulsante destro del mouse su Autenticazione anonima, quindi scegliere Disabilita.  
  
4.  Fare clic con il pulsante destro del mouse su Autenticazione di base, quindi scegliere Abilita.  
  
## <a name="configuring-secure-sockets-layer"></a>Configurazione di SSL (Secure Sockets Layer)  
 Per configurare SSL, specificare un certificato che verrà utilizzato dal computer che esegue IIS. La sincronizzazione Web per la replica di tipo merge supporta l'utilizzo di certificati server, ma non di certificati client. Per configurare IIS per la distribuzione, è innanzitutto necessario ottenere un certificato da un'autorità di certificazione. Per ulteriori informazioni sui certificati, vedere la documentazione di IIS.  
  
 Dopo l'installazione del certificato, è necessario associare il certificato al sito Web utilizzato nella sincronizzazione Web. Per lo sviluppo e i test, è possibile specificare un certificato autofirmato. Con IIS 7 è possibile creare un certificato e registrarlo nel computer.  
  
 La differenza tra la distribuzione per la produzione e le procedure fornite in questo argomento è data dal fatto che nei test di produzione e pre-produzione si utilizza un certificato rilasciato da una CA anziché un certificato autofirmato.  
  
> [!IMPORTANT]  
>  Non è consigliabile utilizzare un certificato autofirmato per un'installazione di produzione. I certificati autofirmati non sono sicuri. Utilizzare tali certificati solo ai fini di sviluppo e test.  
  
 Per configurare SSL, verranno eseguiti i passaggi riportati di seguito:  
  
1.  Configurare il sito Web per richiedere SSL e ignorare i certificati client.  
  
2.  Ottenere un certificato da una CA o creare un certificato autofirmato.  
  
3.  Associare il certificato al sito Web per la replica.  
  
#### <a name="to-require-ssl-security-for-a-web-site"></a>Per richiedere la sicurezza SSL per un sito Web  
  
1.  In **Gestione Internet Information Services (IIS)** espandere il nodo del server locale, quindi fare clic su **Sito Web predefinito** o sul sito di sincronizzazione Web se è diverso dal sito Web predefinito.  
  
2.  Nel riquadro centrale fare doppio clic su **Impostazioni SSL**.  
  
3.  Selezionare l'opzione **Richiedi SSL** . In **Certificati client**verificare che il pulsante **Ignora** sia selezionato.  
  
#### <a name="to-create-a-self-signed-certificate-for-testing"></a>Per creare un certificato autofirmato per i test  
  
1.  In **Gestione Internet Information Services (IIS)** fare clic sul nodo del server locale, quindi fare doppio clic su **Certificati server**.  
  
2.  Nel riquadro **Azioni** fare clic su **Crea certificato autofirmato**.  
  
3.  Nella finestra di dialogo **Crea certificato autofirmato** immettere un nome per il certificato, quindi fare clic su **OK**.  
  
###### <a name="to-bind-a-certificate-to-a-web-site"></a>Per associare un certificato a un sito Web  
  
1.  Nel riquadro **Connessioni** fare clic su **Sito Web predefinito** o sul sito di sincronizzazione Web se è diverso dal sito Web predefinito.  
  
2.  Nel riquadro **Azioni** fare clic su **Binding**, quindi su **Aggiungi**. Verrà visualizzata la finestra di dialogo **Aggiungi binding sito** .  
  
3.  Nell'elenco a discesa **Tipo** selezionare **https**. Mantenere le impostazioni predefinite per **Indirizzo IP** e **Porta**.  
  
4.  Nell'elenco a discesa **Certificato SSL** selezionare il certificato creato in "Per creare un certificato autofirmato per i test", fare clic su **OK**, quindi su **Chiudi**.  
  
###### <a name="to-test-the-certificate"></a>Per testare il certificato  
  
1.  In **Gestione Internet Information Services (IIS)** fare clic su **Sito Web predefinito.**  
  
2.  Nel riquadro **Azioni** fare clic su **Sfoglia \*:443 (https)**.  
  
3.  Verrà aperto Internet Explorer e verrà visualizzato il messaggio "Si è verificato un problema con il certificato di sicurezza del sito Web". Questo avviso suggerisce che il certificato associato non è stato rilasciato da una CA riconosciuta e potrebbe non essere attendibile. Si tratta di un avviso previsto, pertanto fare clic su **Continuare con il sito Web (scelta non consigliata)**.  
  
4.  Se viene visualizzata la richiesta **Connetti a localhost**, immettere un nome utente e una password per continuare. Dovrebbe venire visualizzata la pagina predefinita del sito Web.  
  
## <a name="setting-permissions-for-the-sql-server-replication-listener"></a>Impostazione delle autorizzazioni per Listener per la replica di SQL Server  
 Quando un computer Sottoscrittore si connette al computer che esegue IIS, viene autenticato mediante il tipo di autenticazione specificato durante la configurazione di IIS. Dopo l'autenticazione del Sottoscrittore, in IIS viene controllato se il Sottoscrittore è autorizzato a richiamare la replica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per controllare gli utenti autorizzati a richiamare le replica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , è necessario impostare le autorizzazioni per replisapi.dll. La corretta configurazione delle autorizzazioni è fondamentale per impedire l'accesso non autorizzato alla replica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Per configurare le autorizzazioni minime per l'account utilizzato per l'esecuzione di Listener per la replica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , completare la procedura seguente. I passaggi della procedura seguente sono validi per [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows Server 2008 con IIS 7.0.  
  
 Oltre a eseguire la procedura seguente, assicurarsi che gli account di accesso necessari siano inclusi nell'elenco di accesso alla pubblicazione. Per altre informazioni sull'elenco di acceso alla pubblicazione, vedere [Proteggere il server di pubblicazione](security/secure-the-publisher.md).  
  
 **Importante** L'account creato in questa sezione è quello che verrà utilizzato per la connessione al server di pubblicazione e al database di distribuzione durante la sincronizzazione. È necessario aggiungere questo account come account di accesso SQL nel server di distribuzione e di pubblicazione.  
  
 L'account utilizzato per il listener per la replica di SQL Server deve disporre di autorizzazioni come descritto nell'argomento Sicurezza dell'agente di merge, nella sezione "Connettersi al server di pubblicazione o al database di distribuzione".  
  
 In breve è necessario che l'account:  
  
-   sia membro dell'elenco di accesso alla pubblicazione;  
  
-   sia sottoposto a mapping a un account di accesso associato a un utente nel database di pubblicazione;  
  
-   sia sottoposto a mapping a un account di accesso associato a un utente nel database di distribuzione;  
  
-   disponga delle autorizzazioni di lettura per la condivisione snapshot.  
  
#### <a name="to-configure-the-account-and-permissions"></a>Per configurare l'account e le autorizzazioni  
  
1.  Creare un account locale nel computer che esegue IIS:  
  
    1.  Aprire **Gestione server**. Dal menu Start fare clic con il pulsante destro del mouse su **Computer**e scegliere **Gestisci**.  
  
    2.  In **Gestione server**espandere **Configurazione**, quindi **Utenti e gruppi locali**.  
  
    3.  Fare clic con il pulsante destro del mouse su **Utenti**e quindi scegliere **Nuovo utente**.  
  
    4.  Immettere un nome utente e una password complessa. Deselezionare **Cambiamento obbligatorio password all'accesso successivo**.  
  
    5.  Fare clic su **Crea**e quindi su **Chiudi**.  
  
2.  Aggiungere l'account al gruppo IIS_IUSRS:  
  
    1.  In **Gestione server**espandere **Configurazione**e **Utenti e gruppi locali**, quindi fare clic su **Gruppi**.  
  
    2.  Fare clic con il pulsante destro del mouse su **IIS_IUSRS**, quindi fare clic su **Aggiungi al gruppo**.  
  
    3.  Nella finestra di dialogo **Proprietà - IIS_IUSRS** fare clic su **Aggiungi**.  
  
    4.  Nella finestra di dialogo **Seleziona Utenti** aggiungere l'account creato nel passaggio 1.  
  
    5.  Assicurarsi che nel campo **Da questo percorso** sia visualizzato il nome del computer locale (non di un dominio). Se in questo campo non è visualizzato il nome del computer locale, fare clic su **Percorsi**. Nella finestra di dialogo **Percorsi** selezionare il computer locale e quindi fare clic su **OK**.  
  
    6.  Nelle finestre di dialogo **Seleziona utenti** e **Proprietà - IIS_IUSRS** fare clic su**OK**.  
  
3.  Concedere all'account le autorizzazioni minime per la cartella contenente replisapi.dll:  
  
    1.  In Windows Explorer fare clic con il pulsante destro del mouse sulla cartella creata per replisapi.dll, quindi scegliere **Proprietà**.  
  
    2.  Nella scheda **Sicurezza** fare clic su **Modifica**.  
  
    3.  Nella finestra di dialogo **Autorizzazioni per \<nomecartella>** fare clic su **Aggiungi** per aggiungere l'account creato nel passaggio 1.  
  
    4.  Assicurarsi che nel campo **Da questo percorso** sia visualizzato il nome del computer locale (non di un dominio). Se in questo campo non è visualizzato il nome del computer locale, fare clic su **Percorsi**. Nella finestra di dialogo **Percorsi** selezionare il computer locale e quindi fare clic su **OK**.  
  
    5.  Verificare che all'account siano concesse soltanto le autorizzazioni **Lettura**, **Lettura ed esecuzione** e **Visualizzazione contenuto cartella**.  
  
    6.  Selezionare gli utenti o i gruppi che non necessitano dell'accesso alla directory, quindi fare clic su **Rimuovi**e su **OK**.  
  
4.  Creare un pool di applicazioni in **Gestione Internet Information Services (IIS)**:  
  
    1.  In **Gestione Internet Information Services (IIS)**, nel riquadro **Connessioni** espandere il nodo del server locale.  
  
    2.  Fare clic con il pulsante destro del mouse su **Pool di applicazioni**, quindi scegliere **Aggiungi pool di applicazioni**.  
  
    3.  Immettere un nome per il pool di applicazioni, mantenere i valori predefiniti per i campi rimanenti, quindi fare clic su **OK**.  
  
    > [!NOTE]  
    >  Se si prevede di utilizzare più di due client di sincronizzazione simultanei, è necessario creare un Web garden. Per altre informazioni, vedere "Creazione di un Web garden" in [Configurare la sincronizzazione Web](configure-web-synchronization.md).  
  
5.  Associare l'account al pool di applicazioni:  
  
    1.  In **Gestione Internet Information Services (IIS)** espandere il nodo del server locale, quindi fare clic su **Pool di applicazioni**.  
  
    2.  Fare clic con il pulsante destro del mouse sul pool di applicazioni creato, quindi scegliere **Impostazioni predefinite pool di applicazioni**.  
  
    3.  Nella finestra di dialogo **Impostazioni predefinite pool di applicazioni** passare alla sezione **Modello di processo** , quindi fare clic sul campo **Identità** .  
  
    4.  Fare clic sul pulsante con i puntini di sospensione sul lato destro della riga **Identità** .  
  
    5.  Fare clic sul pulsante di opzione **Account personalizzato** , quindi su **Imposta**.  
  
    6.  Nei campi **Nome utente** e **Password** immettere l'account e la password creati nel passaggio 1, quindi fare clic su **OK**.  
  
    7.  Fare clic su **OK** per chiudere la finestra di dialogo **Identità pool di applicazioni** , quindi fare nuovamente clic su **OK** per chiudere la finestra di dialogo **Impostazioni predefinite pool di applicazioni**.  
  
6.  Associare il pool di applicazioni al sito Web per la replica:  
  
    1.  In **Gestione Internet Information Services (IIS)** espandere il nodo del server locale, quindi fare clic su **Sito Web predefinito** o sul sito di sincronizzazione Web se è diverso dal sito Web predefinito.  
  
    2.  Nel riquadro **Azioni** , in **Gestione sito Web**fare clic su **Impostazioni avanzate**.  
  
    3.  Nella finestra di dialogo **Impostazioni avanzate** fare clic sul pulsante con i puntini di sospensione a destra di **Pool di applicazioni**.  
  
    4.  Nell'elenco a discesa **Pool di applicazioni** selezionare il pool di applicazioni creato nel passaggio 4, quindi fare clic su **OK**.  
  
    5.  Fare nuovamente clic su **OK** per chiudere Impostazioni avanzate.  
  
## <a name="testing-the-connection-to-replisapidll"></a>Test della connessione a replisapi.dll  
 Eseguire la sincronizzazione Web in modalità diagnostica per testare la connessione al computer che esegue IIS e verificare la corretta installazione del certificato SSL (Secure Sockets Layer). Per eseguire la sincronizzazione Web in modalità diagnostica, è necessario disporre dei privilegi di amministratore sul computer che esegue IIS.  
  
#### <a name="to-test-the-connection-to-replisapidll"></a>Per testare la connessione a replisapi.dll  
  
1.  Assicurarsi che le impostazioni per la rete LAN (Local Area Network) nel Sottoscrittore siano corrette:  
  
    1.  In [!INCLUDE[msCoName](../../includes/msconame-md.md)] Internet Explorer fare clic su **Opzioni Internet** dal menu **Strumenti**.  
  
    2.  Nella scheda **Connessioni** fare clic su **Impostazioni LAN**.  
  
    3.  Se nella rete LAN non viene utilizzato un server proxy, deselezionare **Rileva automaticamente impostazioni** e **Utilizza un server proxy server per le connessioni LAN**.  
  
    4.  Se viene utilizzato un server proxy, selezionare **Utilizza un server proxy per le connessioni LAN** e **Ignora server proxy per indirizzi locali**, quindi fare clic su **OK**.  
  
2.  Nel Sottoscrittore, in Internet Explorer, connettersi al server in modalità diagnostica aggiungendo `?diag` alla fine dell'indirizzo di replisapi.dll. Ad esempio: **https://server.domain.com/directory/replisapi.dll?diag**.  
  
    > [!NOTE]  
    >  Nell'esempio precedente sostituire **server.dominio.com** con il nome esatto di **Rilasciato a** elencato nella sezione **Certificati del server** in Gestione IIS.  
  
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
 [Sincronizzazione Web per la replica di tipo merge](web-synchronization-for-merge-replication.md)   
 [Configurare la sincronizzazione Web](configure-web-synchronization.md)  
  
  
