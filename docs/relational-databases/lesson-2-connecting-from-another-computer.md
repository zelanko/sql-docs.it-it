---
title: 'Lezione 2: Connessione da un altro computer | Microsoft Docs'
ms.custom: ''
ms.date: 03/08/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: fd4ddeb8-0cb6-441b-9704-03575c07020f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8389d11868108725a676e9196861c7302241a407
ms.sourcegitcommit: 94f6a4b506dfda242fc3efb2403847e22a36d340
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/30/2019
ms.locfileid: "75546557"
---
# <a name="lesson-2-connecting-from-another-computer"></a>Lezione 2: Connessione da un altro computer
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Per una maggiore sicurezza non è possibile accedere al [!INCLUDE[ssDE](../includes/ssde-md.md)] di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Developer Edition, Express Edition ed Evaluation Edition da un altro computer al momento dell'installazione iniziale. In questa lezione vengono descritte le procedure per abilitare i protocolli, configurare le porte e configurare Windows Firewall per la connessione da altri computer.  
  
In questa lezione sono incluse le attività seguenti:  
  
-   [Abilitazione di protocolli](#protocols)  
  
-   [Configurazione di una porta fissa](#port)  
  
-   [Apertura di porte nel firewall](#firewall)  
  
-   [Connessione al Motore di database da un altro computer](#otherComp)  
  
-   [Connessione tramite il servizio SQL Server Browser](#browser)  
  
## <a name="protocols"></a>Abilitazione di protocolli  
Per migliorare la sicurezza, [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]Developer ed Evaluation vengono installati solo con una connettività di rete limitata. Le connessioni a [!INCLUDE[ssDE](../includes/ssde-md.md)] possono essere eseguite da strumenti in esecuzione sullo stesso computer, non da altri computer. Se si intende eseguire l'attività di sviluppo nello stesso computer del [!INCLUDE[ssDE](../includes/ssde-md.md)], non è necessario abilitare protocolli aggiuntivi. [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] si connetterà al [!INCLUDE[ssDE](../includes/ssde-md.md)] usando il protocollo Shared Memory. che è già abilitato.  
  
Se si intende effettuare la connessione a [!INCLUDE[ssDE](../includes/ssde-md.md)] da un altro computer, è necessario abilitare un protocollo, ad esempio TCP/IP.  
  
#### <a name="how-to-enable-tcpip-connections-from-another-computer"></a>Come abilitare le connessioni TCP/IP da un altro computer  
  
1.  Fare clic sul menu **Start** , scegliere **Tutti i programmi**, [!INCLUDE[ssCurrentUI](../includes/sscurrentui-md.md)], **Strumenti di configurazione**e quindi **Gestione configurazione SQL Server**.  
  
    > [!NOTE]  
    > Possono essere disponibili entrambe le opzioni a 32 e 64 bit.  
  
    > [!NOTE]  
    > Poiché Gestione configurazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] è uno snap-in per il programma [!INCLUDE[msCoName](../includes/msconame-md.md)] Management Console e non un programma autonomo, Gestione configurazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] non viene visualizzato come applicazione nelle versioni più recenti di Windows. Il nome del file contiene un numero che rappresenta il numero di versione di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per aprire Gestione configurazione tramite il comando Esegui, sono elencati di seguito i percorsi per le ultime quattro versioni con Windows installato nell'unità C.  
  
    |||  
    |-|-|
    |[!INCLUDE[ssSQL17](../includes/sssql17-md.md)]|C:\Windows\SysWOW64\SQLServerManager14.msc|
    |[!INCLUDE[ssSQL16](../includes/sssql16-md.md)]|C:\Windows\SysWOW64\SQLServerManager13.msc|  
    |[!INCLUDE[ssSQL14](../includes/sssql14-md.md)]|C:\Windows\SysWOW64\SQLServerManager12.msc|  
    |[!INCLUDE[ssSQL11](../includes/sssql11-md.md)]|C:\Windows\SysWOW64\SQLServerManager11.msc|
  
2.  In **Gestione configurazione SQL Server** espandere **Configurazione di rete SQL Server**, quindi fare clic su **Protocolli per** _<InstanceName>_ .  
  
    L'istanza predefinita (un'istanza senza nome) è indicata come **MSSQLSERVER**. Se è stata installata un'istanza denominata, il nome fornito è elencato. [!INCLUDE[ssExpressEd11](../includes/ssexpressed11-md.md)] viene installato come **SQLEXPRESS**, a meno che non sia stato specificato un nome diverso durante l'installazione.  
  
3.  Nell'elenco dei protocolli fare clic con il pulsante destro del mouse sul protocollo da abilitare (**TCP/IP**), quindi scegliere **Abilita**.  
  
    > [!NOTE]  
    > Dopo avere apportato modifiche ai protocolli di rete, è necessario riavviare il servizio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Questa operazione viene completata nell'attività successiva.  

## <a name="port"></a>Configurazione di una porta fissa  
Per una maggiore sicurezza, in Windows Server 2008, [!INCLUDE[wiprlhlong](../includes/wiprlhlong-md.md)] e Windows 7 è abilitato Windows Firewall. Se si desidera connettersi a questa istanza da un altro computer, è necessario aprire una porta di comunicazione nel firewall. L'istanza predefinita di [!INCLUDE[ssDE](../includes/ssde-md.md)] resta in attesa sulla porta 1433 e non è pertanto necessario configurare una porta fissa. Le istanze denominate, inclusa [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] , restano tuttavia in attesa su porte dinamiche. Per aprire una porta nel firewall, è innanzitutto necessario configurare il [!INCLUDE[ssDE](../includes/ssde-md.md)] per l'attesa su una porta specifica nota come porta fissa o statica. In caso contrario, è possibile che il [!INCLUDE[ssDE](../includes/ssde-md.md)] resti in attesa su una porta diversa a ogni avvio. Per altre informazioni sui firewall e sulle impostazioni predefinite di Windows Firewall e per una descrizione delle porte TCP che interessano il motore di database, Analysis Services, Reporting Services e Integration Services, vedere [Configurare Windows Firewall per consentire l'accesso a SQL Server](../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
> [!NOTE]  
> Le assegnazioni dei numeri di porta vengono gestite da IANA (Internet Assigned Numbers Authority) e sono elencate in [https://www.iana.org](https://go.microsoft.com/fwlink/?LinkId=48844). I numeri di porta devono essere assegnati utilizzando numeri compresi tra 49152 e 65535.  
  
#### <a name="configure-sql-server-to-listen-on-a-specific-port"></a>Configurare SQL Server per l'attesa su una porta specifica  
  
1.  In Gestione configurazione [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] espandere **Configurazione di rete SQL Server** e quindi fare clic sull'istanza del server che si vuole configurare.  
  
2.  Nel riquadro destro fare doppio clic su **TCP/IP**.  
  
3.  Nella finestra di dialogo **Proprietà TCP/IP** fare clic sulla scheda **Indirizzi IP** .  
  
4.  Nella casella **Porta TCP** della sezione **IPAll** digitare un numero di porta disponibile. Per questa esercitazione verrà usata la porta **49172**.  
  
5.  Scegliere **OK** per chiudere la finestra di dialogo e scegliere di nuovo **OK** nel messaggio di avviso che indica che è necessario riavviare il servizio.  
  
6.  Nel riquadro di sinistra fare clic su **Servizi di SQL Server**.  
  
7.  Nel riquadro di destra fare clic con il pulsante destro del mouse sull'istanza di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], quindi scegliere **Riavvia**. Al riavvio, il [!INCLUDE[ssDE](../includes/ssde-md.md)] sarà in attesa sulla porta **49172**.  
  
## <a name="firewall"></a>Apertura di porte nel firewall  
I sistemi firewall contribuiscono a impedire l'accesso non autorizzato alle risorse del computer. Per connettersi a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] da un altro computer quando un firewall è attivato, è necessario aprire una porta nel firewall.  
  
> [!IMPORTANT]  
> L'apertura di porte nel firewall potrebbe esporre il server ad attacchi dannosi. Prima di aprire porte, è opportuno avere familiarità con i sistemi firewall. Per altre informazioni, vedere [Security Considerations for a SQL Server Installation](../sql-server/install/security-considerations-for-a-sql-server-installation.md).  
  
Dopo aver configurato [!INCLUDE[ssDE](../includes/ssde-md.md)] per l'utilizzo di una porta fissa, attenersi alle istruzioni seguenti per aprire tale porta in Windows Firewall. Non è necessario configurare una porta fissa per l'istanza predefinita poiché è già impostata sulla porta TCP 1433.  
  
#### <a name="to-open-a-port-in-the-windows-firewall-for-tcp-access-windows-7"></a>Per aprire una porta in Windows Firewall per l'accesso TCP (Windows 7)  
  
1.  Dal menu **Start** scegliere **Esegui**, digitare **WF.msc**, quindi fare clic su **OK**.  
  
2.  Nel riquadro sinistro di **Windows Firewall con sicurezza avanzata**fare clic con il pulsante destro del mouse su **Regole in entrata**, quindi scegliere **Nuova regola** nel riquadro azioni.  
  
3.  Nella finestra di dialogo **Tipo di regola** selezionare **Porta**, quindi fare clic su **Avanti**.  
  
4.  Nella finestra di dialogo **Protocollo e porte** selezionare **TCP**. Selezionare **Porte locali specifiche**e quindi digitare il numero di porta dell'istanza di [!INCLUDE[ssDE](../includes/ssde-md.md)]. Digitare 1433 per l'istanza predefinita. Digitare **49172** se si sta configurando un'istanza denominata ed è stata configurata una porta fissa nell'attività precedente. Fare clic su **Avanti**.  
  
5.  Nella finestra di dialogo **Azione** selezionare **Consenti la connessione**, quindi fare clic su **Avanti**.  
  
6.  Nella finestra di dialogo **Profilo** selezionare tutti i profili che descrivono l'ambiente di connessione del computer quando si desidera eseguire la connessione al [!INCLUDE[ssDE](../includes/ssde-md.md)], quindi fare clic su **Avanti**.  
  
7.  Nella finestra di dialogo **Nome** digitare un nome e una descrizione per questa regola, quindi fare clic su **Fine**.  
  
Per altre informazioni sulla configurazione del firewall e le istruzioni per [!INCLUDE[wiprlhlong](../includes/wiprlhlong-md.md)], vedere [Configurazione di Windows Firewall per l'accesso al Motore di database](../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md). Per altre informazioni sulle impostazioni predefinite di Windows Firewall e per una descrizione delle porte TCP che interessano il motore di database, Analysis Services, Reporting Services e Integration Services, vedere [Configurare Windows Firewall per consentire l'accesso a SQL Server](../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md).  
  
## <a name="otherComp"></a>Connessione al Motore di database da un altro computer  
Dopo avere configurato [!INCLUDE[ssDE](../includes/ssde-md.md)] per l'ascolto su una porta fissa e avere aperto tale porta nel firewall, è possibile connettersi a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] da un altro computer.  
  
Se il servizio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser è in esecuzione nel computer server e la porta UDP 1434 è aperta nel firewall, è possibile stabilire la connessione specificando il nome del computer e quello dell'istanza. Per migliorare la sicurezza, in questo esempio non viene utilizzato il servizio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser.  
  
#### <a name="to-connect-to-the-database-engine-from-another-computer"></a>Per connettersi al Motore di database da un altro computer  
  
1.  In un secondo computer contenente gli strumenti client di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , eseguire l'accesso con un account autorizzato a connettersi a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]e aprire [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)].  
  
2.  Nella finestra di dialogo **Connetti al server** confermare l'opzione **Motore di database** nella casella **Tipo server** .  
  
3.  Nella casella **Nome server** digitare **tcp:** per specificare il protocollo, quindi immettere il nome del computer, una virgola e il numero di porta. Per la connessione all'istanza predefinita viene automaticamente usata la porta 1433, la quale può quindi essere omessa. Digitare pertanto **tcp:** _<nome_computer>_ . In questo esempio di istanza denominata digitare **tcp:** _<nome_computer>_ **,49172**.  
  
    > [!NOTE]  
    > Se si omette **tcp:** nella casella **Nome server** , il client eseguirà un tentativo con tutti i protocolli abilitati, nell'ordine specificato nella configurazione client.  
  
4.  Nella casella **Autenticazione** confermare l'opzione **Autenticazione di Windows**e quindi fare clic su **Connetti**.  
  
## <a name="browser"></a>Connessione tramite il servizio SQL Server Browser  
Il servizio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser resta in attesa delle richieste in ingresso di risorse di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e fornisce informazioni sulle istanze di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] installate nel computer. Quando il servizio [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser è in esecuzione, gli utenti possono connettersi a istanze denominate specificando il nome del computer e il nome dell'istanza anziché il nome del computer e il numero della porta. Dato che [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser riceve richieste UDP non autenticate, non sempre è abilitato durante l'installazione. Per una descrizione del servizio e dei casi in cui viene attivato, vedere [Servizio SQL Server Browser &#40;Motore database e SSAS&#41;](../database-engine/configure-windows/sql-server-browser-service-database-engine-and-ssas.md).  
  
Per utilizzare [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Browser, è necessario seguire la stessa procedura descritta in precedenza e aprire la porta UDP 1434 nel firewall.  
  
Si conclude così questa breve esercitazione sulla connettività di base.  
  
## <a name="return-to-tutorials-portal"></a>Ritornare al portale delle esercitazioni  
[Esercitazione: Introduzione al motore di database](../relational-databases/tutorial-getting-started-with-the-database-engine.md)  
  

