---
title: Configurare l'accesso HTTP ad Analysis Services in Internet Information Services (IIS) 8.0 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: cf2e2c84-0a69-4cdd-90a1-fb4021936513
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4c8af52dfe8c95b80f5b9550b41a14e1f70c7a6e
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66080169"
---
# <a name="configure-http-access-to-analysis-services-on-internet-information-services-iis-80"></a>Configurare l'accesso HTTP ad Analysis Services in Internet Information Services (IIS) 8.0
  In questo articolo viene illustrato come configurare un endpoint HTTP per l'accesso a un'istanza di Analysis Services. È possibile abilitare l'accesso HTTP configurando MSMDPUMP.dll, un'estensione ISAPI che viene eseguita in IIS (Internet Information Services) e che consente di eseguire attività di data pump da applicazioni client a un server Analysis Services e viceversa. Questo approccio fornisce un'alternativa per la connessione ad Analysis Services se per le soluzioni Business Intelligence in uso sono richieste le funzionalità seguenti:  
  
-   L'accesso client viene eseguito tramite connessioni Internet o Extranet, con restrizioni relativamente alle porte che è possibile abilitare.  
  
-   Le connessioni client hanno origine da domini non attendibili nella stessa rete.  
  
-   Le applicazioni client vengono eseguite in un ambiente di rete che consente connessioni HTTP ma non TCP/IP.  
  
