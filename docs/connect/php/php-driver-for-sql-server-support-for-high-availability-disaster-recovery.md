---
title: Supporto per la disponibilità elevata, ripristino di emergenza per i driver Microsoft per PHP per SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 07/31/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 73a80821-d345-4fea-b076-f4aabeb4af3e
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 5e0ad826c8846330c7207b14ac2344687563bbfa
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66797104"
---
# <a name="support-for-high-availability-disaster-recovery"></a>Supporto per il ripristino di emergenza a disponibilità elevata
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

In questo argomento viene trattato il supporto di [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] (aggiunto nella versione 3.0) per il ripristino di emergenza a disponibilità elevata -- [!INCLUDE[ssHADR](../../includes/sshadr_md.md)].  Il supporto [!INCLUDE[ssHADR](../../includes/sshadr_md.md)] è stato aggiunto in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]. Per altre informazioni su [!INCLUDE[ssHADR](../../includes/sshadr_md.md)], vedere la documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
Nella versione 3.0 di [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] è possibile specificare il listener di un gruppo di disponibilità (per ripristino di emergenza a disponibilità elevata) nella proprietà di connessione. Se un'applicazione [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] è connessa a un database AlwaysOn che esegue il failover, dopo il failover la connessione originale viene interrotta e l'applicazione deve aprire una nuova connessione per proseguire con l'esecuzione.  
  
Se non si sta eseguendo la connessione a un listener del gruppo di disponibilità e se più indirizzi IP sono associati a un nome host, in [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] viene eseguita l'iterazione di tutti gli indirizzi IP associati alla voce DNS. Questa operazione può richiedere tempi lunghi se il primo indirizzo IP restituito dal server DNS non è associato ad alcuna scheda di interfaccia di rete. Durante la connessione a un listener di un gruppo di disponibilità, [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] effettua tentativi connessione a tutti gli indirizzi IP in parallelo. Se un tentativo riesce, tutti gli altri tentativi di connessione in sospeso vengono ignorati.  
  
> [!NOTE]  
> L'aumento del timeout di connessione e l'implementazione della logica di riesecuzione per le connessioni aumentano le probabilità che un'applicazione si connetta a un gruppo di disponibilità. Inoltre, poiché potrebbe non essere possibile stabilire una connessione a causa del failover di un gruppo di disponibilità, è opportuno implementare la logica di riesecuzione delle connessioni, finché non si ottiene la riconnessione.  
  
## <a name="connecting-with-multisubnetfailover"></a>Connessione con MultiSubnetFailover  
La proprietà di connessione **MultiSubnetFailover** indica che l'applicazione viene distribuita in un gruppo di disponibilità o nell'istanza del cluster di failover e che [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] effettua un tentativo di connessione al database nell'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] primaria tramite la connessione a tutti gli indirizzi IP. Quando si specifica **MultiSubnetFailover=true** per una connessione, i ripetuti tentativi di connessione TCP del client vengono eseguiti più rapidamente rispetto agli intervalli di ritrasmissione TCP predefiniti del sistema operativo. In tal modo si abilita la riconnessione a seguito di failover di un gruppo di disponibilità AlwaysOn o un'istanza del cluster di failover AlwaysOn ed è applicabile a istanze del cluster di failover o a gruppi di disponibilità su una singola subnet o su più subnet.  
  
Specificare sempre **MultiSubnetFailover=true** in caso di connessione a un listener del gruppo di disponibilità di SQL Server 2012 o a un'istanza del cluster di failover di SQL Server 2012. **MultiSubnetFailover** consente un failover più veloce per tutti i gruppi di disponibilità, permette di abilitare l'istanza del cluster di failover in SQL Server 2012 e riduce notevolmente la durata del failover per le topologie AlwaysOn singole e su più subnet. Durante un failover su più subnet, verranno tentate connessioni in parallelo da parte del client. Durante un failover su una subnet, [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] effettua tentativi ripetuti e frequenti di connessione TCP.  
  
Per altre informazioni sulle parole chiave delle stringhe di connessione in [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)], vedere [le opzioni di connessione](../../connect/php/connection-options.md).  
  
La specifica di **MultiSubnetFailover=true** durante la connessione a un oggetto diverso da un listener del gruppo di disponibilità o dall'istanza del cluster di failover non è supportata, perché può causare un calo delle prestazioni.  
  
Utilizzare le linee guida seguenti per connettersi a un server in un gruppo di disponibilità:  
  
-   Usare la proprietà di connessione **MultiSubnetFailover** in caso di connessione a una singola subnet o a più subnet, in modo da migliorare le prestazioni.  
  
-   Per eseguire la connessione a un gruppo di disponibilità, specificare il listener del gruppo di disponibilità come server nella stringa di connessione.  
  
