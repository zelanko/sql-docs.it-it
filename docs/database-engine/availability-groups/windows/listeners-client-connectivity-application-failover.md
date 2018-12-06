---
title: Listener, connettività client e failover dell'applicazione | Microsoft Docs
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], listeners
- read-only routing
- read-intent connections [AlwaysOn Availability Groups]
- Availability Groups [SQL Server], configuring
- Availability Groups [SQL Server], read-only routing
- Availability Groups [SQL Server], client connectivity
ms.assetid: 76fb3eca-6b08-4610-8d79-64019dd56c44
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: b02b430acbc2fc56942e1c7287ea1c7e4527ccc4
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52408888"
---
# <a name="listeners-client-connectivity-application-failover"></a>Listener, connettività client e failover dell'applicazione
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  In questo argomento sono contenute informazioni sulla funzionalità di failover delle applicazioni e sulla connettività client di [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] .  
  
> [!NOTE]  
>  Per la maggior parte delle configurazioni comuni del listener, è possibile creare il listener del primo gruppo di disponibilità tramite cmdlet di PowerShell o istruzioni [!INCLUDE[tsql](../../../includes/tsql-md.md)] . Per ulteriori informazioni, vedere [Attività correlate](#RelatedTasks)più avanti in questo argomento.  
  
 **Contenuto dell'argomento:**  
  
-   [Listener del gruppo di disponibilità](#AGlisteners)  
  
-   [Utilizzo di un listener per connettersi alla replica primaria](#ConnectToPrimary)  
  
-   [Utilizzo di un listener per connettersi a una replica secondaria di sola lettura (routing di sola lettura)](#ConnectToSecondary)  
  
    -   [Per configurare repliche di disponibilità per il routing di sola lettura](#ConfigureARsForROR)  
  
    -   [Finalità dell'applicazione di sola lettura e routing di sola lettura](#ReadOnlyAppIntent)  
  
-   [Ignorare i listener del gruppo di disponibilità](#BypassAGl)  
  
-   [Comportamento delle connessioni client al failover](#CCBehaviorOnFailover)  
  
-   [Supporto del failover su più subnet del gruppo di disponibilità](#SupportAgMultiSubnetFailover)  
  
-   [Listener del gruppo di disponibilità e certificati SSL](#SSLcertificates)  
  
-   [Listener del gruppo di disponibilità e nomi entità server (SPN)](#SPNs)  
  
-   [Attività correlate](#RelatedTasks)  
  
-   [Contenuto correlato](#RelatedContent)  
  
##  <a name="AGlisteners"></a> Listener del gruppo di disponibilità  
 È possibile fornire la connettività client al database di un determinato gruppo di disponibilità creando un listener del gruppo di disponibilità. Un listener del gruppo di disponibilità è un nome di rete virtuale (VNN, Virtual Network Name) a cui i client possono connettersi per accedere a un database in una replica primaria o secondaria di un gruppo di disponibilità Always On. Un listener del gruppo di disponibilità consente a un client di connettersi a una replica di disponibilità senza conoscere il nome dell'istanza fisica di SQL Server a cui il client si deve connettere.  Non è necessario modificare la stringa di connessione client per connettersi al percorso corrente della replica primaria corrente.  
  
 Un listener del gruppo di disponibilità è composto da un nome listener DNS, dal numero di porta e da uno o più indirizzi IP. Solo il protocollo TCP è supportato dal listener del gruppo di disponibilità.  È inoltre necessario che il nome DNS del listener sia univoco nel dominio e in NetBIOS.  Alla sua creazione, il listener del gruppo di disponibilità diventa una risorsa di un cluster con un nome di rete virtuale (VNN) e un indirizzo IP virtuale (VIP) associati, oltre alla dipendenza del gruppo di disponibilità. Un client utilizza il DNS per risolvere il VNN in più indirizzi IP e quindi tenta di connettersi a ogni indirizzo, fino a che una richiesta di connessione riesce o fino a che le richieste di connessione non scadranno.  
  
 Se il routing di sola lettura viene configurato per una o più [repliche secondarie leggibili](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md), le connessioni client con finalità di lettura alla replica primaria vengono reindirizzate a una replica secondaria leggibile. Inoltre, se la replica primaria viene portata offline su un'istanza di SQL Server e una nuova replica primaria viene portata online su un'altra, il listener del gruppo di disponibilità abilita i client a connettersi alla nuova replica primaria.  
  
 Per informazioni essenziali sui listener del gruppo di disponibilità, vedere [Creare o configurare un listener del gruppo di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md).  
  
 **Contenuto della sezione**  
  
-   [Configurazione del listener del gruppo di disponibilità](#AGlConfig)  
  
-   [Selezione della porta per il listener del gruppo di disponibilità](#SelectListenerPort)  
  
###  <a name="AGlConfig"></a> Configurazione del listener del gruppo di disponibilità  
 Il listener del gruppo di disponibilità è definito dagli elementi seguenti:  
  
 Nome DNS univoco  
 È noto anche come nome di rete virtuale (VNN). Si applicano le regole di denominazione di Active Directory per i nomi host DNS. Per ulteriori informazioni, vedere l'articolo della Knowledge Base [Convenzioni di denominazione di Active Directory per computer, domini, siti e unità organizzative](https://support.microsoft.com/kb/909264) .  
  
 Uno o più indirizzi IP virtuali (VIP)  
 Indirizzi IP virtuali configurati per una o più subnet su cui è possibile eseguire il failover del gruppo di disponibilità.  
  
 Configurazione dell'indirizzo IP  
 Per un listener del gruppo di disponibilità specifico, nell'indirizzo IP vengono utilizzati il protocollo DHCP (Dynamic Host Configuration Protocol) o uno o più indirizzi IP statici.  
  
-   DHCP (Dynamic Host Configuration Protocol)  
  
     Se un gruppo di disponibilità risiede in una sola subnet, è possibile configurare tutti gli indirizzi IP del listener del gruppo di disponibilità per l'utilizzo di DHCP. Per gli ambienti di pre-produzione, tramite DHCP viene offerta una semplice installazione per un gruppo di disponibilità per cui non è richiesto il ripristino di emergenza su un sito remoto in una subnet separata. Tuttavia, non è consigliabile utilizzare DHCP insieme a un listener del gruppo di disponibilità in un ambiente di produzione, poiché in caso di inattività, se il lease IP DHCP scade, per la registrazione del nuovo indirizzo IP DHCP associato al nome DNS del listener viene richiesto tempo aggiuntivo. Il tempo aggiuntivo causerà un errore di connessione del client.  
  
-   Indirizzi IP statici  
  
     Negli ambienti di produzione è consigliabile che nei listener del gruppo di disponibilità vengano utilizzati indirizzi IP statici. Inoltre, nel caso in cui i gruppi di disponibilità si estendano su più subnet di un dominio, nel listener di un gruppo di disponibilità devono essere utilizzati indirizzi IP statici.  
  
 Le configurazioni di rete ibride e DHCP su più subnet non sono supportate per i listener del gruppo di disponibilità. Quando si verifica un failover è di fatto possibile che un indirizzo IP dinamico scada o venga rilasciato, compromettendo la disponibilità elevata complessiva.  
  
###  <a name="SelectListenerPort"></a> Selezione della porta per il listener del gruppo di disponibilità  
 Quando si configura un listener del gruppo di disponibilità, è necessario specificare una porta.  È possibile configurare la porta predefinita su 1433 per non rendere troppo complesse le stringhe di connessione client. Se si intende utilizzare la porta 1433, non è necessario specificare un numero di porta in una stringa di connessione.   Inoltre, poiché ogni listener del gruppo di disponibilità dispone di un nome di rete virtuale separato, ogni listener del gruppo di disponibilità configurato su un solo cluster WSFC può essere configurato per fare riferimento alla stessa porta predefinita 1433.  
  
 È inoltre possibile specificare una porta del listener non standard. Ciò significa, tuttavia, che è necessario specificare in modo esplicito una porta di destinazione nella stringa di connessione ogni volta che ci si connette al listener del gruppo di disponibilità.  Sarà inoltre necessario aprire un'autorizzazione sul firewall per la porta non standard.  
  
 Se si utilizza la porta predefinita 1433 per il nome di rete virtuale del listener del gruppo di disponibilità, è necessario assicurarsi che nessuno altro servizio sul nodo cluster utilizzi questa porta, cosa che provocherebbe un conflitto tra porte.  
  
 Se una delle istanze di SQL Server è già in attesa sulla porta TCP 1433 attraverso il listener dell'istanza e nessun altro servizio, incluse istanze aggiuntive di SQL Server, nel computer è in attesa sulla porta 1433, non si verificherà alcun conflitto tra porte con il listener del gruppo di disponibilità.  Il motivo è dato dal fatto che il listener del gruppo di disponibilità può condividere la stessa porta TCP nello stesso processo del servizio.  È tuttavia opportuno non configurare più istanze di SQL Server (side-by-side) per l'attesa sulla stessa porta.  
  
##  <a name="ConnectToPrimary"></a> Utilizzo di un listener per connettersi alla replica primaria  
 Per utilizzare un listener del gruppo di disponibilità per connettersi alla replica primaria per l'accesso in lettura e scrittura, nella stringa di connessione è necessario specificare il nome DNS del listener del gruppo di disponibilità.  Se una nuova replica diventa la replica primaria del gruppo di disponibilità, le connessioni esistenti che utilizzano il nome di rete del listener del gruppo di disponibilità vengono interrotte.  Le nuove connessioni al listener del gruppo di disponibilità vengono quindi indirizzate alla nuova replica primaria. Di seguito è riportato un esempio di una stringa di connessione di base per il provider ADO.NET (System.Data.SqlClient).  
  
```  
Server=tcp: AGListener,1433;Database=MyDB;IntegratedSecurity=SSPI  
```  
  
 È ancora possibile scegliere di fare riferimento direttamente all'istanza del nome SQL Server della replica primaria o delle repliche secondarie anziché utilizzare il nome server del listener del gruppo di disponibilità, tuttavia se si sceglie di procedere in questo modo le nuove connessioni non verranno indirizzate automaticamente alla replica primaria corrente, perdendo così un notevole vantaggio.  Verranno meno anche i vantaggi derivanti dal routing in sola lettura.  
  
##  <a name="ConnectToSecondary"></a> Utilizzo di un listener per connettersi a una replica secondaria di sola lettura (routing di sola lettura)  
 Con*routing di sola lettura* si intende la capacità di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] di instradare le connessioni in ingresso dirette a un listener del gruppo di disponibilità a una replica secondaria configurata per consentire carichi di lavoro di sola lettura. Una connessione in ingresso che fa riferimento a un nome del listener del gruppo di disponibilità può essere automaticamente indirizzata a una replica in sola lettura qualora sussistano le condizioni seguenti:  
  
-   Almeno una replica secondaria viene impostata sull'accesso di sola lettura e ogni replica secondaria di sola lettura e la replica primaria vengono configurate per supportare il routing di sola lettura. Per altre informazioni, vedere [Per configurare repliche di disponibilità per il routing di sola lettura](#ConfigureARsForROR)più avanti in questa sezione.  

-   La stringa di connessione fa riferimento a un database coinvolto nel gruppo di disponibilità. In alternativa, è possibile configurare il database come database predefinito nell'account di accesso usato nella connessione. Per altre informazioni, vedere [questo articolo sul funzionamento dell'algoritmo con il routing di sola lettura](https://blogs.msdn.microsoft.com/mattn/2012/04/25/calculating-read_only_routing_url-for-alwayson/).

-   La stringa di connessione fa riferimento a un listener del gruppo di disponibilità e la finalità dell'applicazione della connessione in ingresso è impostata su sola lettura, ad esempio con la parola chiave **Application Intent=ReadOnly** nelle proprietà o negli attributi di connessione oppure nelle stringhe di connessione ODBC o OLEDB. Per altre informazioni, vedere [Finalità dell'applicazione di sola lettura e routing di sola lettura](#ReadOnlyAppIntent)più avanti in questa sezione.  
  
###  <a name="ConfigureARsForROR"></a> Per configurare repliche di disponibilità per il routing di sola lettura  
 Un amministratore del database deve configurare le repliche di disponibilità come segue:  
  
1.  Per ogni replica di disponibilità che si desidera configurare come replica secondaria leggibile, un amministratore del database deve configurare le impostazioni seguenti che vengono applicate solo nel ruolo secondario:  
  
    -   È necessario impostare l'accesso alla connessione su "tutto" o "sola lettura".  
  
    -   È necessario specificare l'URL del routing di sola lettura.  
  
2.  Per ognuna di queste repliche, è necessario specificare un elenco di routing di sola lettura per il ruolo primario. Specificare uno o più nomi di server come destinazioni del routing.  
  
####  <a name="RelatedTasksROR"></a> Attività correlate  
  
-   [Configurare l'accesso in sola lettura in una replica di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Configurare il routing di sola lettura per un gruppo di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
###  <a name="ReadOnlyAppIntent"></a> Finalità dell'applicazione di sola lettura e routing di sola lettura  
 La proprietà della stringa di connessione della finalità dell'applicazione esprime la richiesta dell'applicazione client di essere indirizzata a una versione in lettura e scrittura o in sola lettura del database del gruppo di disponibilità. Per utilizzare un routing di sola lettura, un client deve utilizzare la finalità dell'applicazione di sola lettura nella stringa di connessione per connettersi al listener del gruppo di disponibilità. Senza la finalità dell'applicazione di sola lettura, le connessioni al listener del gruppo di disponibilità sono indirizzate al database sulla una replica primaria.  
  
 L'attributo della finalità dell'applicazione viene archiviato nella sessione del client durante l'accesso. L'istanza di SQL Server elaborerà questa finalità e determinerà come procedere in base alla configurazione del gruppo di disponibilità e allo stato in lettura e scrittura corrente del database di destinazione nella replica secondaria.  
  
 Di seguito è riportato un esempio di una stringa di connessione per il provider ADO.NET (System.Data.SqlClient) che specifica la finalità dell'applicazione in sola lettura.  
  
```  
Server=tcp:AGListener,1433;Database=AdventureWorks;IntegratedSecurity=SSPI;ApplicationIntent=ReadOnly  
```  
  
 In questo esempio il client tenta di connettersi al database AdventureWorks tramite un listener del gruppo di disponibilità denominato `AGListener` sulla porta 1433. È possibile omettere la porta se il listener del gruppo di disponibilità è in ascolto sulla porta 1433.  La stringa di connessione contiene la proprietà **ApplicationIntent** impostata su **ReadOnly**ed è quindi una *stringa di connessione con finalità di lettura*.  Senza questa impostazione, il server non avrebbe tentato di eseguire il routing in sola lettura della connessione.  
  
 Il database primario del gruppo di disponibilità elabora la richiesta di routing in sola lettura in ingresso e tenta di trovare una replica online in sola lettura che sia stata aggiunta alla replica primaria e configurata per il routing in sola lettura.  Il client riceve nuovamente le informazioni di connessione dal server della replica primaria e si connette alla replica in sola lettura identificata.  
  
 La finalità dell'applicazione può essere inviata da un driver client a un'istanza di livello inferiore di SQL Server.  In questo caso, la finalità dell'applicazione di sola lettura viene ignorato e la connessione procede normalmente.  
  
 È possibile ignorare il routing di sola lettura non impostando la proprietà di connessione della finalità dell'applicazione su **ReadOnly** (se non viene specificata, il valore predefinito durante l'accesso è **ReadWrite** ) oppure connettendosi direttamente all'istanza della replica primaria di SQL Server anziché usare il nome del listener del gruppo di disponibilità.  Il routing in sola lettura non può avvenire se la connessione viene eseguita direttamente a una replica in sola lettura.  
  
####  <a name="RelatedTasksApps"></a> Attività correlate  
  
-   [Supporto di SQL Server Native Client per il ripristino di emergenza a disponibilità elevata](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)  
  
-   [Utilizzo delle parole chiave delle stringhe di connessione con SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
  
##  <a name="BypassAGl"></a> Ignorare i listener del gruppo di disponibilità  
 Se i listener dei gruppi di disponibilità consentono il supporto per il reindirizzamento del failover e il routing in sola lettura, le connessioni client non devono utilizzarli. Una connessione client può anche fare riferimento all'istanza di SQL Server anziché stabilire la connessione al listener del gruppo di disponibilità.  
  
 Per l'istanza di SQL Server è irrilevante se una connessione effettua l'accesso tramite il listener del gruppo di disponibilità o un altro endpoint dell'istanza.  L'istanza di SQL Server verificherà lo stato del database di destinazione e consentirà o meno la connettività in base alla configurazione del gruppo di disponibilità e lo stato corrente del database sull'istanza.  Ad esempio, se un'applicazione client si connette direttamente a un'istanza della porta di SQL Server e a un database di destinazione ospitato in un gruppo di disponibilità e il database di destinazione si trova nello stato primario ed è online, la connettività ha esito positivo.  Se il database di destinazione è offline o si trova in uno stato transizionale, la connettività al database ha esito negativo.  
  
 In alternativa, durante la migrazione dal mirroring del database a [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], le applicazioni possono specificare la stringa di connessione per il mirroring del database purché esista una sola replica secondaria e non siano consentite le connessioni utente. Per altre informazioni, vedere [Uso delle stringhe di connessione per il mirroring del database con gruppi di disponibilità](#DbmConnectionString)più avanti in questa sezione.  
  
###  <a name="DbmConnectionString"></a> Uso delle stringhe di connessione per il mirroring del database con gruppi di disponibilità  
 Se un gruppo di disponibilità include solo una replica di disponibilità ed è configurato ALLOW_CONNECTIONS = READ_ONLY o ALLOW_CONNECTIONS = NONE per la replica secondaria, i client possono connettersi alla replica primaria tramite una stringa di connessione per il mirroring del database. Questo approccio può essere utile durante la migrazione di un'applicazione esistente dal mirroring del database a un gruppo di disponibilità, a condizione che il gruppo di disponibilità sia limitato a due repliche di disponibilità (una replica primaria e una replica secondaria). Se si aggiungono altre repliche di disponibilità, è necessario creare un listener per il gruppo di disponibilità e aggiornare le applicazioni affinché utilizzino il nome DNS del listener del gruppo di disponibilità.  
  
 Quando si utilizzano le stringhe di connessione per il mirroring del database, il client può utilizzare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client o il provider di dati .NET Framework per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. La stringa di connessione fornita da un client deve specificare almeno il nome di un'istanza del server, ovvero il *nome del partner iniziale*, per identificare l'istanza del server che ospita inizialmente la replica di disponibilità alla quale si desidera connettersi. Facoltativamente, la stringa di connessione può fornire anche il nome di un'altra istanza del server, il *nome del partner di failover*, per identificare l'istanza del server che ospita inizialmente la replica secondaria come nome del partner di failover.  
  
 Per altre informazioni sulle stringhe di connessione per il mirroring del database, vedere [Connettere client a una sessione di mirroring del database &#40;SQL Server&#41;](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md).  
  
##  <a name="CCBehaviorOnFailover"></a> Comportamento delle connessioni client al failover  
 Quando si verifica un failover del gruppo di disponibilità, le connessioni persistenti esistenti al gruppo di disponibilità vengono terminate e il client deve stabilire una nuova connessione per poter continuare a utilizzare lo stesso database primario o il database secondario in sola lettura.  Nel corso di un failover sul lato server, la connettività al gruppo di disponibilità potrebbe non essere disponibile, di conseguenza l'applicazione client potrebbe tentare di riconnettersi finché il database primario non viene riportato online.  
  
 Se il gruppo di disponibilità viene riportato online durante un tentativo di connessione dell'applicazione client, ma prima del periodo di timeout della connessione, è possibile che il driver client si connetta correttamente durante uno di questi tentativi interni senza che si verifichi alcun errore.  
  
##  <a name="SupportAgMultiSubnetFailover"></a> Supporto del failover su più subnet del gruppo di disponibilità  
 Se si usano librerie client che supportano l'opzione di connessione MultiSubnetFailover nella stringa di connessione, è possibile ottimizzare il failover del gruppo di disponibilità su un'altra subnet impostando MultiSubnetFailover su "True" o "Yes", a seconda della sintassi del provider in uso.  
  
> [!NOTE]  
>  È consigliabile utilizzare questa impostazione per le connessioni con una o più subnet a listener di gruppi di disponibilità e a istanze del cluster di failover di SQL Server.  Abilitando questa opzione si aggiungono ulteriori ottimizzazioni, anche per scenari con una sola subnet.  
  
 L'opzione di connessione **MultiSubnetFailover** funziona unicamente con il protocollo di rete TCP ed è supportata solo in caso di connessione a un listener del gruppo di disponibilità e per qualsiasi nome di rete virtuale che si connette a [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)].  
  
 Di seguito è riportato un esempio di una stringa di connessione per il provider ADO.NET (System.Data.SqlClient) che consente il failover su più subnet:  
  
```  
Server=tcp:AGListener,1433;Database=AdventureWorks;IntegratedSecurity=SSPI; MultiSubnetFailover=True  
```  
  
 L'opzione di connessione **MultiSubnetFailover** deve essere impostata su **True** anche se il gruppo di disponibilità si estende su una sola subnet.  In questo modo è possibile preconfigurare nuovi client affinché supportino l'espansione futura su più subnet senza necessità di modificare la stringa di connessione client, oltre a ottimizzare le prestazioni dei failover su una sola subnet.  L'opzione di connessione **MultiSubnetFailover** non è obbligatoria, ma permette di accelerare il failover su subnet.  Il driver client tenta infatti di aprire un socket TCP per ogni indirizzo IP in parallelo associato al gruppo di disponibilità.  Il driver client attende che il primo indirizzo IP risponda, quindi utilizza tale risposta per la connessione.  
  
##  <a name="SSLcertificates"></a> Listener del gruppo di disponibilità e certificati SSL  
 Quando ci si connette a un listener del gruppo di disponibilità, se le istanze di SQL Server utilizzano i certificati SSL insieme alla crittografia della sessione, il driver client che tenta la connessione deve supportare il Nome soggetto alternativo nel certificato SSL per forzare la crittografia.  Il supporto del driver SQL Server per il Nome soggetto alternativo del certificato è pianificato per ADO.NET (SqlClient), Microsoft JDBC e SQL Native Client (SNAC).  
  
 È necessario configurare un certificato X.509 per ogni nodo server che partecipa nel cluster di failover con un elenco di tutti i listener dei gruppi di disponibilità impostati nel Nome soggetto alternativo del certificato.  
  
 Ad esempio, se il cluster WSFC dispone di tre listener con i nomi `AG1_listener.Adventure-Works.com`, `AG2_listener.Adventure-Works.com`e `AG3_listener.Adventure-Works.com`, il Nome soggetto alternativo per il certificato deve essere impostato nel modo seguente:  
  
```  
CN = ServerFQDN  
SAN = ServerFQDN,AG1_listener.Adventure-Works.com, AG2_listener.Adventure-Works.com, AG3_listener.Adventure-Works.com  
```  
  
##  <a name="SPNs"></a> Listener del gruppo di disponibilità e nomi entità server (SPN)  
 Un amministratore di dominio deve configurare un nome entità server (SPN) in Active Directory per ogni nome di listener del gruppo di disponibilità per abilitare Kerberos per la connessione client al listener del gruppo di disponibilità. Per registrare il nome SPN, è necessario usare l'account del servizio dell'istanza del server che ospita la replica di disponibilità.  Per fare in modo che il nome SPN funzioni su tutte le repliche, è necessario riutilizzare lo stesso account del servizio per tutte le istanze nel cluster WSFC che ospita il gruppo di disponibilità.  
  
 Usare lo strumento della riga di comando di Windows **setspn** per configurare il nome SPN.  Ad esempio, per configurare un nome SPNr per un gruppo di disponibilità denominato `AG1listener.Adventure-Works.com` ospitato in un set di istanze di SQL Server configurate per essere eseguite nell'account di dominio `corp/svclogin2`:  
  
```  
setspn -A MSSQLSvc/AG1listener.Adventure-Works.com:1433 corp/svclogin2  
```  
  
 Per ulteriori informazioni sulla registrazione manuale di un nome SPN per SQL Server, vedere [Registrazione di un nome dell'entità servizio per le connessioni Kerberos](../../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md).  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
-   [Connettività client Always On &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md)  
  
-   [Creare o configurare un listener del gruppo di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/create-or-configure-an-availability-group-listener-sql-server.md)  
  
-   [Visualizzare le proprietà del listener del gruppo di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/view-availability-group-listener-properties-sql-server.md)  
  
-   [Rimuovere un listener del gruppo di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-an-availability-group-listener-sql-server.md)  
  
-   [Configurare l'accesso in sola lettura in una replica di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-access-on-an-availability-replica-sql-server.md)  
  
-   [Configurare il routing di sola lettura per un gruppo di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md)  
  
##  <a name="RelatedContent"></a> Contenuto correlato  
  
-   [Microsoft SQL Server Always On Solutions Guide for High Availability and Disaster Recovery (Guida alle soluzioni Always On di Microsoft SQL Server per la disponibilità elevata e il ripristino di emergenza)](https://go.microsoft.com/fwlink/?LinkId=227600)  
  
-   [Introduction to the Availability Group Listener](https://blogs.msdn.microsoft.com/sqlalwayson/2012/01/16/introduction-to-the-availability-group-listener/) (Introduzione al listener del gruppo di disponibilità), nel blog del team di SQL Server Always On  
  
-   [SQL Server Always On Team Blog: The official SQL Server Always On Team Blog (Blog del team di SQL Server Always On: blog ufficiale del team di SQL Server Always On)](https://blogs.msdn.microsoft.com/sqlalwayson/)  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Connettività client AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/always-on-client-connectivity-sql-server.md)   
 [Informazioni sull'accesso alla connessione client per le repliche di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/about-client-connection-access-to-availability-replicas-sql-server.md)   
 [Repliche secondarie attive: Repliche secondarie leggibili &#40;Gruppi di disponibilità AlwaysOn&#41;](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md)   
 [Connettere client a una sessione di mirroring del database &#40;SQL Server&#41;](../../../database-engine/database-mirroring/connect-clients-to-a-database-mirroring-session-sql-server.md)  
  
  