-   Nelle applicazioni client non è possibile utilizzare le librerie client di Analysis Services (ad esempio, un'applicazione Java in esecuzione in un server UNIX). Se non è possibile utilizzare le librerie client di Analysis Services per l'accesso ai dati, è possibile utilizzare SOAP e XML/A in una connessione HTTP diretta a un'istanza di Analysis Services.  
  
-   Sono richiesti metodi di autenticazione diversi dalla sicurezza integrata di Windows. In particolare, è possibile utilizzare le connessioni anonime e l'autenticazione di base quando si configura Analysis Services per l'accesso HTTP. Le autenticazioni Digest, basate su form e ASP.NET non sono supportate. Un requisito di autenticazione di base è uno dei motivi principali per l'abilitazione dell'accesso HTTP. Per altre informazioni, vedere [Microsoft BI Authentication and Identity Delegation](https://go.microsoft.com/fwlink/?LinkId=286576) (Autenticazione a Microsoft BI e delega d'identità).  
  
 È possibile configurare l'accesso HTTP per qualsiasi versione o edizione supportata di Analysis Services con l'esecuzione in modalità tabulare o multidimensionale. I cubi locali sono un'eccezione. È possibile connettersi a un cubo locale tramite un endpoint HTTP.  
  
 L'impostazione dell'accesso HTTP è un'attività di post-installazione. Analysis Services deve essere installato prima di configurarlo per l'accesso HTTP. Come amministratore di Analysis Services, sarà necessario concedere autorizzazioni agli account di Windows prima che sia possibile eseguire l'accesso HTTP. Inoltre, è buona norma convalidare prima di tutto l'installazione, verificando che sia pienamente operativa prima di proseguire la configurazione del server. Dopo aver configurato l'accesso HTTP, è possibile usare sia l'endpoint HTTP sia il nome di rete regolare del server su TCP/IP. La configurazione dell'accesso HTTP non invalida altri approcci per l'accesso ai dati.  
  
 Proseguendo nella configurazione di MSMDPUMP, tenere presente che ci sono due connessioni da considerare: da client a IIS e da IIS a SSAS. Le istruzioni in questo articolo riguardano la connessione da IIS a SSAS. L'applicazione client potrebbe richiedere una configurazione aggiuntiva per la connessione a IIS. Le decisioni riguardanti l'uso di SSL o la configurazione delle associazioni non sono comprese nell'ambito di questo articolo. Per altre informazioni su IIS, vedere [Web Server (IIS)](https://technet.microsoft.com/library/hh831725.aspx).  
  
 In questo argomento sono contenute le sezioni seguenti:  
  
-   [Panoramica](#bkmk_overview)  
  
-   [Prerequisiti](#bkmk_prereq)  
  
-   [Copiare il file MSMDPUMP.dll in una cartella sul server Web](#bkmk_copy)  
  
-   [Creare un pool di applicazioni e una directory virtuale in IIS](#bkmk_appPool)  
  
-   [Configurare l'autenticazione IIS e aggiungere l'estensione](#bkmk_auth)  
  
-   [Modificare il file MSMDPUMP.INI per impostare il server di destinazione](#bkmk_edit)  
  
-   [Testare la configurazione](#bkmk_test)  
  
##  <a name="bkmk_overview"></a> Panoramica  
 MSMDPUMP è un'estensione ISAPI che viene caricata in IIS e fornisce il reindirizzamento a un'istanza di Analysis Services locale o remota. Configurando l'estensione ISAPI, viene creato un endpoint HTTP a un'istanza di Analysis Services.  
  
 Per ogni endpoint HTTP è necessario creare e configurare una directory virtuale. A ogni endpoint dovrà essere associato un proprio set di file MSMDPUMP, per ogni istanza di Analysis Services a cui si desidera effettuare la connessione. In un file di configurazione in questo set di file viene specificato il nome dell'istanza di Analysis Services utilizzata per ciascun endpoint HTTP.  
  
 In IIS la connessione di MSMDPUMP ad Analysis Services viene eseguita tramite il provider OLE DB di Analysis Services su TCP/IP. Anche se le richieste client possono avere origine all'esterno del trust del dominio, Analysis Services e IIS devono essere nello stesso dominio o in domini trusted affinché la connessione nativa abbia esito positivo.  
  
 Per la connessione di MSMDPUMP ad Analysis Services, viene utilizzata un'identità utente di Windows. Questo account sarà un account anonimo se è stata configurata la directory virtuale per le connessioni anonime o un account utente di Windows. L'account deve disporre dei diritti di accesso ai dati adatti per il database e il server Analysis Services.  
  
 ![Diagramma che mostra le connessioni tra i componenti](../media/ssas.gif "diagramma che mostra le connessioni tra i componenti")  
  
 Nella tabella seguente vengono elencate ulteriori considerazioni relative all'abilitazione dell'accesso HTTP per scenari diversi.  
  
|Scenario|Configurazione|  
|--------------|-------------------|  
|IIS e Analysis Services nello stesso computer|Si tratta della configurazione più semplice in quanto consente all'utente di utilizzare la configurazione predefinita (dove il nome del server è localhost), il provider OLE DB locale per Analysis Services e la sicurezza integrata di Windows con NTLM. Presupponendo che anche il client si trovi nello stesso dominio, l'autenticazione è visibile all'utente, senza la necessità di lavoro aggiuntivo.|  
|IIS e Analysis Services in computer diversi|Per questa topologia, è necessario installare il provider OLE DB di Analysis Services nel server Web. È inoltre necessario modificare il file msmdpump.ini per specificare il percorso dell'istanza di Analysis Services nel computer remoto.<br /><br /> In questa topologia viene aggiunto un passaggio di autenticazione a doppio hop, nel quale le credenziali devono essere propagate dal client al server Web e al server Analysis Services back-end. Se si utilizzano le credenziali di Windows e NTLM, viene restituito un errore perché NTLM non consente la delega delle credenziali del client a un secondo server. La soluzione più comune consiste nell'utilizzare l'autenticazione di base con SSL (Secure Sockets Layer), ma ciò richiede che gli utenti forniscano un nome utente e una password al momento dell'accesso alla directory virtuale MSMDPUMP. Un approccio più diretto potrebbe consistere nell'abilitare Kerberos e configurare la delega vincolata di Analysis Services per consentire agli utenti di accedere ad Analysis Services in modo trasparente. Per altri dettagli, vedere [Configurare Analysis Services per la delega vincolata Kerberos](configure-analysis-services-for-kerberos-constrained-delegation.md).<br /><br /> Considerare quali porte sbloccare in Windows Firewall. Sarà necessario sbloccare le porte su entrambi i server per consentire l'accesso all'applicazione Web in IIS e ad Analysis Services in un server remoto.|  
|Origine delle connessioni client rappresentata da un dominio non attendibile o da una connessione Extranet|Le connessioni client con origine in un dominio non attendibile introducono ulteriori restrizioni relativamente all'autenticazione. Per impostazione predefinita, in Analysis Services viene utilizzata l'autenticazione integrata di Windows, per la quale è necessario che gli utenti si trovino nello stesso dominio del server. Agli eventuali utenti di una Extranet che eseguono la connessione a IIS dall'esterno del dominio verrà restituito un errore di connessione se il server è configurato per l'utilizzo delle impostazioni predefinite.<br /><br /> Le soluzioni alternative includono la possibilità, per gli utenti che si trovano in una Extranet, di eseguire la connessione tramite una rete VPN utilizzando le credenziali di dominio. Tuttavia, un approccio migliore potrebbe consistere nell'abilitare l'autenticazione di base e SSL nel sito Web IIS in uso.|  
  
##  <a name="bkmk_prereq"></a> Prerequisiti  
 Le istruzioni in questo articolo presuppongono che IIS sia già configurato e che sia già installato Analysis Services. Windows Server 2012 viene fornito con IIS 8.x come ruolo server che può essere abilitato nel sistema.  
  
 **Configurazione aggiuntiva in IIS 8.0**  
  
 Nella configurazione predefinita di IIS 8.0 mancano componenti necessari per l'accesso HTTP ad Analysis Services. Questi componenti, disponibili nelle aree funzionali **Sicurezza** e **Sviluppo di applicazioni** del ruolo **Server Web (IIS)** , sono i seguenti:  
  
-   **Sicurezza** | **Autenticazione Windows**o **Autenticazione di base**e qualsiasi altra funzionalità di sicurezza necessaria per lo scenario di accesso ai dati.  
  
-   **Sviluppo di applicazioni** | **CGI**  
  
-   **Sviluppo di applicazioni** | **Estensioni ISAPI**  
  
 Per verificare o aggiungere questi componenti, usare **Gestione server** | **Gestisci** | **Aggiungi ruoli e funzionalità**. Eseguire la procedura guidata fino a **Ruoli server**. Scorrere fino a **Server Web (IIS)**.  
  
1.  Aprire **Server Web** | **Sicurezza** e scegliere i metodi di autenticazione.  
  
2.  Aprire **Server Web** | **Sviluppo di applicazioni** e scegliere **CGI** ed **Estensioni ISAPI**.  
  
     ![Pagina Aggiungi funzionalità per il ruolo server Web](../media/ssas-httpaccess-isapicgi.png "pagina Aggiungi funzionalità per il ruolo server Web")  
  
 **Quando IIS è in un server remoto**  
  
 Una connessione remota tra IIS e Analysis Services richiede l'installazione del provider OLE DB per Analysis Services (MSOLAP) nel server Windows che esegue IIS.  
  
1.  Aprire la pagina di download per il [Feature Pack di SQL Server 2014](https://www.microsoft.com/download/details.aspx?id=42295)  
  
2.  Fare clic sul pulsante rosso Scarica.  
  
3.  Scorrere verso il basso fino a trovare ITA\x64\SQL_AS_OLEDB.msi  
  
4.  Per completare l'installazione, seguire le istruzioni della procedura guidata.  
  
> [!NOTE]  
>  Ricordarsi di sbloccare le porte in Windows Firewall per consentire le connessioni client a un server Analysis Services remoto. Per altre informazioni, vedere [Configure the Windows Firewall to Allow Analysis Services Access](configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
##  <a name="bkmk_copy"></a> Passaggio 1: Copiare i file MSMDPUMP in una cartella sul server Web  
 A ogni endpoint HTTP creato deve essere associato un proprio set di file MSMDPUMP. In questo passaggio si esegue la copia del file eseguibile MSMDPUMP, del file di configurazione e della cartella delle risorse dalle cartelle di programma di Analysis Services in una cartella della directory virtuale IIS che verrà creata nel file system del computer in cui è in esecuzione IIS.  
  
 È necessario formattare l'unità per il file system NTFS. Il percorso della cartella creata non deve contenere spazi.  
  
1.  Copiare i file seguenti, disponibili in \<unità >: \Programmi\Microsoft SQL Server\\< istanza\>\OLAP\bin\isapi: MSMDPUMP. DLL, MSMDPUMP. INI e una cartella Resources.  
  
     ![Esplora file con i file da copiare](../media/ssas-httpaccess-msmdpumpfilecopy.PNG "Esplora File con i file da copiare")  
  
2.  Nel server del web, creare una nuova cartella: \<unità >: \inetpub\wwwroot\\**OLAP**  
  
3.  Incollare i file copiati in precedenza in questa nuova cartella.  
  
4.  Verificare che nella cartella \inetpub\wwwroot\OLAP nel server web contiene quanto segue: MSMDPUMP. DLL, MSMDPUMP. INI e una cartella Resources. La struttura di cartelle dovrebbe essere simile alla seguente:  
  
    -   \<drive>:\inetpub\wwwroot\OLAP\MSMDPUMP.dll  
  
    -   \<drive>:\inetpub\wwwroot\OLAP\MSMDPUMP.ini  
  
    -   \<unità >: \inetpub\wwwroot\OLAP\Resources  
  
##  <a name="bkmk_appPool"></a> Passaggio 2: Creare un pool di applicazioni e una directory virtuale in IIS  
 Successivamente, creare un pool di applicazioni e un endpoint al data pump.  
  
#### <a name="create-an-application-pool"></a>Creare un pool di applicazioni  
  
1.  Avviare Gestione IIS.  
  
2.  Aprire la cartella del server, fare clic con il pulsante destro del mouse su **Pool di applicazioni** e scegliere **Aggiungi pool di applicazioni**. Creare un pool di applicazioni con il nome **OLAP**, usando .NET Framework, con Modalità pipeline gestita impostata su **Classica**.  
  
     ![Finestra di dialogo screenshot di Aggiungi Pool di applicazioni](../media/ssas-httpaccess.PNG "dialogo Screenshot di Aggiungi Pool di applicazioni")  
  
3.  Per impostazione predefinita, IIS crea pool di applicazioni usando **ApplicationPoolIdentity** come identità di sicurezza,una scelta valida per l'accesso HTTP ad Analysis Services. Se si hanno motivi specifici per modificare l'identità, fare clic con il pulsante destro su **OLAP**e scegliere **Impostazioni avanzate**. Selezionare **ApplicationPoolIdentity**. Fare clic sul pulsante **Cambia** di questa proprietà per sostituire l'account predefinito con quello personalizzato che si vuole usare.  
  
     ![Pagina delle proprietà Impostazioni cattura di schermata di Advanced](../media/ssas-httpaccess-advsettings.PNG "pagina delle proprietà Impostazioni cattura di schermata della avanzate")  
  
4.  Per impostazione predefinita, in un sistema operativo a 64 bit, tramite IIS la proprietà **Attiva applicazioni a 32 bit** viene impostata su **False**. Se il file msmdpump.dll è stato copiato da un'installazione a 64 bit di Analysis Services, questa è l'impostazione corretta per l'estensione MSMDPUMP in un server IIS a 64 bit. Se i file binari MSMDPUMP sono stati copiati da un'installazione a 32 bit, impostare su **True**. Controllare questa proprietà in **Impostazioni avanzate** per assicurarsi che sia impostata correttamente.  
  
#### <a name="create-an-application"></a>Creare un'applicazione  
  
1.  In Gestione IIS aprire **Siti**e selezionare **Sito Web predefinito**. Verrà visualizzata una cartella denominata **Olap**. Si tratta di un riferimento alla cartella OLAP creata in \inetpub\wwwroot.  
  
     ![Cartella OLAP nel sito web predefinito](../media/ssas-httpaccess-convertfolderbefore.png "cartella OLAP nel sito web predefinito")  
  
2.  Fare clic con il pulsante destro del mouse sulla cartella e scegliere **Converti in applicazione**.  
  
3.  In Aggiungi applicazione immettere **OLAP** per l'alias. Fare clic su **Seleziona** per scegliere il pool di applicazioni OLAP. Impostare l'opzione Percorso fisico su C:\inetpub\wwwroot\OLAP  
  
     ![Finestra di dialogo Aggiungi applicazione](../media/ssas-httpaccess-convertedapp.png "nella finestra di dialogo Aggiungi applicazione")  
  
4.  Fare clic su **OK**. Aggiornare il sito Web. La cartella OLAP è ora un'applicazione nel sito Web predefinito. A questo punto viene stabilito il percorso virtuale per il file MSMDPUMP.  
  
     ![Cartella OLAP dopo la conversione di app](../media/ssas-httpaccess-convertfolderafter.png "cartella OLAP dopo la conversione di app")  
  
> [!NOTE]  
>  Le versioni precedenti di queste istruzioni includevano i passaggi per la creazione di una directory virtuale. Tale passaggio non è più necessario.  
  
##  <a name="bkmk_auth"></a> Passaggio 3: Configurare l'autenticazione IIS e aggiungere l'estensione  
 In questo passaggio viene configurata ulteriormente la directory virtuale SSAS appena creata. Viene specificato un metodo di autenticazione e quindi aggiunto un mapping di script. Tra i metodi di autenticazione supportati per Analysis Services tramite HTTP sono inclusi:  
  
-   Autenticazione di Windows (Kerberos o NTLM)  
  
-   Autenticazione di base  
  
-   Autenticazione anonima  
  
 L'**autenticazione di Windows** è considerata la forma di autenticazione più sicura. Consente anche di usare l'infrastruttura esistente per le reti che impiegano Active Directory. Per utilizzare l'autenticazione di Windows in modo efficiente, tutti i browser e le applicazioni client e server devono supportarla. Si tratta della modalità più sicura e consigliata, per la quale è tuttavia necessario che IIS abbia accesso a un controller di dominio Windows in grado di autenticare l'identità dell'utente che richiede una connessione.  
  
 Per le topologie in cui Analysis Services e IIS vengono installati in computer diversi, sarà necessario risolvere i problemi di doppio hop che si verificano quando un'identità utente deve essere delegata a un secondo servizio in un computer remoto, in genere abilitando Analysis Services per la delega vincolata Kerberos. Per altre informazioni, vedere [Configure Analysis Services for Kerberos constrained delegation](configure-analysis-services-for-kerberos-constrained-delegation.md).  
  
 L'**autenticazione di base** viene usata in presenza di identità di Windows. Le connessioni utente hanno tuttavia origine da domini non attendibili, che non consentono l'uso di connessioni rappresentate o delegate. L'autenticazione di base consente di specificare un'identità utente e una password in una stringa di connessione. Anziché utilizzare il contesto di sicurezza dell'utente corrente, per effettuare la connessione ad Analysis Services vengono utilizzate le credenziali nella stringa di connessione. Poiché Analysis Services supporta solo l'autenticazione di Windows, tutte le credenziali che gli vengono passate devono rappresentare un utente o gruppo di Windows che sia un membro del dominio in cui Analysis Services è ospitato.  
  
 L'**autenticazione anonima** viene spesso usata durante il test iniziale, perché la relativa semplicità di configurazione consente di convalidare rapidamente la connettività HTTP ad Analysis Services. In soli pochi passaggi è possibile assegnare un account utente univoco come identità, concedere all'account le autorizzazioni in Analysis Services, utilizzare l'account per verificare l'accesso ai dati in un'applicazione client e infine disabilitare l'autenticazione anonima al completamento del test.  
  
 È anche possibile usare l'autenticazione anonima in un ambiente di produzione se gli utenti non dispongono di account utente di Windows, ma si attengono le procedure consigliate bloccando le autorizzazioni nel sistema host, come illustrato in questo articolo: [Abilitare l'autenticazione anonima (IIS 7)](https://technet.microsoft.com/library/cc731244\(v=ws.10\).aspx). Assicurarsi che l'autenticazione sia impostata nella directory virtuale e non nel sito Web padre, per ridurre ulteriormente il livello di accesso dell'account.  
  
 Quando è abilitata l'autenticazione anonima, la connessione come utente anonimo è consentita per qualsiasi connessione utente all'endpoint HTTP. Sarà in grado di controllare le connessioni di singolo utente, né utilizzare l'identità dell'utente per selezionare i dati da un modello. Come è possibile vedere, l'utilizzo dell'autenticazione anonima ha impatto su vari aspetti, dalla progettazione dei modelli, all'aggiornamento dei dati e all'accesso a questi ultimi. Tuttavia, se gli utenti non dispongono di un account di accesso di Windows con cui iniziare, è possibile che l'unica opzione disponibile sia l'account anonimo.  
  
#### <a name="set-the-authentication-type-and-add-a-script-map"></a>Impostare il tipo di autenticazione e aggiungere un mapping di script  
  
1.  In Gestione IIS aprire **Siti**, selezionare **Sito Web predefinito**e scegliere la directory virtuale **OLAP** .  
  
2.  Fare doppio clic su **Autenticazione** nella sezione IIS della pagina principale.  
  
     ![Pagina principale della schermata di gestione IIS](../media/ssas-httpaccess-iis.png "pagina principale della schermata di gestione IIS")  
  
3.  Se si usa la sicurezza integrata di Windows, abilitare **Autenticazione Windows** .  
  
     ![Le impostazioni di autenticazione della schermata di Vdir](../media/ssas-httpaccess-iisauth.png "impostazioni Screenshot di autenticazione della directory virtuale")  
  
4.  In alternativa, abilitare **Autenticazione di base** se le applicazioni client e server in uso si trovano in domini diversi. Per poter utilizzare questa modalità, l'utente dovrà immettere un nome utente e una password. Il nome utente e la password vengono trasmessi a IIS mediante connessione HTTP. Tramite IIS si tenterà di rappresentare l'utente che utilizza le credenziali specificate durante la connessione a MSMDPUMP, ma le credenziali in questione non verranno delegate ad Analysis Services. Sarà invece necessario passare un nome utente e una password validi in una connessione, come descritto nel Passaggio 6 del presente documento.  
  
    > [!IMPORTANT]  
    >  Si noti che chiunque compili un sistema in cui viene trasmessa la password deve disporre di modalità per la sicurezza del canale di comunicazione. In IIS è disponibile un set di strumenti che consente di proteggere il canale. Per altre informazioni, vedere [Enable Anonymous Authentication (IIS 7)](https://go.microsoft.com/fwlink/?LinkId=207562) (Abilitare l'Autenticazione anonima (IIS 7).  
  
5.  Disabilitare **Autenticazione anonima** se si usa l'autenticazione di Windows o di base. Quando abilitata, l'autenticazione anonima viene sempre utilizzata per prima in IIS, persino se si abilitano altri metodi di autenticazione.  
  
     Con l'autenticazione anonima, il data pump (msmdpump.dll) viene eseguito come account utente stabilito per l'utente anonimo. Non esiste alcuna distinzione tra l'utente connesso a IIS e quello connesso ad Analysis Services. Per impostazione predefinita, in IIS viene utilizzato l'account IUSR, ma è possibile impostarlo su un account utente di dominio con autorizzazioni di rete. Questa funzionalità è necessario se IIS e Analysis Services si trovano in computer diversi.  
  
     Per istruzioni su come configurare le credenziali per l'autenticazione anonima, vedere [Anonymous Authentication](http://www.iis.net/configreference/system.webserver/security/authentication/anonymousauthentication)(Autenticazione anonima).  
  
    > [!IMPORTANT]  
    >  L'autenticazione anonima risulta disponibile con maggiore probabilità in un ambiente estremamente controllato, in cui l'accesso viene concesso o negato in base agli elenchi di controllo di accesso nel file system. Per le procedure consigliate, vedere [Enable Anonymous Authentication (IIS 7)](https://technet.microsoft.com/library/cc731244\(v=ws.10\).aspx) (Abilitare l'Autenticazione anonima (IIS 7).  
  
6.  Fare clic sulla directory virtuale **OLAP** per aprire la pagina principale. Fare doppio clic su **Mapping gestori**.  
  
     ![Icona del mapping gestori nella pagina della funzionalità](../media/ssas-httpaccess-handlermapping.png "icona del mapping gestori nella pagina della funzionalità")  
  
7.  Fare clic con il pulsante destro del mouse in un punto qualsiasi della pagina e selezionare **Aggiungi mapping di script**. Nella finestra di dialogo Aggiungi mapping di script specificare **\*.dll** come percorso della richiesta e c:\inetpub\wwwroot\OLAP\msmdpump.dll come file eseguibile e digitare **OLAP** come nome. Mantenere tutte le restrizioni predefinite associate a questo mapping di script.  
  
     ![Finestra di dialogo screenshot di Aggiungi mapping di Script](../media/ssas-httpaccess-addscript.png "nella finestra di dialogo Screenshot di Aggiungi mapping di Script")  
  
8.  Alla richiesta di consentire l'estensione ISAPI, fare clic su **Sì**.  
  
     ![Schermata di conferma per aggiungere l'estensione ISAPI](../media/ssas-httpaccess-isapiprompt.png "schermata di conferma per aggiungere l'estensione ISAPI")  
  
##  <a name="bkmk_edit"></a> Passaggio 4: Modificare il file MSMDPUMP.INI per impostare il server di destinazione  
 Nel file MSMDPUMP.INI viene specificata l'istanza di Analysis Services a cui MSMDPUMP.DLL effettua la connessione. Questa istanza può essere locale o remota, installata come quella predefinita o come istanza denominata.  
  
 Aprire il file msmdpump.ini posizionato nella cartella C:\inetpub\wwwroot\OLAP ed esaminare il relativo contenuto. Il risultato sarà simile al seguente:  
  
```  
<ConfigurationSettings>  
<ServerName>localhost</ServerName>  
<SessionTimeout>3600</SessionTimeout>  
<ConnectionPoolSize>100</ConnectionPoolSize>  
</ConfigurationSettings>  
  
```  
  
 Se l'istanza di Analysis Services per la quale si configura l'accesso HTTP si trova sul computer locale e viene installata come predefinita, non esiste alcun motivo per modificare questa impostazione. In caso contrario, è necessario specificare il nome del server (ad esempio, \<ServerName > ADWRKS-SRV01\TABULAR</ServerName-SRV01\</ServerName >). Per un server che viene installato come istanza denominata, assicurarsi di aggiungere il nome dell'istanza (ad esempio, \<ServerName > ADWRKS-SRV01\TABULAR</ServerName SRV01\Tabular\</ServerName >).  
  
 Per impostazione predefinita, Analysis Services è in ascolto sulla porta TCP/IP 2383. Se Analysis Services è installato come istanza predefinita, non è necessario specificare alcuna porta in \<ServerName > perché Analysis Services in grado di restare in ascolto automaticamente sulla porta 2383. Tuttavia, è necessario consentire connessioni in ingresso per tale porta in Windows Firewall. Per altre informazioni, vedere [Configure the Windows Firewall to Allow Analysis Services Access](configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
 Se è stato configurato un oggetto denominato o predefinito di istanza di Analysis Services in ascolto su una porta fissa, è necessario aggiungere il numero di porta al nome del server (ad esempio, \<ServerName > AW-lt;nomeserver>AW-Srv01:55555</nomeserver&gt\</ServerName >) ed è necessario consentire in ingresso connessioni a tale porta nel Firewall di Windows.  
  
## <a name="step-5-grant-data-access-permissions"></a>Passaggio 5: Concedere le autorizzazioni di accesso  
 Come indicato in precedenza, sarà necessario concedere le autorizzazioni nell'istanza di Analysis Services. A ogni oggetto di database verranno assegnati ruoli mediante i quali viene fornito un livello specificato di autorizzazioni (lettura o lettura/scrittura) e ogni ruolo disporrà di membri costituiti da identità utente di Windows.  
  
 Per impostare le autorizzazioni è possibile utilizzare SQL Server Management Studio. Nella cartella **Database** | **Ruoli** è possibile creare ruoli, specificare le autorizzazioni del database, assegnare l'appartenenza agli account utente e di gruppo Windows, nonché concedere le autorizzazioni di lettura o scrittura per oggetti specifici. In genere, le autorizzazioni di **lettura** per un cubo sono sufficienti per le connessioni client, mediante le quali vengono usati, ma non aggiornati, i dati del modello.  
  
 L'assegnazione dei ruoli varia a seconda della modalità con cui è stata configurata l'autenticazione.  
  
|||  
|-|-|  
|Anonima|Aggiungere all'elenco Appartenenza l'account specificato in **Modifica credenziali di autenticazione anonima** in IIS. Per altre informazioni, vedere [Anonymous Authentication](http://www.iis.net/configreference/system.webserver/security/authentication/anonymousauthentication)(Autenticazione anonima).|  
|Autenticazione Windows|Aggiungere all'elenco Appartenenza gli account di gruppo o utente di Windows che richiedono i dati di Analysis Services mediante la rappresentazione o la delega.<br /><br /> Supponendo che venga utilizzata la delega vincolata Kerberos, gli unici account che richiedono le autorizzazioni sono gli account di gruppo e l'utente di Windows che richiedono l'accesso. Nessuna autorizzazione è necessaria per l'identità del pool di applicazioni.|  
|Autenticazione di base|Aggiungere all'elenco Appartenenza gli account di gruppo o utente di Windows che vengono passati nella stringa di connessione.<br /><br /> Inoltre, se si passano le credenziali tramite `EffectiveUserName` nella stringa di connessione, l'identità del pool di applicazioni deve disporre dei diritti di amministratore sull'istanza di Analysis Services. In SSMS, fare doppio clic sull'istanza di &#124; **delle proprietà** &#124; **sicurezza** &#124; **Add**. Immettere l'identità del pool di applicazioni. Se è stata usata l'identità predefinita incorporata, l'account viene specificato come **IIS AppPool\DefaultAppPool**.<br /><br /> ![](../media/ssas-httpaccess-iisapppoolidentity.png)|  
  
 Per altre informazioni, vedere [Autorizzazione dell'accesso a oggetti e operazioni &#40;Analysis Services&#41;](../multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)(Autenticazione a Microsoft BI e delega d'identità).  
  
##  <a name="bkmk_test"></a> Passaggio 6: Testare la configurazione  
 La sintassi della stringa di connessione per MSMDPUMP è l'URL del MSMDPUMP.dll.  
  
 Se l'applicazione web è in ascolto su una porta fissa, aggiungere il numero di porta per il nome del server o l'indirizzo IP (ad esempio, http://my-web-srv01:8080/OLAP/msmdpump.dll o http://123.456.789.012:8080/OLAP/msmdpump.dll.  
  
 Per testare la connessione in modo rapido, è possibile aprirne una usando Microsoft Excel o SQL Server Management Studio  
  
 **Verificare le connessioni tramite SQL Server Management Studio**  
  
1.  Nella finestra di dialogo Connetti al server di Management Studio selezionare **Analysis Services** come tipo di server. In Nome server immettere l'indirizzo HTTP dell'estensione msmdpump: `http://my-web-srv01/OLAP/msmdpump.dll`.  
  
     Esplora oggetti consente di visualizzare la connessione HTTP:  
  
     ![Visualizza la connessione http a SSAS di Esplora oggetti](../media/ssas-httpaccess-ssms.PNG "Esplora oggetti Visualizza la connessione http a SSAS")  
  
2.  L'autenticazione deve essere quella di Windows e l'utente che utilizza Management Studio deve essere un amministratore di Analysis Services. Un amministratore può concedere ulteriori autorizzazioni per consentire l'accesso di altri utenti.  
  
 **Verificare le connessioni tramite Excel**  
  
1.  In Carica dati esterni della scheda Dati in Excel fare clic su **Da altre origini**e scegliere **Da Analysis Services** per avviare la Connessione dati guidata.  
  
2.  In Nome server immettere l'indirizzo HTTP dell'estensione msmdpump: `http://my-web-srv01/OLAP/msmdpump.dll`.  
  
3.  Per le credenziali di accesso, selezionare **Usa autenticazione di Windows** , se si usa la sicurezza integrata di Windows o l'autenticazione NTLM o un utente anonimo.  
  
     Per l'autenticazione di base, scegliere **Usa nome utente e password seguenti**e specificare le credenziali usate per l'accesso. Le credenziali immesse verranno passate nella stringa di connessione ad Analysis Services.  
  
 **Verificare le connessioni tramite AMO**  
  
 È possibile verificare l'accesso HTTP a livello di codice tramite AMO, sostituendo l'URL dell'endpoint per il nome del server. Per informazioni dettagliate, vedere il [post del forum relativo alla modalità di sincronizzazione di database di SSAS 2008 R2 tramite HTTPS nei limiti di dominio, foresta e firewall](http://social.msdn.microsoft.com/Forums/en/sqlanalysisservices/thread/c4249d55-914d-4c81-9980-44d0b8df9c3e).  
  
 Di seguito è riportata una stringa di connessione di esempio che illustra la sintassi per l'accesso HTTP(S) tramite l'autenticazione di base:  
  
 `Data Source=https://<servername>/olap/msmdpump.dll; Initial Catalog=AdventureWorksDW2012; Integrated Security=Basic; User ID=XXXX; Password=XXXXX;`  
  
 Per altre informazioni sulla connessione a livello di programmazione, vedere [Implementazione di connessioni protette in ADOMD.NET](https://docs.microsoft.com/bi-reference/adomd/multidimensional-models-adomd-net-client/connections-in-adomd-net-establishing-secure-connections).  
  
 Come passaggio finale, accertarsi di eseguire successivamente un test più rigido utilizzando un computer client in esecuzione nell'ambiente di rete dal quale hanno origine le connessioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Post del forum (accesso http tramite msmdpump e autenticazione di base)](http://social.msdn.microsoft.com/Forums/en/sqlanalysisservices/thread/79d2f225-df35-46da-aa22-d06e98f7d658)   
 [Configure the Windows Firewall to Allow Analysis Services Access](configure-the-windows-firewall-to-allow-analysis-services-access.md)   
 [Autorizzazione dell'accesso a oggetti e operazioni &#40;Analysis Services&#41;](../multidimensional-models/authorizing-access-to-objects-and-operations-analysis-services.md)   
 [Metodi di autenticazione IIS](https://go.microsoft.com/fwlink/?LinkdID=208461)   
 [Enable Anonymous Authentication (IIS 7)](https://go.microsoft.com/fwlink/?LinkId=207562)  
  
  
