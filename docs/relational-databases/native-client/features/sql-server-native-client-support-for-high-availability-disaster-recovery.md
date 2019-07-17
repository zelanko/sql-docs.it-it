---
title: Supporto SQL Server Native Client per la disponibilità elevata, ripristino di emergenza | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 2b06186b-4090-4728-b96b-90d6ebd9f66f
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0a3b5c8d98b2c7bbfa62641b89b0bfcb031a6c02
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68067249"
---
# <a name="sql-server-native-client-support-for-high-availability-disaster-recovery"></a>Supporto di SQL Server Native Client per il ripristino di emergenza a disponibilità elevata
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  In questo argomento viene illustrato il supporto in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client (aggiunto in [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]) per [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Per altre informazioni sulle [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], vedere [listener del gruppo di disponibilità, connettività Client e Failover dell'applicazione &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/listeners-client-connectivity-application-failover.md), [la creazione e configurazione di gruppi di disponibilità &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/creation-and-configuration-of-availability-groups-sql-server.md), [Clustering di Failover e gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](~/database-engine/availability-groups/windows/failover-clustering-and-always-on-availability-groups-sql-server.md), e [repliche secondarie attive: Repliche secondarie leggibili &#40;gruppi di disponibilità AlwaysOn&#41;](~/database-engine/availability-groups/windows/active-secondaries-readable-secondary-replicas-always-on-availability-groups.md).  
  
 È possibile specificare il listener di un determinato gruppo di disponibilità nella stringa di connessione. Se un'applicazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client è connessa a un database in un gruppo di disponibilità, la connessione originale viene interrotta e deve esserne aperta una nuova per l'applicazione affinché quest'ultima possa continuare a funzionare dopo il failover.  
  
 Se non si sta eseguendo la connessione a un listener del gruppo di disponibilità e se più indirizzi IP sono associati a un nome host, in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client verranno scorsi in sequenza tutti gli indirizzi IP associati alla voce DNS. Questa operazione può richiedere tempi lunghi se il primo indirizzo IP restituito dal server DNS non è associato ad alcuna scheda di interfaccia di rete. In caso di connessione a un listener del gruppo di disponibilità, in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client viene effettuato un tentativo di connessione a tutti gli indirizzi IP in parallelo e in caso di riuscita, tramite il driver verrà rimosso qualsiasi tentativo di connessione in sospeso.  
  
> [!NOTE]  
>  L'aumento del timeout di connessione e l'implementazione della logica di riesecuzione per le connessioni aumentano le probabilità che un'applicazione si connetta a un gruppo di disponibilità. Inoltre, poiché potrebbe non essere possibile stabilire una connessione a causa del failover di un gruppo di disponibilità, è opportuno implementare la logica di riesecuzione delle connessioni, finché non si ottiene la riconnessione.  
  
## <a name="connecting-with-multisubnetfailover"></a>Connessione con MultiSubnetFailover  
 Specificare sempre **MultiSubnetFailover=Yes** in caso di connessione a un listener del gruppo di disponibilità di SQL Server 2012 o a un'istanza del cluster di failover di SQL Server 2012. **MultiSubnetFailover** consente il failover più veloce per tutti i gruppi di disponibilità e cluster di failover dell'istanza di SQL Server 2012, riducendo notevolmente il tempo di failover per una o più subnet Always On le topologie. Durante un failover su più subnet, verranno tentate connessioni in parallelo da parte del client. Durante un failover della subnet, in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client verrà ritentata in modo insistente la connessione TCP.  
  
 La proprietà di connessione **MultiSubnetFailover** indica che l'applicazione viene distribuita in un gruppo di disponibilità o nell'istanza del cluster di failover e che in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client verrà effettuato un tentativo di connessione al database nell'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] primaria tramite la connessione a tutti gli indirizzi IP. Quando si specifica **MultiSubnetFailover=Yes** per una connessione, i ripetuti tentativi di connessione TCP del client vengono eseguiti più rapidamente rispetto agli intervalli di ritrasmissione TCP predefiniti del sistema operativo. Ciò consente una riconnessione più veloce dopo il failover di un gruppo di disponibilità AlwaysOn o un sempre nel Cluster di failover ed è applicabile solo su più subnet gruppi di disponibilità sia istanze del Cluster di Failover.  
  
 Per altre informazioni sulle parole chiave della stringa di connessione, vedere [Utilizzo delle parole chiave delle stringhe di connessione con SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 La specifica di **MultiSubnetFailover=Yes** durante la connessione a un oggetto diverso da un listener del gruppo di disponibilità o dall'istanza del cluster di failover non è supportata poiché potrebbe determinare un impatto negativo sulle prestazioni.  
  
 Utilizzare le linee guida seguenti per connettersi a un server in un gruppo di disponibilità o nell'istanza del cluster di failover:  
  
-   Usare la proprietà di connessione **MultiSubnetFailover** in caso di connessione a una singola subnet o a più subnet, in modo da migliorare le prestazioni.  
  
-   Per eseguire la connessione a un gruppo di disponibilità, specificare il listener del gruppo di disponibilità come server nella stringa di connessione.  
  
-   La connessione a un'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] configurata con più di 64 indirizzi IP determinerà un errore di connessione.  
  
-   Comportamento di un'applicazione che usa il **MultiSubnetFailover** proprietà di connessione non è interessata in base al tipo di autenticazione: [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] L'autenticazione, l'autenticazione Kerberos o autenticazione di Windows.  
  
-   È possibile aumentare il valore di **loginTimeout** per adattarlo alla durata del failover e ridurre il numero di nuovi tentativi di connessione dell'applicazione.  
  
-   Le transazioni distribuite non sono supportate.  
  
 Se il routing di sola lettura non è attivo, non è possibile stabilire una connessione a un percorso di replica secondaria in un gruppo di disponibilità nelle situazioni seguenti:  
  
1.  Se il percorso di replica secondaria non è configurato per accettare le connessioni.  
  
2.  Se un'applicazione usa **ApplicationIntent=ReadWrite** (vedere di seguito) e il percorso di replica secondaria è configurato per l'accesso in sola lettura.  
  
 Una connessione non riesce se una replica primaria è configurata per rifiutare i carichi di lavoro in sola lettura e la stringa di connessione contiene **ApplicationIntent=ReadOnly**.  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>Aggiornamento per l'utilizzo di cluster su più subnet dal mirroring del database  
 Si verificherà un errore di connessione se nella stringa di connessione sono presenti le parole chiave di connessione **MultiSubnetFailover** e **Failover_Partner**. Si verificherà un errore anche se viene usato **MultiSubnetFailover** e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] restituisce una risposta del partner di failover in cui viene indicato che fa parte di una coppia del mirroring del database.  
  
 Se si aggiorna un'applicazione [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client che usa il mirroring del database in uno scenario su più subnet, è necessario rimuovere la proprietà di connessione **Failover_Partner** e sostituirla con **MultiSubnetFailover** impostata su **Yes**, nonché sostituire il nome del server nella stringa di connessione con un listener del gruppo di disponibilità. Se in una stringa di connessione vengono usati **Failover_Partner** e **MultiSubnetFailover=Yes**, il driver genererà un errore. Se tuttavia in una stringa di connessione vengono usati **Failover_Partner** e **MultiSubnetFailover=No** (o **ApplicationIntent=ReadWrite**), l'applicazione userà il mirroring del database.  
  
 Il driver restituirà un errore se il mirroring del database viene usato nel database primario nel gruppo di disponibilità e se **MultiSubnetFailover=Yes** veine usato nella stringa di connessione a un database primario anziché a un listener del gruppo di disponibilità.  


[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="odbc"></a>ODBC  
 Sono state aggiunte due parole chiave per le stringhe di connessione ODBC per supportare [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client:  
  
-   **ApplicationIntent**  
  
-   **MultiSubnetFailover**  
  
 Per altre informazioni sulle parole chiave della stringa di connessione ODBC in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, vedere [Utilizzo delle parole chiave delle stringhe di connessione con SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Le proprietà di connessione equivalenti sono:  
  
-   **SQL_COPT_SS_APPLICATION_INTENT**  
  
-   **SQL_COPT_SS_MULTISUBNET_FAILOVER**  
  
 Per altre informazioni sulle proprietà di connessione ODBC in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, vedere [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md).  
  
 La funzionalità delle parole chiave **ApplicationIntent** e **MultiSubnetFailover** verrà esposta in Amministratore origine dati ODBC per i DSN in cui viene usato il driver di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, a partire da [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)].  
  
 Un'applicazione ODBC di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client può utilizzare, per la connessione, una delle tre funzioni seguenti:  
  
|Funzione|Descrizione|  
|--------------|-----------------|  
|[SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md)|L'elenco di server restituiti da **SQLBrowseConnect** non includerà i nomi di rete virtuale. Verrà visualizzato solo un elenco di server senza indicazione del fatto che il server sia un server autonomo oppure un server primario o secondario in un cluster WSFC (Windows Server Failover Clustering) che contiene due o più istanze di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] abilitate per [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)]. Se si esegue la connessione a un server e viene restituito un errore, è possibile che sia stata stabilita la connessione a un server e che l'impostazione **ApplicationIntent** non sia compatibile con la configurazione del server.<br /><br /> Poiché **SQLBrowseConnect** non riconosce i server in un cluster WSFC (Windows Server Failover Clustering) che contiene due o più istanze di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] abilitate per [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], la parola chiave della stringa di connessione **MultiSubnetFailover** viene ignorata da **SQLBrowseConnect**.|  
|[SQLConnect](../../../relational-databases/native-client-odbc-api/sqlconnect.md)|**SQLConnect** supporta sia **ApplicationIntent** che **MultiSubnetFailover** tramite un nome origine dati (DSN, Data Source Name) o una proprietà di connessione.|  
|[SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md)|**SQLDriverConnect** supporta **ApplicationIntent** e **MultiSubnetFailover** tramite parole chiave di stringa di connessione, proprietà di connessione o DSN.|  
  
## <a name="ole-db"></a>OLE DB  
 OLE DB in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client non supporta la parola chiave **MultiSubnetFailover**.  
  
 OLE DB in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client supporta la finalità dell'applicazione. La finalità dell'applicazione è la stessa per le applicazioni OLE DB e per quelle ODBC (vedere sopra).  
  
 Per supportare [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client è stata aggiunta una parole chiave per la stringa di connessione OLE DB:  
  
-   **Application Intent**  
  
 Per altre informazioni sulle parole chiave della stringa di connessione in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, vedere [Utilizzo delle parole chiave delle stringhe di connessione con SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md).  
  
 Le proprietà di connessione equivalenti sono:  
  
-   **SSPROP_INIT_APPLICATIONINTENT**  
  
-   **DBPROP_INIT_PROVIDERSTRING**  
  
 Un'applicazione OLE DB di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client può utilizzare, per specificare la finalità dell'applicazione, uno dei metodi seguenti:  
  
 **IDBInitialize::Initialize**  
 **IDBInitialize::Initialize** prevede l'uso del set di proprietà precedentemente configurato per inizializzare l'origine dati e creare l'oggetto origine dati. La finalità dell'applicazione viene specificata come proprietà del provider o come parte della stringa di proprietà estesa.  
  
 **IDataInitialize::GetDataSource**  
 **IDataInitialize::GetDatasource** accetta una stringa di connessione di input che può contenere la parola chiave **Application Intent**.  
  
 **IDBProperties:: GetProperties**  
 **IDBProperties::GetProperties** consente di recuperare il valore della proprietà attualmente impostata sull'origine dati.  È possibile recuperare il valore di **Application Intent** tramite la proprietà DBPROP_INIT_PROVIDERSTRING e la proprietà SSPROP_INIT_APPLICATIONINTENT.  
  
 **IDBProperties::SetProperties**  
 Per impostare il valore della proprietà **ApplicationIntent**, chiamare **IDBProperties::SetProperties** passando la proprietà **SSPROP_INIT_APPLICATIONINTENT** con un valore "**ReadWrite**" o "**ReadOnly**" o la proprietà **DBPROP_INIT_PROVIDERSTRING** con un valore contenente "**ApplicationIntent=ReadOnly**" o "**ApplicationIntent=ReadWrite**".  
  
 È possibile specificare la finalità dell'applicazione nel campo delle proprietà della finalità dell’applicazione della scheda Tutte nella finestra di dialogo **Proprietà di Data Link**.  
  
 Quando vengono stabilite connessioni implicite, per la connessione viene utilizzata l'impostazione relativa alla finalità dell'applicazione definita per la connessione padre. Analogamente, più sessioni create dalla stessa origine dati ereditano l'impostazione relativa alla finalità dell'applicazione definita per l'origine dati.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzionalità di SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)   
 [Utilizzo delle parole chiave delle stringhe di connessione con SQL Server Native Client](../../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)  
  
  