-   La connessione a un'istanza di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] configurata con più di 64 indirizzi IP determinerà un errore di connessione.  
  
-   Il comportamento di un'applicazione in cui viene usata la proprietà di connessione **MultiSubnetFailover** non è influenzato dal tipo di autenticazione, cioè dall'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], dall'autenticazione Kerberos, o dall’autenticazione di Windows.  
  
-   Aumentare il valore di **loginTimeout** per adattarlo alla durata del failover e ridurre il numero di nuovi tentativi di connessione dell'applicazione.  
  
-   Le transazioni distribuite non sono supportate.  
  
Se il routing di sola lettura non è attivo, non è possibile stabilire una connessione a un percorso di replica secondaria in un gruppo di disponibilità nelle situazioni seguenti:  
  
- Se il percorso di replica secondaria non è configurato per accettare le connessioni.  
  
- Se un'applicazione usa **ApplicationIntent=ReadWrite** (vedere di seguito) e il percorso di replica secondaria è configurato per l'accesso in sola lettura.  
  
Una connessione non riesce se una replica primaria è configurata per rifiutare i carichi di lavoro in sola lettura e la stringa di connessione contiene **ApplicationIntent=ReadOnly**.  

## <a name="transparent-network-ip-resolution-tnir"></a>Risoluzione dell'IP di rete trasparente (TNIR)

Transparent Network IP risoluzione (TNIR) è una revisione della funzionalità MultiSubnetFailover esistente. Il primo problema è risolto IP del nome host non risponde e non vi sono più indirizzi IP associati al nome host riguarda la sequenza di connessione del driver. Insieme a MultiSubnetFailover forniscono le sequenze di quattro connessioni seguenti: 

- TNIR abilitato e disabilitato MultiSubnetFailover: tentativo di un indirizzo IP, seguito da tutti gli indirizzi IP in parallelo
- TNIR abilitato a & bilitato MultiSubnetFailover: tutti gli indirizzi IP vengono eseguiti in parallelo
- Disattivato TNIR & MultiSubnetFailover disabilitato: tutti gli indirizzi IP vengono eseguiti uno dopo l'altro
- Disattivato TNIR a & bilitato MultiSubnetFailover: tutti gli indirizzi IP vengono eseguiti in parallelo

TNIR è abilitato per impostazione predefinita e MultiSubnetFailover è disabilitata per impostazione predefinita.

Questo è un esempio di abilitazione TNIR sia MultiSubnetFailover Usa il driver PDO_SQLSRV:

```
<?php
$serverName = "yourservername";
$username = "yourusername";
$password = "yourpassword";
$connectionString = "sqlsrv:Server=$serverName; TransparentNetworkIPResolution=Enabled; MultiSubnetFailover=yes";
try {
    $conn = new PDO($connectionString, $username, $password, array(PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION));
    // your code 
    // more of your code
    // when done, close the connection
    unset($conn);
} catch(PDOException $e) {
    print_r($e->errorInfo);
}
?>
```

## <a name="upgrading-to-use-multi-subnet-clusters-from-database-mirroring"></a>Aggiornamento per l'utilizzo di cluster su più subnet dal mirroring del database  
Si verificherà un errore di connessione se nella stringa di connessione sono presenti le parole chiave di connessione **MultiSubnetFailover** e **Failover_Partner**. Si verificherà un errore anche se viene usato **MultiSubnetFailover** e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] restituisce una risposta del partner di failover in cui viene indicato che fa parte di una coppia del mirroring del database.  
  
Se si aggiorna un'applicazione [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] che usa il mirroring del database in uno scenario su più subnet, è necessario rimuovere la proprietà di connessione **Failover_Partner** e sostituirla con **MultiSubnetFailover** impostata su **Yes**, nonché sostituire il nome del server nella stringa di connessione con un listener del gruppo di disponibilità. Se in una stringa di connessione vengono usati **Failover_Partner** e **MultiSubnetFailover=true** il driver genera un errore. Se tuttavia in una stringa di connessione vengono usati **Failover_Partner** e **MultiSubnetFailover=false** (o **ApplicationIntent=ReadWrite**) l'applicazione usa il mirroring del database.  
  
Il driver restituisce un errore se il mirroring del database viene usato nel database primario nel gruppo di disponibilità e se **MultiSubnetFailover=true** viene usato nella stringa di connessione a un database primario anziché a un listener del gruppo di disponibilità.  


[!INCLUDE[specify-application-intent_read-only-routing](~/includes/paragraph-content/specify-application-intent-read-only-routing.md)]


## <a name="see-also"></a>Vedere anche  
[Connessione al server](../../connect/php/connecting-to-the-server.md)  
  
