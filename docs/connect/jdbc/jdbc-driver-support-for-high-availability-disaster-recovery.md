---
title: Supporto del driver JDBC per il ripristino di emergenza a disponibilità elevata | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 62de4be6-b027-427d-a7e5-352960e42877
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8e2df0607162f5f2cb90ff6b0525fdc530b7be66
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 12/11/2018
ms.locfileid: "53211821"
---
# <a name="jdbc-driver-support-for-high-availability-disaster-recovery"></a>Supporto di Microsoft JDBC Driver per il ripristino di emergenza a disponibilità elevata
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  In questo argomento viene illustrato il supporto di [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] per il ripristino di emergenza a disponibilità elevata - [!INCLUDE[ssHADR](../../includes/sshadr_md.md)]. Per altre informazioni su [!INCLUDE[ssHADR](../../includes/sshadr_md.md)], vedere la documentazione online di [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] .  
  
 A partire dalla versione 4.0 di [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] è possibile specificare il listener del gruppo di disponibilità (ripristino di emergenza a disponibilità elevata) nella proprietà di connessione. Se un'applicazione [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] è connessa a un database AlwaysOn che esegue il failover, dopo il failover la connessione originale viene interrotta e l'applicazione deve aprire una nuova connessione per proseguire con l'esecuzione. Le [proprietà di connessione](../../connect/jdbc/setting-the-connection-properties.md) seguenti sono state aggiunte in [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)]:  
  
-   **multiSubnetFailover**  
  
-   **applicationIntent**
 
Specificare multiSubnetFailover=true in caso di connessione al listener di un gruppo di disponibilità o a un'istanza del cluster di failover. Si noti che **multiSubnetFailover** è false per impostazione predefinita. Uso **applicationIntent** per dichiarare il tipo di carico di lavoro dell'applicazione. Nelle sezioni seguenti per altre informazioni, vedere.
 
Partire dalla versione 6.0 di Microsoft JDBC Driver per SQL Server, una nuova proprietà di connessione **transparentNetworkIPResolution** (TNIR) viene aggiunto per la connessione trasparente ai gruppi di disponibilità Always On o a un server che ha più indirizzi IP associati. Quando **transparentNetworkIPResolution** è true, il driver tenta di connettersi al primo indirizzo IP disponibile. Se il primo tentativo non riesce, il driver prova a connettersi a tutti gli indirizzi IP in parallelo fino a quando non scade il timeout, ignorando eventuali tentativi di connessione in sospeso quando uno di essi ha esito positivo.   

Si noti che:
* transparentNetworkIPResolution è true per impostazione predefinita
* transparentNetworkIPResolution viene ignorato se multiSubnetFailover è true
* transparentNetworkIPResolution viene ignorato se viene utilizzato il mirroring del database
* transparentNetworkIPResolution viene ignorato se sono presenti più di 64 indirizzi IP
* Quando transparentNetworkIPResolution è true, il primo tentativo di connessione Usa un valore di timeout di 500 ms. REST di tentativi di connessione seguire la stessa logica della funzionalità multiSubnetFailover. 

> [!NOTE]
> Se si utilizza Microsoft JDBC Driver 4.2 (o inferiore) per SQL Server e se **multiSubnetFailover** è false, il [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] tenta di connettersi al primo indirizzo IP. Se [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] non stabilisce una connessione con il primo indirizzo IP, la connessione avrà esito negativo. Tramite [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] non verranno eseguiti tentativi di connessione ad altri indirizzi IP successivi associati al server. 
> 
> 
> [!NOTE]
>  L'aumento del timeout di connessione e l'implementazione della logica di riesecuzione per le connessioni aumentano le probabilità che un'applicazione si connetta a un gruppo di disponibilità. Inoltre, poiché potrebbe non essere possibile stabilire una connessione a causa del failover di un gruppo di disponibilità, è opportuno implementare la logica di riesecuzione delle connessioni, finché non si ottiene la riconnessione.  
  
 
  
