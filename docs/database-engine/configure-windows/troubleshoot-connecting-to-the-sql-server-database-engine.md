---
title: Risolvere i problemi di connessione al motore di database di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 02/07/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- troubleshooting, connecting to Database Engine
- connecting to Database Engine, troubleshooting
ms.assetid: 474c365b-c451-4b07-b636-1653439f4b1f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: d70a08ac868aa28a38f3e32a9fb32024bc345193
ms.sourcegitcommit: 96032813f6bf1cba680b5e46d82ae1f0f2da3d11
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/15/2019
ms.locfileid: "54300468"
---
# <a name="troubleshoot-connecting-to-the-sql-server-database-engine"></a>Risolvere i problemi di connessione al motore di database di SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]


  > [!div class="nextstepaction"]
  > [Condividi il feedback sul sommario della documentazione SQL](https://aka.ms/sqldocsurvey)

Di seguito sono elencate tutte le tecniche di risoluzione dei problemi che è possibile usare quando non è possibile connettersi al motore di database di SQL Server. I passaggi non seguono l'ordine dei problemi più frequenti dei quali probabilmente sono già stati tentati i passaggi. I passaggi seguono invece un ordine basato sulla complessità, dai problemi di base ai problemi più complessi. Nei passaggi si presuppone che la connessione a SQL Server venga stabilita da un altro computer usando il protocollo TCP/IP, che è la situazione più comune. I passaggi sono stati scritti per SQL Server 2016 con SQL Server e le applicazioni client che eseguono Windows 10. I passaggi tuttavia si applicano in genere alle altre versioni di SQL Server e ad altri sistemi operativi con leggere differenze.

Le istruzioni specificate risultano particolarmente utili per la risoluzione dell'errore "**Connect to Server**"(Connessione al server) con numero di errore: 11001 o 53, gravità: 20, stato: 0 e di messaggi di errore quali:

*   "Si è verificato un errore di rete o specifico dell'istanza mentre si cercava di stabilire una connessione con SQL Server. Server non trovato o non accessibile. Verificare che il nome dell'istanza sia corretto e che il server sia configurato in modo da consentire connessioni remote. " 

*   "(provider: Provider named pipe, errore: 40 - Non è stato possibile aprire una connessione a SQL Server) (Microsoft SQL Server, errore: 53)" oppure "(provider: provider TCP, errore: 0 - No such host is known.) (Host sconosciuto) (Microsoft SQL Server, errore: 11001)" 

Questo errore indica in genere che non è possibile trovare il computer SQL Server o che il numero di porta TCP non è noto, non è corretto o è bloccato da un firewall.

> [!TIP]
>  Una pagina di risoluzione interattiva è disponibile dal Supporto Tecnico Microsoft [!INCLUDE[msCoName_md](../../includes/msconame-md.md)] in [Risoluzionedei problemi di connettività a SQL Server](https://support.microsoft.com/help/4009936/solving-connectivity-errors-to-sql-server).

### <a name="not-included"></a>Errori non inclusi

* In questo argomento non vengono fornite informazioni sugli errori SSPI. Per gli errori SSPI, vedere [Risoluzione del messaggio di errore "Impossibile generare il contesto SSPI"](https://support.microsoft.com/kb/811889).  
* In questo argomento non vengono fornite informazioni sugli errori Kerberos. Per altre informazioni, vedere [Microsoft Kerberos Configuration Manager per SQL Server](https://www.microsoft.com/download/details.aspx?id=39046).
* In questo argomento non vengono fornite informazioni sulla connettività SQL di Azure. Per altre informazioni, vedere [Risoluzione dei problemi di connettività al database SQL di Microsoft Azure](https://support.microsoft.com/help/10085/troubleshooting-connectivity-issues-with-microsoft-azure-sql-database). 

## <a name="gathering-information-about-the-instance-of-sql-server"></a>Raccolta di informazioni sull'istanza di SQL Server

È necessario innanzitutto raccogliere le informazioni di base sul motore di database.

1. Verificare che l'istanza del motore di database di SQL Server sia installata e in esecuzione.
    1.  Accedere al computer che ospita l'istanza di SQL Server.
    2.  Avviare Gestione configurazione SQL Server. Gestione configurazione viene installata automaticamente nel computer durante l'installazione di SQL Server. Le istruzioni per l'avvio di Gestione configurazione variano leggermente a seconda della versione di SQL Server e Windows. Per informazioni sull'avvio di Gestione configurazione, vedere [Gestione configurazione SQL Server](../../relational-databases/sql-server-configuration-manager.md).
    3.  In Gestione configurazione nel riquadro sinistro selezionare **Servizi di SQL Server**. Nel riquadro destro verificare che l'istanza del motore di database sia presente e in esecuzione. Un'istanza denominata **SQL Server (MSSQLSERVER)** è un'istanza predefinita (senza nome). Può essere presente una sola istanza predefinita. I nomi delle altre istanze con nome sono indicati tra parentesi. SQL Server Express usa il nome **SQL Server (SQLEXPRESS)** come nome di istanza se non viene specificato un nome diverso durante l'installazione. Prendere nota del nome dell'istanza a cui si sta tentando di connettersi. Verificare inoltre che l'istanza sia in esecuzione cercando la freccia verde. Se l'istanza è contrassegnata con un quadrato rosso, fare clic con il pulsante destro del mouse sull'istanza e quindi fare clic su **Avvia**. L'istanza verrà contrassegnata in verde.
     4. Se si sta tentando di connettersi a un'istanza denominata, assicurarsi che il servizio SQL Server Browser sia in esecuzione.
 

2.  Ottenere l'indirizzo IP del computer.
    1. Nel menu Start fare clic su **Esegui**. Nella finestra **Esegui** digitare **cmd**e quindi fare clic su **OK**.
    2.  Nella finestra del prompt dei comandi digitare **ipconfig** e quindi premere INVIO. Prendere nota dell'indirizzo **IPv4** e dell'indirizzo **IPv6** . SQL Server è in grado di stabilire la connessione usando la versione 4 del protocollo IP o la nuova versione 6 del protocollo IP. È possibile che la rete supporti uno dei due protocolli o entrambi. Nella maggior parte dei casi la risoluzione dei problemi viene iniziata con l'indirizzo **IPv4** . che risulta più breve e facile da digitare.


3.  Ottenere il numero di porta TCP usato da SQL Server. Nella maggior parte dei casi si stabilisce la connessione al motore di database da un altro computer usando il protocollo TCP.
    1.  Usando SQL Server Management Studio nel computer che esegue SQL Server, connettersi all'istanza di SQL Server. In Esplora oggetti espandere **Gestione**, espandere **Log di SQL Server**e fare doppio clic sul log corrente.
    2.  Nel Visualizzatore log fare clic sul pulsante **Filtro** sulla barra degli strumenti. Nella casella **Testo contenuto nel messaggio** digitare **Il server è in attesa su**, fare clic su **Applica filtro**e quindi fare clic su **OK**.
    3.  Viene visualizzato un messaggio simile a **Il server è in attesa su [ 'qualsiasi' \<ipv4> 1433]**. Questo messaggio indica che l'istanza di SQL Server è in attesa su tutti gli indirizzi IP nel computer in uso (per la versione IP 4) ed è in attesa sulla porta TCP 1433. La porta TCP 1433 è in genere la porta usata dal motore di database. Poiché una porta può essere usata da una sola istanza di SQL Server, in presenza di più istanze di SQL Server installate è necessario che alcune istanze usino altri numeri di porta. Prendere nota del numero di porta usato dall'istanza di [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] a cui si sta cercando di connettersi. 

    > [!NOTE] 
    > Verrà probabilmente indicato l'indirizzo IP 127.0.0.1. Si tratta dell'indirizzo della scheda di loopback cui è possibile connettersi soltanto da processi nello stesso computer. Può essere utile per la risoluzione dei problemi, ma non può essere usato per la connessione da un altro computer.

## <a name="enable-protocols"></a>Abilitare i protocolli

In alcune installazioni di SQL Server la connessione al motore di database da un altro computer non è abilitata, a meno che non venga abilitata da un amministratore usando Gestione configurazione. Per abilitare le connessioni da un altro computer:

1.  Aprire Gestione configurazione SQL Server come descritto sopra. 
2.  In Gestione configurazione nel riquadro sinistro espandere **Configurazione di rete SQL Server**e quindi selezionare l'istanza di SQL Server a cui si vuole connettersi. Nel riquadro destro sono elencati i protocolli di connessione disponibili. Il protocollo Shared Memory è in genere abilitato. Poiché può essere usato solo dallo stesso computer, il protocollo Shared Memory è abilitato nella maggior parte delle installazioni. La connessione a SQL Server da un altro computer avviene in genere tramite TCP/IP. Se TCP/IP non è abilitato, fare clic con il pulsante destro del mouse su **TCP/IP**e quindi fare clic su **Abilita**. 
3.  Se si modifica l'impostazione di abilitazione per un protocollo, è necessario riavviare il motore di database. Nel riquadro sinistro selezionare **Servizi di SQL Server**. Nel riquadro destro fare clic con il pulsante destro del mouse sull'istanza del motore di database e quindi fare clic su **Riavvia**. 

## <a name="testing-tcpip-connectivity"></a>Test della connettività TCP/IP

Per connettersi a SQL Server tramite TCP/IP è necessario che Windows sia in grado di stabilire la connessione. Usare lo strumento `ping` per testare la connettività TCP.
1.  Nel menu Start fare clic su **Esegui**. Nella finestra **Esegui** digitare **cmd**e quindi fare clic su **OK**. 
2.  Nella finestra del prompt dei comandi digitare `ping` e quindi l'indirizzo IP del computer che esegue SQL Server. Ad esempio, usare `ping 192.168.1.101` con un indirizzo IPv4 oppure usare `ping fe80::d51d:5ab5:6f09:8f48%11` con un indirizzo IPv6. Sostituire i numeri dopo il comando ping con gli indirizzi IP nel computer raccolti in precedenza. 
3.  Se la rete è configurata correttamente, si riceverà una **Risposta da \<indirizzo IP>** seguita da informazioni aggiuntive. Se si riceve un errore, ad esempio **Host di destinazione non raggiungibile** o **Timeout della richiesta**, significa che la connettività TCP/IP non è stata configurata correttamente. Verificare che l'indirizzo IP sia corretto e digitato correttamente. Gli errori di questo tipo potrebbero indicare un problema del computer client, del computer server o di un componente della rete, ad esempio un router. In Internet sono disponibili diverse risorse per la risoluzione dei problemi della connessione TCP/IP. È possibile ad esempio iniziare con l'articolo del 2006 [How to Troubleshoot Basic TCP/IP Problems](https://support.microsoft.com/kb/169790)(Come risolvere i problemi di base TCP/IP).
4.  Successivamente, se il test di ping ha esito positivo usando l'indirizzo IP, verificare che il nome del computer possa essere risolto nell'indirizzo TCP/IP. Nella finestra del prompt dei comandi nel computer client digitare `ping` seguito dal nome del computer che esegue SQL Server. Ad esempio, usare `ping newofficepc` 
5.  Se è stato possibile effettuare il ping dell'indirizzo IP, ma successivamente viene visualizzato un errore, come **Host di destinazione non raggiungibile** o **Timeout della richiesta**, è possibile che siano presenti informazioni di risoluzione dei nomi non aggiornate memorizzate nella cache del computer client. Digitare `ipconfig /flushdns` per cancellare la cache DNS (Dynamic Name Resolution). Quindi eseguire nuovamente il ping del computer per nome. Con la cache DNS vuota, il computer client cercherà le informazioni più recenti sull'indirizzo IP del computer server. 
6.  Se la rete è configurata correttamente, si riceverà una **Risposta da \<indirizzo IP>** seguita da informazioni aggiuntive. Se il ping del computer server con l'indirizzo IP ha esito positivo ma si riceve un errore, ad esempio **Host di destinazione non raggiungibile** o **Timeout della richiesta**, quando si esegue il ping con il nome del computer, significa che la risoluzione dei nomi non è configurata correttamente. Per altre informazioni, vedere l'articolo del 2006 indicato in precedenza [How to Troubleshoot Basic TCP/IP Problems](https://support.microsoft.com/kb/169790) (Come risolvere i problemi di base TCP/IP). Poiché la risoluzione dei nomi non è necessaria per connettersi a SQL Server, se il nome del computer non può essere risolto in un indirizzo IP, è necessario stabilire le connessioni specificando l'indirizzo IP. Sebbene non sia la soluzione ideale, la risoluzione dei nomi può essere corretta in seguito.
  
  
## <a name="testing-a-local-connection"></a>Test di una connessione locale

Prima di risolvere un problema di connessione da un altro computer, verificare innanzitutto la possibilità di connettersi da un'applicazione client installata nel computer che esegue SQL Server. In questo modo sarà possibile evitare i problemi del firewall. In questa procedura viene usato SQL Server Management Studio. Se Management Studio non è installato, vedere [Scaricare SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md). Se non si è in grado di installare Management Studio, è possibile testare la connessione usando l'utilità `sqlcmd.exe` che viene installata con il motore di database. Per altre informazioni su `sqlcmd.exe`, vedere [Utilità sqlcmd](../../tools/sqlcmd-utility.md).
1.  Accedere al computer in cui è installato SQL Server usando un account che dispone dell'autorizzazione per accedere a SQL Server. Durante l'installazione, SQL Server richiede almeno un accesso come amministratore di SQL Server. Se non si conosce un amministratore, vedere [Connettersi a SQL Server se gli amministratori di sistema sono bloccati](connect-to-sql-server-when-system-administrators-are-locked-out.md).
2.   Nella pagina iniziale digitare **SQL Server Management Studio**oppure nelle versioni precedenti di Windows nel menu Start scegliere **Tutti i programmi**, quindi scegliere **Microsoft SQL Server**e fare clic su **SQL Server Management Studio**.
3.  Nella finestra di dialogo **Connetti al server** selezionare **Motore di database** nella casella **Tipo di server**. Nella casella **Autenticazione** selezionare **Autenticazione di Windows**. Nella casella **Nome server** digitare una delle opzioni seguenti:

|Connessione a:|Tipo:|Esempio:|
|-----------------|---------------|-----------------|
|Istanza predefinita|Nome del computer|ACCNT27|
|Istanza denominata|Nome del computer\nome dell'istanza|ACCNT27\PAYROLL|

> [!NOTE]
>  Per la connessione a SQL Server da un'applicazione client nello stesso computer viene usato il protocollo Shared Memory. Poiché Shared Memory è un tipo di named pipe locale, a volte si verificano errori relativi alle pipe.

Se si verifica un errore in questa fase, è necessario risolverlo prima di procedere. Possono verificarsi diversi tipi di problemi. È possibile che l'account di accesso non sia autorizzato a connettersi. Il database predefinito potrebbe non essere disponibile.

> [!NOTE]
>    Alcuni messaggi di errore passati al client non forniscano intenzionalmente informazioni sufficienti per risolvere il problema. Si tratta di una misura di sicurezza per evitare di fornire informazioni su SQL Server a un utente malintenzionato. Per visualizzare informazioni complete sull'errore, esaminare il log degli errori di SQL Server. Il log contiene informazioni dettagliate. Se si verifica l'errore **18456 L'accesso non è riuscito per l'utente**, vedere l'argomento [MSSQLSERVER_18456](../../relational-databases/errors-events/mssqlserver-18456-database-engine-error.md) della documentazione online che include informazioni aggiuntive sui codici di errore. Un blog di Aaron Bertrand include un elenco completo dei codici di errore in [Troubleshooting Error 18456](https://www2.sqlblog.com/blogs/aaron_bertrand/archive/2011/01/14/sql-server-v-next-denali-additional-states-for-error-18456.aspx)(Risoluzione dell'errore 18456). Se si è in grado di stabilire la connessione, è possibile visualizzare il log degli errori con SSMS nella sezione Gestione di Esplora oggetti. In caso contrario, è possibile visualizzare il log degli errori con il Blocco note di Windows. Il percorso predefinito varia in base alla versione e può essere modificato durante l'installazione. Il percorso predefinito per [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] è `C:\Program Files\Microsoft SQL Server\MSSQL13.MSSQLSERVER\MSSQL\Log\ERRORLOG`.  

4.   Se è possibile connettersi tramite Shared Memory, testare la connessione usando TCP. È possibile forzare una connessione TCP specificando **tcp:** prima del nome. Ad esempio

|Connessione a:|Tipo:|Esempio:|
|-----------------|---------------|-----------------|
|Istanza predefinita|tcp: Nome del computer|tcp:ACCNT27|
|Istanza denominata|tcp: Nome del computer/nome dell'istanza|tcp:ACCNT27\PAYROLL|
  
Se è possibile connettersi con Shared Memory e non con TCP, è necessario correggere il problema TCP. La causa più probabile è che TCP non sia abilitato. Per abilitare TCP, vedere i passaggi descritti sopra in **Abilitare i protocolli** .

5.   Quando è possibile connettersi come amministratore, se si vuole stabilire la connessione con un account diverso dall'account di amministratore, provare a connettersi usando l'account di accesso con autenticazione di Windows o l'account di accesso con autenticazione di SQL Server dell'applicazione client.

## <a name="opening-a-port-in-the-firewall"></a>Apertura di una porta nel firewall

Da diversi anni, a partire da Windows XP Service Pack 2, è abilitato Windows Firewall che blocca le connessioni da altri computer. Per connettersi tramite TCP/IP da un altro computer, è necessario configurare il firewall nel computer SQL Server per consentire le connessioni alla porta TCP usata dal motore di database. Come accennato in precedenza, l'istanza predefinita è in genere in ascolto sulla porta TCP 1433. Se ci sono istanze denominate o se l'istanza predefinita è stata modificata, la porta TCP di [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] potrebbe essere in ascolto su un'altra porta. Vedere la sezione iniziale relativa alla raccolta di informazioni per determinare la porta.  
Se si stabilisce la connessione a un'istanza denominata o a una porta diversa dalla porta TCP 1433, è necessario aprire anche la porta UDP 1434 per il servizio SQL Server Browser. Per istruzioni dettagliate sull'apertura di una porta in Windows Firewall, vedere [Configurazione di Windows Firewall per l'accesso al Motore di database](configure-a-windows-firewall-for-database-engine-access.md).

## <a name="testing-the-connection"></a>Test della connessione

Quando è possibile connettersi tramite TCP nello stesso computer, provare a connettersi dal computer client. Sebbene sia in teoria possibile usare qualsiasi applicazione client, per evitare complessità è consigliabile installare gli strumenti di gestione di SQL Server nel client ed eseguire il tentativo usando SQL Server Management Studio.

1. Nel computer client usare SQL Server Management Studio per tentare di connettersi con l'indirizzo IP e il numero di porta TCP nel formato indirizzo IP virgola numero di porta. Ad esempio, **192.168.1.101,1433** Se non funziona, è probabile che si sia verificato uno dei problemi seguenti:

    * Il**ping** dell'indirizzo IP non funziona e indica un problema di configurazione TCP generale. Tornare alla sezione **Test della connettività TCP/IP**. 
    *   SQL Server non è in attesa sul protocollo TCP. Tornare alla sezione **Abilitare i protocolli**. 
    *   SQL Server è in attesa su una porta diversa da quella specificata. Tornare alla sezione **Raccolta di informazioni sull'istanza di SQL Server**. 
    *   La porta TCP di SQL Server è bloccata dal firewall. Tornare alla sezione **Apertura di una porta nel firewall**.


2. Quando è possibile connettersi usando l'indirizzo IP e il numero di porta, tentare di connettersi usando l'indirizzo IP senza un numero di porta. Per un'istanza predefinita, è sufficiente usare l'indirizzo IP. Per un'istanza denominata, usare l'indirizzo IP e il nome dell'istanza nel formato IP indirizzo barra rovesciata nome dell'istanza, ad esempio **192.168.1.101\PAYROLL** Se non funziona, è probabile che si sia verificato uno dei problemi seguenti:

    *   Se ci si connette all'istanza predefinita, è possibile che l'istanza sia in attesa su una porta diversa dalla porta TCP 1433 e che il client non stia tentando di connettersi al numero di porta corretto.
    *   Se ci si connette a un'istanza denominata, il numero di porta non viene restituito al client.  

Entrambi questi problemi sono correlati al servizio SQL Server Browser che indica il numero di porta al client. Le soluzioni sono:

  * Avviare il servizio SQL Server Browser. Tornare a **Raccolta di informazioni sull'istanza di SQL Server**, sezione 1.d.
  * Il servizio SQL Server Browser è bloccato dal firewall. Aprire la porta UDP 1434 nel firewall. Tornare alla sezione **Apertura di una porta nel firewall**. Assicurarsi di aprire una porta UDP e non TCP. Si tratta di porte diverse.
  * Le informazioni sulla porta UDP 1434 sono bloccate da un router. La comunicazione UDP (User Datagram Protocol) non è progettata per passare tramite router. In questo modo la rete viene occupata da traffico con priorità bassa. Dovrebbe essere possibile configurare il router per l'inoltro del traffico UDP oppure è possibile decidere di comunicare sempre il numero di porta quando si stabilisce la connessione.
  * Se il computer client usa Windows 7, Windows Server 2008 o un sistema operativo più recente, è possibile che il traffico UDP venga eliminato dal sistema operativo client poiché la risposta del server viene restituita da un indirizzo IP diverso da quello richiesto. Si tratta di una misura di sicurezza che blocca il "loose source mapping". Per altre informazioni, vedere la sezione **Più indirizzi IP del server** dell'argomento della documentazione online [Risoluzione dei problemi: Timeout scaduto](https://msdn.microsoft.com/library/ms190181.aspx). Sebbene si tratti di un articolo relativo a SQL Server 2008 R2, le nozioni fornite sono ancora valide. Dovrebbe essere possibile configurare il client in modo che venga usato l'indirizzo IP corretto oppure è possibile decidere di comunicare sempre il numero di porta quando si stabilisce la connessione.
     
3. Quando è possibile connettersi usando l'indirizzo IP o l'indirizzo IP e il nome dell'istanza per un'istanza denominata, provare a connettersi usando il nome del computer o il nome del computer e il nome dell'istanza per un'istanza denominata. Inserire `tcp:` prima del nome del computer per forzare una connessione TCP/IP. Ad esempio, per l'istanza predefinita in un computer denominato `ACCNT27`usare `tcp:ACCNT27` . Per un'istanza denominata `PAYROLL`nello stesso computer usare `tcp:ACCNT27\PAYROLL` . Se è possibile connettersi usando l'indirizzo IP ma non è possibile farlo usando il nome del computer, significa che c'è un problema di risoluzione dei nomi. Tornare alla parte 4 della sezione **Test della connettività TCP/IP**.

4. Quando è possibile connettersi usando il nome del computer forzando TCP, tentare la connessione usando il nome del computer senza forzare TCP. Ad esempio, per un'istanza predefinita usare solo il nome del computer, ad esempio `CCNT27` Per un'istanza denominata usare il nome del computer e il nome di istanza, ad esempio `ACCNT27\PAYROLL` Se è stato possibile connettersi forzando TCP ma non è stato possibile senza forzare TCP, è probabile che il client stia usando un altro protocollo, ad esempio named pipe.

    1. In Gestione configurazione SQL Server nel computer client espandere **Configurazione** *SQL Native Client* **versione**nel riquadro sinistro e quindi selezionare **Protocolli client**.
    2. Nel riquadro destro assicurarsi che TCP/IP sia abilitato. Se TCP/IP è disabilitato, fare clic con il pulsante destro del mouse su **TCP/IP** e quindi fare clic su **Abilita**.
    3. Assicurarsi che l'ordine dei protocolli per TCP/IP sia rappresentato da un numero più piccolo rispetto a quello di named pipe o protocolli VIA (nelle versioni precedenti). In genere è consigliabile lasciare Shared Memory con ordine 1 e TCP/IP con ordine 2. Shared Memory viene usato solo quando il client e SQL Server sono in esecuzione nello stesso computer. Viene tentato l'uso di tutti i protocolli abilitati nell'ordine fino a quando non viene stabilita una connessione, ad eccezione di Shared Memory che viene ignorato quando non viene stabilita la connessione allo stesso computer. 

