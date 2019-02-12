---
title: Supporto SQL Server Native Client per la disponibilità elevata, ripristino di emergenza | Microsoft Docs
ms.custom: ''
ms.date: 08/31/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 2b06186b-4090-4728-b96b-90d6ebd9f66f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4bd73d32a58e156a3ae8577d41bbdd4725f85656
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56040232"
---
# <a name="sql-server-native-client-support-for-high-availability-disaster-recovery"></a>Supporto di SQL Server Native Client per il ripristino di emergenza a disponibilità elevata
  In questo argomento viene illustrato il supporto in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (aggiunto in [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]) per [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Per altre informazioni sulle [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], vedere [listener del gruppo di disponibilità, connettività Client e Failover dell'applicazione &#40;SQL Server&#41;](../../../database-engine/listeners-client-connectivity-application-failover.md), [la creazione e configurazione di gruppi di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md), [Clustering di Failover e gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md), e [repliche secondarie attive: Repliche secondarie leggibili (gruppi di disponibilità AlwaysOn)](../../../database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).  
  
 È possibile specificare il listener di un determinato gruppo di disponibilità nella stringa di connessione. Se un'applicazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client è connessa a un database in un gruppo di disponibilità, la connessione originale viene interrotta e deve esserne aperta una nuova per l'applicazione affinché quest'ultima possa continuare a funzionare dopo il failover.  
  
 Se non si sta eseguendo la connessione a un listener del gruppo di disponibilità e se più indirizzi IP sono associati a un nome host, in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client verranno scorsi in sequenza tutti gli indirizzi IP associati alla voce DNS. Questa operazione può richiedere tempi lunghi se il primo indirizzo IP restituito dal server DNS non è associato ad alcuna scheda di interfaccia di rete. In caso di connessione a un listener del gruppo di disponibilità, in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client viene effettuato un tentativo di connessione a tutti gli indirizzi IP in parallelo e in caso di riuscita, tramite il driver verrà rimosso qualsiasi tentativo di connessione in sospeso.  
  
> [!NOTE]  
>  L'aumento del timeout di connessione e l'implementazione della logica di riesecuzione per le connessioni aumentano le probabilità che un'applicazione si connetta a un gruppo di disponibilità. Inoltre, poiché potrebbe non essere possibile stabilire una connessione a causa del failover di un gruppo di disponibilità, è opportuno implementare la logica di riesecuzione delle connessioni, finché non si ottiene la riconnessione.  
  
## <a name="connecting-with-multisubnetfailover"></a>Connessione con MultiSubnetFailover  
 Specificare sempre `MultiSubnetFailover=Yes` in caso di connessione a un listener del gruppo di disponibilità di SQL Server 2012 o a un'istanza del cluster di failover di SQL Server 2012. `MultiSubnetFailover` consente un failover più veloce per tutti i gruppi di disponibilità, permette di abilitare l'istanza del cluster di failover in SQL Server 2012, nonché di ridurre in modo significativo la durata del failover per le topologie AlwaysOn singole e su più subnet. Durante un failover su più subnet, verranno tentate connessioni in parallelo da parte del client. Durante un failover della subnet, in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client verrà ritentata in modo insistente la connessione TCP.  
  
 La proprietà di connessione `MultiSubnetFailover` indica che l'applicazione viene distribuita in un gruppo di disponibilità o nell'istanza del cluster di failover e che in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client verrà effettuato un tentativo di connessione al database nell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] primaria tentando di connettersi a tutti gli indirizzi IP. Quando si `MultiSubnetFailover=Yes` viene specificato per una connessione, il client Riprova tentativi di connessione TCP più velocemente rispetto a intervalli di ritrasmissione TCP predefiniti del sistema operativo. In tal modo si abilita la riconnessione a seguito di failover di un gruppo di disponibilità AlwaysOn o un'istanza del cluster di failover AlwaysOn ed è applicabile a istanze del cluster di failover o a gruppi di disponibilità su una singola subnet o su più subnet.  
  
 Per altre informazioni sulle parole chiave della stringa di connessione, vedere [Utilizzo delle parole chiave delle stringhe di connessione con SQL Server Native Client](../applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 La specificazione di `MultiSubnetFailover=Yes` durante la connessione a un oggetto diverso da un listener del gruppo di disponibilità o dell'istanza del cluster di failover non è supportata poiché potrebbe determinare un impatto negativo sulle prestazioni.  
  
 Utilizzare le linee guida seguenti per connettersi a un server in un gruppo di disponibilità o nell'istanza del cluster di failover:  
  
-   Utilizzare la proprietà di connessione `MultiSubnetFailover` in caso di connessione a una subnet singola o a più subnet, in modo da migliorare le prestazioni.  
  
-   Per eseguire la connessione a un gruppo di disponibilità, specificare il listener del gruppo di disponibilità come server nella stringa di connessione.  
  
-   La connessione a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] configurata con più di 64 indirizzi IP determinerà un errore di connessione.  
  
-   Il comportamento di un'applicazione in cui viene utilizzata la proprietà di connessione `MultiSubnetFailover` non è influenzato dal tipo di autenticazione, cioè Autenticazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], Autenticazione Kerberos o Autenticazione di Windows.  
  
-   È possibile aumentare il valore di `loginTimeout` per adattarlo alla durata del failover e ridurre il numero di nuovi tentativi di connessione dell'applicazione.  
  
-   Le transazioni distribuite non sono supportate.  
  
 Se il routing di sola lettura non è attivo, non è possibile stabilire una connessione a un percorso di replica secondaria in un gruppo di disponibilità nelle situazioni seguenti:  
  
1.  Se il percorso di replica secondaria non è configurato per accettare le connessioni.  
  
2.  Se in un'applicazione viene utilizzato `ApplicationIntent=ReadWrite` (già illustrato in precedenza) e il percorso di replica secondaria è configurato per l'accesso in sola lettura.  
  
 Una connessione non verrà eseguita correttamente se una replica primaria è configurata per rifiutare i carichi di lavoro in sola lettura e nella stringa di connessione è contenuto `ApplicationIntent=ReadOnly`.  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>Aggiornamento per l'utilizzo di cluster su più subnet dal mirroring del database  
 Si verificherà un errore di connessione se nella stringa di connessione sono presenti le parole chiave di connessione `MultiSubnetFailover` e `Failover_Partner`. Si verificherà un errore anche se viene utilizzato `MultiSubnetFailover` e se tramite [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] viene restituita una risposta del partner di failover in cui viene indicato che fa parte di una coppia del mirroring del database.  
  
 Se si aggiorna un'applicazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client in cui al momento è utilizzato il mirroring del database in uno scenario su più subnet, è necessario rimuovere la proprietà di connessione `Failover_Partner` e sostituirla con `MultiSubnetFailover` impostata su `Yes`, nonché sostituire il nome del server nella stringa di connessione con un listener del gruppo di disponibilità. Se in una stringa di connessione vengono utilizzati `Failover_Partner` e `MultiSubnetFailover=Yes`, verrà generato un errore dal driver. Se, tuttavia, in una stringa di connessione vengono utilizzati `Failover_Partner` e `MultiSubnetFailover=No` (o `ApplicationIntent=ReadWrite`), nell'applicazione verrà utilizzato il mirroring del database.  
  
 Tramite il driver verrà restituito un errore se il mirroring del database viene utilizzato nel database primario nel gruppo di disponibilità e se `MultiSubnetFailover=Yes` viene utilizzato nella stringa di connessione a un database primario anziché a un listener del gruppo di disponibilità.  
  
## <a name="specifying-application-intent"></a>Specificazione della finalità dell'applicazione  
 Se `ApplicationIntent=ReadOnly`, nel client viene richiesto un carico di lavoro di lettura quando si esegue la connessione a un database abilitato per AlwaysOn. Tramite il server, la finalità verrà applicata al momento della connessione e durante un'istruzione di database USE, ma solo a un database abilitato per Always On.  
  
 La parola chiave `ApplicationIntent` non funziona con i database legacy di sola lettura.  
  
 Un database può consentire o impedire carichi di lavoro di lettura nel database AlwaysOn di destinazione. (Questa operazione viene eseguita con il `ALLOW_CONNECTIONS` clausola del `PRIMARY_ROLE` e `SECONDARY_ROLE` [!INCLUDE[tsql](../../../includes/tsql-md.md)] istruzioni.)  
  
 La parola chiave `ApplicationIntent` è utilizzata per abilitare il routing di sola lettura.  
  
## <a name="read-only-routing"></a>Routing di sola lettura  
 Il routing di sola lettura è una funzionalità che può garantire la disponibilità di una replica di sola lettura di un database. Per abilitare il routing di sola lettura:  
  
1.  È necessario connettersi a un listener del gruppo di disponibilità Always On.  
  
2.  La parola chiave della stringa di connessione `ApplicationIntent` deve essere impostata su `ReadOnly`.  
  
3.  Il gruppo di disponibilità deve essere configurato dall'amministratore del database per abilitare il routing di sola lettura.  
  
 È possibile che non tutte le connessioni in cui viene utilizzato il routing di sola lettura vengano stabilite alla stessa replica di sola lettura. Le modifiche nella sincronizzazione del database o nella configurazione di routing del server possono comportare connessioni client a repliche di sola lettura diverse. Per assicurare la connessione di tutte le richieste di sola lettura alla stessa replica di sola lettura, non fornire un listener del gruppo di disponibilità alla parola chiave della stringa di connessione `Server`. Specificare invece il nome dell'istanza di sola lettura.  
  
 Il routing di sola lettura potrebbe impiegare più tempo a connettersi rispetto alla replica primaria poiché innanzitutto viene eseguita la connessione del routing di sola lettura alla replica primaria e, successivamente, viene cercata la replica secondaria migliore dal punto di vista della lettura. Per questo motivo è necessario aumentare il timeout di accesso.  
  
## <a name="odbc"></a>ODBC  
 Sono state aggiunte due parole chiave per le stringhe di connessione ODBC per supportare [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client:  
  
-   `ApplicationIntent`  
  
-   `MultiSubnetFailover`  
  
 Per altre informazioni sulle parole chiave della stringa di connessione ODBC in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, vedere [Utilizzo delle parole chiave delle stringhe di connessione con SQL Server Native Client](../applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Le proprietà di connessione equivalenti sono:  
  
-   `SQL_COPT_SS_APPLICATION_INTENT`  
  
-   `SQL_COPT_SS_MULTISUBNET_FAILOVER`  
  
 Per altre informazioni sulle proprietà di connessione ODBC in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, vedere [SQLSetConnectAttr](../../native-client-odbc-api/sqlsetconnectattr.md).  
  
 La funzionalità delle parole chiave `ApplicationIntent` e `MultiSubnetFailover` verrà esposta in Amministratore origine dati ODBC per i DSN in cui viene utilizzato il driver di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, a partire da [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
 Un'applicazione ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client può utilizzare, per la connessione, una delle tre funzioni seguenti:  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|[SQLBrowseConnect](../../native-client-odbc-api/sqlbrowseconnect.md)|L'elenco di server restituiti da `SQLBrowseConnect` non includerà i nomi di rete virtuale. Verrà visualizzato solo un elenco di server senza indicazione del fatto che il server sia un server autonomo oppure un server primario o secondario in un cluster WSFC (Windows Server Failover Clustering) che contiene due o più istanze di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] abilitate per [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Se si esegue la connessione a un server e viene restituito un errore, è possibile che sia stata stabilita la connessione a un server e l'impostazione `ApplicationIntent` non sia compatibile con la configurazione del server.<br /><br /> Poiché `SQLBrowseConnect` non riconosce i server in un cluster WSFC (Windows Server Failover Clustering) che contiene due o più istanze di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] abilitate per [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], la parola chiave della stringa di connessione `SQLBrowseConnect` viene ignorata da `MultiSubnetFailover`.|  
|[SQLConnect](../../native-client-odbc-api/sqlconnect.md)|`SQLConnect` supporta sia `ApplicationIntent` sia `MultiSubnetFailover` tramite un nome di origine dati (DSN) o proprietà di connessione.|  
|[SQLDriverConnect](../../native-client-odbc-api/sqldriverconnect.md)|`SQLDriverConnect` supporta `ApplicationIntent` e `MultiSubnetFailover` tramite parole chiave della stringa di connessione, proprietà di connessione o DSN.|  
  
## <a name="ole-db"></a>OLE DB  
 OLE DB in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client non supporta la parola chiave `MultiSubnetFailover`.  
  
 OLE DB in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client supporta la finalità dell'applicazione. La finalità dell'applicazione è la stessa per le applicazioni OLE DB e per quelle ODBC (vedere sopra).  
  
 Per supportare [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client è stata aggiunta una parole chiave per la stringa di connessione OLE DB:  
  
-   `Application Intent`  
  
 Per altre informazioni sulle parole chiave della stringa di connessione in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, vedere [Utilizzo delle parole chiave delle stringhe di connessione con SQL Server Native Client](../applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Le proprietà di connessione equivalenti sono:  
  
-   `SSPROP_INIT_APPLICATIONINTENT`  
  
-   `DBPROP_INIT_PROVIDERSTRING`  
  
 Un'applicazione OLE DB di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client può utilizzare, per specificare la finalità dell'applicazione, uno dei metodi seguenti:  
  
 `IDBInitialize::Initialize`  
 `IDBInitialize::Initialize` prevede l'utilizzo del set di proprietà precedentemente configurato per inizializzare l'origine dati e creare l'oggetto origine dati. La finalità dell'applicazione viene specificata come proprietà del provider o come parte della stringa di proprietà estesa.  
  
 `IDataInitialize::GetDataSource`  
 `IDataInitialize::GetDataSource` accetta una stringa di connessione di input che può contenere la parola chiave `Application Intent`.  
  
 `IDBProperties::GetProperties`  
 `IDBProperties::GetProperties` consente di recuperare il valore della proprietà attualmente impostata sull'origine dati.  È possibile recuperare il valore di `Application Intent` tramite la proprietà DBPROP_INIT_PROVIDERSTRING e la proprietà SSPROP_INIT_APPLICATIONINTENT.  
  
 `IDBProperties::SetProperties`  
 Per impostare il valore della proprietà `ApplicationIntent`, chiamare `IDBProperties::SetProperties` passando la proprietà `SSPROP_INIT_APPLICATIONINTENT` con un valore "`ReadWrite`" o "`ReadOnly`" oppure la proprietà `DBPROP_INIT_PROVIDERSTRING` con un valore contenente "`ApplicationIntent=ReadOnly`" o "`ApplicationIntent=ReadWrite`".  
  
 È possibile specificare la finalità dell'applicazione nel campo delle proprietà della finalità dell’applicazione della scheda Tutte nella finestra di dialogo **Proprietà di Data Link**.  
  
 Quando vengono stabilite connessioni implicite, per la connessione viene utilizzata l'impostazione relativa alla finalità dell'applicazione definita per la connessione padre. Analogamente, più sessioni create dalla stessa origine dati ereditano l'impostazione relativa alla finalità dell'applicazione definita per l'origine dati.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità di SQL Server Native Client](sql-server-native-client-features.md)   
 [Utilizzo delle parole chiave delle stringhe di connessione con SQL Server Native Client](../applications/using-connection-string-keywords-with-sql-server-native-client.md)  
  
  