## <a name="connecting-with-multisubnetfailover"></a>Connessione con MultiSubnetFailover  
 Specificare sempre **multiSubnetFailover=true** in caso di connessione al listener di un gruppo di disponibilità di [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] o a un'istanza del cluster di failover di [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. **multiSubnetFailover** consente un failover più veloce per tutti i gruppi di disponibilità, abilita istanze del cluster di failover in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e riduce in modo significativo la durata del failover per le topologie AlwaysOn a subnet singola e a più subnet. Durante un failover su più subnet, verranno tentate connessioni in parallelo da parte del client. Durante un failover su una subnet, [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] effettua tentativi ripetuti e frequenti di connessione TCP.  
  
 La proprietà di connessione **multiSubnetFailover** indica che l'applicazione viene distribuita in un gruppo di disponibilità o nell'istanza del cluster di failover e che [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] tenterà di connettersi al database nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] primaria tramite la connessione a tutti gli indirizzi IP. Quando si specifica **MultiSubnetFailover=true** per una connessione, i ripetuti tentativi di connessione TCP del client vengono eseguiti più rapidamente rispetto agli intervalli di ritrasmissione TCP predefiniti del sistema operativo. In tal modo si abilita la riconnessione a seguito di failover di un gruppo di disponibilità AlwaysOn o un'istanza del cluster di failover AlwaysOn ed è applicabile a istanze del cluster di failover o a gruppi di disponibilità su una singola subnet o su più subnet.  
  
 Per altre informazioni sulle parole chiave delle stringhe di connessione nel [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], vedere [impostando le proprietà di connessione](../../connect/jdbc/setting-the-connection-properties.md).  
  
 La specifica di **multiSubnetFailover=true** durante la connessione a un oggetto diverso da un listener del gruppo di disponibilità o dall'istanza del cluster di failover non è supportata, perché può causare un calo delle prestazioni.  
  
 Se lo strumento di gestione della sicurezza non è installato, gli indirizzi IP virtuali vengono memorizzati nella cache di Java Virtual Machine per un periodo di tempo limitato definito, per impostazione predefinita, dall'implementazione JDK e dalle proprietà Java networkaddress.cache.ttl e networkaddress.cache.negative.ttl. Se lo strumento di gestione della sicurezza JDK è installato, gli indirizzi IP virtuali vengono memorizzati nella cache di Java Virtual Machine, ma la cache non viene aggiornata per impostazione predefinita. È consigliabile impostare "time-to-live" (networkaddress.cache.ttl) su un giorno per la cache di Java Virtual Machine. Se non si imposta il valore predefinito su un giorno (o un valore simile), il valore precedente non verrà eliminato dalla cache di Java Virtual Machine quando viene aggiunto o aggiornato un indirizzo IP virtuale. Per altre informazioni sulle TTL e networkAddress, vedere [ https://download.oracle.com/javase/6/docs/technotes/guides/net/properties.html ](https://download.oracle.com/javase/6/docs/technotes/guides/net/properties.html).  
  
 Utilizzare le linee guida seguenti per connettersi a un server in un gruppo di disponibilità o nell'istanza del cluster di failover:  
  
-   Il driver genererà un errore se il **instanceName** proprietà di connessione viene utilizzata nella stringa di connessione stessa come le **multiSubnetFailover** proprietà di connessione. Ciò riflette il fatto che SQL Browser non viene utilizzato in un gruppo di disponibilità. Tuttavia, se il **NumeroPorta** viene specificata anche proprietà di connessione, il driver ignorerà **instanceName** e usare **NumeroPorta**.  
  
-   Usare la proprietà di connessione **multiSubnetFailover** in caso di connessione a una singola subnet o a più subnet, in modo da migliorare le prestazioni.  
  
-   Per eseguire la connessione a un gruppo di disponibilità, specificare il listener del gruppo di disponibilità come server nella stringa di connessione. Ad esempio, jdbc:sqlserver://VNN1.  
  
-   La connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurata con più di 64 indirizzi IP determinerà un errore di connessione.  
  
-   Il comportamento di un'applicazione in cui viene usata la proprietà di connessione **multiSubnetFailover** non è influenzato dal tipo di autenticazione, cioè Autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Autenticazione Kerberos o Autenticazione di Windows.  
  
-   Aumentare il valore di **loginTimeout** per adattarlo alla durata del failover e ridurre il numero di nuovi tentativi di connessione dell'applicazione.  
  
-   Le transazioni distribuite non sono supportate.  
  
 Se il routing di sola lettura non è attivo, non è possibile stabilire una connessione a un percorso di replica secondaria in un gruppo di disponibilità nelle situazioni seguenti:  
  
1.  Se il percorso di replica secondaria non è configurato per accettare le connessioni.  
  
2.  Se un'applicazione usa **applicationIntent=ReadWrite** (vedere di seguito) e il percorso di replica secondaria è configurato per l'accesso in sola lettura.  
  
 Una connessione non riesce se una replica primaria è configurata per rifiutare i carichi di lavoro in sola lettura e la stringa di connessione contiene **ApplicationIntent=ReadOnly**.  
  
## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>Aggiornamento per l'utilizzo di cluster su più subnet dal mirroring del database  
 Se si aggiorna un'applicazione [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] che usa il mirroring del database in uno scenario su più subnet, è necessario rimuovere la proprietà di connessione **failoverPartner** e sostituirla con **multiSubnetFailover** impostata su **true**, nonché sostituire il nome server nella stringa di connessione con un listener del gruppo di disponibilità. Se in una stringa di connessione vengono usati **failoverPartner** e **multiSubnetFailover=true** il driver genererà un errore. Se tuttavia in una stringa di connessione vengono usati **failoverPartner** e **multiSubnetFailover=false** (o **ApplicationIntent=ReadWrite**), l'applicazione userà il mirroring del database.  
  
 Il driver restituirà un errore se il mirroring del database viene usato nel database primario nel gruppo di disponibilità e se **multiSubnetFailover=true** viene usato nella stringa di connessione a un database primario anziché a un listener del gruppo di disponibilità.  


[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="new-methods-supporting-multisubnetfailover-and-applicationintent"></a>Nuovi metodi che supportano multiSubnetFailover e applicationIntent  
 I metodi seguenti forniscono accesso programmatico per il **multiSubnetFailover**, **applicationIntent** e **transparentNetworkIPResolution** stringa di connessione parole chiave:  
  
-   [SQLServerDataSource.getApplicationIntent](../../connect/jdbc/reference/getapplicationintent-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.setApplicationIntent](../../connect/jdbc/reference/setapplicationintent-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.getMultiSubnetFailover](../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md)  
  
-   [SQLServerDataSource.setMultiSubnetFailover](../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)  
  
-   [SQLServerDriver.getPropertyInfo](../../connect/jdbc/reference/getpropertyinfo-method-sqlserverdriver.md)  

-   SQLServerDataSource.setTransparentNetworkIPResolution

-   SQLServerDataSource.getTransparentNetworkIPResolution
  
 Il **getMultiSubnetFailover**, **setMultiSubnetFailover**, **getApplicationIntent**, **setApplicationIntent**, **getTransparentNetworkIPResolution** e **setTransparentNetworkIPResolution** vengono aggiunti anche i metodi [classi di SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md), [ Classe SQLServerConnectionPoolDataSource](../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md), e [classe SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md).  
  
## <a name="ssl-certificate-validation"></a>Convalida del certificato SSL  
 Un gruppo di disponibilità è costituito da più server fisici. In [!INCLUDE[jdbc_40](../../includes/jdbc_40_md.md)] è stato aggiunto il supporto per **Subject Alternate Name** nei certificati SSL, in modo che più host possano essere associati allo stesso certificato. Per altre informazioni su SSL, vedere [informazioni sul supporto SSL](../../connect/jdbc/understanding-ssl-support.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Connessione a SQL Server con il driver JDBC](../../connect/jdbc/connecting-to-sql-server-with-the-jdbc-driver.md)   
 [Impostazione delle proprietà di connessione](../../connect/jdbc/setting-the-connection-properties.md)  
  
  
