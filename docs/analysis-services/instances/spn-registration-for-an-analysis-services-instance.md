---
title: Registrazione del nome SPN per un'istanza di Analysis Services | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7b4516470b1b55c697cbfee065dbf53c3187a6a1
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52526489"
---
# <a name="spn-registration-for-an-analysis-services-instance"></a>Registrazione del nome SPN per un'istanza di Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Un nome SPN (Service Principle Name) identifica in modo univoco un'istanza del servizio in un dominio Active Directory quando Kerberos viene usato per l'autenticazione reciproca delle identità del servizio e del client. Il nome SPN è associato all'account di accesso con cui viene eseguita l'istanza del servizio.  
  
 Per le applicazioni client che si connettono ad Analysis Services tramite l'autenticazione Kerberos, le librerie client di Analysis Services creano un nome SPN usando il nome host dalla stringa di connessione e altre variabili note, ad esempio la classe del servizio, che vengono risolte in qualsiasi versione specificata di Analysis Services.  
  
 Per eseguire l'autenticazione reciproca, i nomi SPN creati dal client devono corrispondere a un oggetto SPN corrispondente in un controller di dominio Active Directory. Pertanto potrebbe essere necessario registrare più nomi SPN per una singola istanza di Analysis Services per includere tutte le modalità con cui un utente può specificare il nome host in una stringa di connessione. Ad esempio, probabilmente sono necessari due nomi SPN per gestire il nome di dominio completo (FQDN) di un server e il nome breve di un computer. Una corretta registrazione del nome SPN di Analysis Services è essenziale per una valida connessione. Se il nome SPN è inesistente, in formato non valido o duplicato, la connessione avrà esito negativo.  
  
 La registrazione del nome SPN è un'attività manuale eseguita dall'amministratore di Analysis Services. Diversamente da quanto accade per il motore di database di SQL Server, in Analysis Services non viene mai eseguita la registrazione automatica del nome SPN all'avvio del servizio. È necessaria la registrazione manuale quando Analysis Services viene eseguito con l'account virtuale predefinito, un account utente di dominio o un account predefinito, compreso un SID per servizio.  
  
 La registrazione del nome SPN non è necessaria se il servizio viene eseguito con un account del servizio gestito predefinito creato da un amministratore di dominio. Si noti che a seconda del livello funzionale del dominio, è possibile che per registrare un nome SPN siano necessarie le autorizzazioni di amministratore di dominio.  
  
> [!TIP]  
>  **[!INCLUDE[msCoName](../../includes/msconame-md.md)] Kerberos Configuration Manager per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** è uno strumento di diagnostica che semplifica la risoluzione dei problemi di connettività correlati a Kerberos con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Microsoft Kerberos Configuration Manager per SQL Server](http://www.microsoft.com/download/details.aspx?id=39046).  
  
 In questo argomento sono incluse le sezioni seguenti:  
  
 [Quando è necessaria la registrazione del nome SPN](#bkmk_scnearios)  
  
 [Formato SPN per Analysis Services](#bkmk_SPNSyntax)  
  
 [Registrazione del nome SPN per un account virtuale](#bkmk_virtual)  
  
 [Registrazione del nome SPN per un account di dominio](#bkmk_domain)  
  
 [Registrazione del nome SPN per un account predefinito](#bkmk_builtin)  
  
 [Registrazione del nome SPN per un'istanza denominata](#bkmk_spnNamed)  
  
 [Registrazione del nome SPN per un cluster SSAS](#bkmk_spnCluster)  
  
 [Registrazione del nome SPN per le istanze di SSAS configurate per l'accesso HTTP](#bkmk_spnHTTP)  
  
 [Registrazione del nome SPN per le istanze di SSAS in attesa su porte fisse](#bkmk_spnFixedPorts)  
  
##  <a name="bkmk_scnearios"></a> Quando è necessaria la registrazione del nome SPN  
 Qualsiasi connessione client che specifica "SSPI = Kerberos" nella connessione stringa introdurrà i requisiti di registrazione SPN per un'istanza di Analysis Services.  
  
 La registrazione del nome SPN è necessaria nei casi seguenti. Per informazioni più dettagliate, vedere [Configure Analysis Services for Kerberos constrained delegation](../../analysis-services/instances/configure-analysis-services-for-kerberos-constrained-delegation.md).  
  
-   È necessaria la delega dell'identità per far passare l'identità dell'utente dall'applicazione client o da un servizio di livello intermedio ad Analysis Services. La delega dell'identità viene in genere usata quando vengono definiti filtri o autorizzazioni per utente in oggetti specifici.  
  
     Uno scenario comune relativo alla delega dell'identità è quando si configurano servizi di livello intermedio, ad esempio Excel Services o Reporting Services, per la delega vincolata al fine di rappresentare l'identità di un utente per il recupero dati in Analysis Services. Per supportare questo comportamento, è necessario fornire un nome SPN di Analysis Services come servizio di destinazione quando si configura Excel Services o Reporting Services per la delega vincolata.  
  
-   Analysis Services delega un'identità utente quando vengono recuperati i dati da un database relazionale di SQL Server per i database tabulari tramite la modalità DirectQuery. Questo è l'unico scenario in cui Analysis Services delegherà l'identità utente a un altro servizio.  
  
##  <a name="bkmk_SPNSyntax"></a> Formato SPN per Analysis Services  
 Usare **setspn** per registrare un nome SPN. Nei sistemi operativi più recenti, **setspn** viene installato come utilità di sistema. Per altre informazioni, vedere [SetSPN](http://technet.microsoft.com/library/cc731241\(WS.10\).aspx).  
  
 Nella tabella seguente vengono descritte le singole parti di un nome SPN di Analysis Services.  
  
|Elemento|Descrizione|  
|-------------|-----------------|  
|Classe del servizio|MSOLAPSvc.3 identifica il servizio come istanza di Analysis Services. L'estensione .3 è un riferimento alla versione del protocollo XMLA-over-TCP/IP usato nelle trasmissioni di Analysis Services. È indipendente dalla versione del prodotto. Di conseguenza, MSOLAPSvc.3 è la classe del servizio corretta per SQL Server 2005, 2008, 2008 R2, 2012 e per qualsiasi versione successiva di Analysis Services finché il protocollo non viene revisionato.|  
|Nome host|Viene identificato il computer in cui viene eseguito il servizio. Può trattarsi di un nome di dominio completo o di un nome NetBIOS. È consigliabile registrare un nome SPN per entrambi.<br /><br /> Quando si registra un nome SPN per il nome NetBIOS di un server, accertarsi di usare `SetupSPN -S` per verificare eventuali registrazioni duplicate. Per i nomi NetBIOS non viene garantita l'univocità nella foresta e l'esistenza di una registrazione duplicata del nome SPN causerà un errore di connessione.<br /><br /> Per i cluster con carico bilanciato di Analysis Services, il nome host deve essere il nome virtuale assegnato al cluster.<br /><br /> Non creare mai un nome SPN usando l'indirizzo IP. Kerberos usano le funzionalità di risoluzione DNS del dominio. Specificando un indirizzo IP si ignora tale funzionalità.|  
|Numero di porta|Sebbene il numero di porta faccia parte della sintassi del nome SPN, non specificare mai un numero di porta quando si registra un nome SPN di Analysis Services. I due punti (:), in genere utilizzati per fornire un numero di porta nella sintassi standard del nome SPN, vengono utilizzati da Analysis Services per specificare il nome dell'istanza. Per un'istanza di Analysis Services, si presume che la porta usata sia la porta predefinita (TCP 2383) o una porta assegnata dal servizio SQL Server Browser (TCP 2382).|  
|Nome istanza|Analysis Services è un servizio replicabile che è possibile installare più volte nello stesso computer. Ogni istanza viene identificata tramite il nome.<br /><br /> Il nome dell'istanza è preceduto dai due punti (:). Ad esempio, per un computer host denominato SRV01 e un'istanza denominata SSAS-Tabular, il nome SPN sarà SRV01:SSAS-Tabular.<br /><br /> Si noti che la sintassi per specificare un'istanza denominata di Analysis Services differisce da quella usata da altre istanze di SQL Server. Altri servizi usano una barra rovesciata (\) per aggiungere il nome dell'istanza in un nome SPN.|  
|Account servizio|Si tratta dell'account di avvio del servizio Windows **MSSQLServerOLAPService** . Può essere un account utente di dominio di Windows, un account virtuale, un account dei servizi gestiti o un account predefinito, ad esempio un SID per servizio, NetworkService o LocalSystem. Un account utente di dominio di Windows possono essere formattate come dominio\utente o user@domain.|  
  
##  <a name="bkmk_virtual"></a> Registrazione del nome SPN per un account virtuale  
 Gli account virtuali sono il tipo di account predefinito per i servizi di SQL Server. L'account virtuale è **NT Service\MSOLAPService** per un'istanza predefinita e **NT Service\MSOLAP$**\<nome-istanza > per un'istanza denominata.  
  
 Come indicato dal nome, questi account non esistono in Active Directory. Un account virtuale esiste solo nel computer locale. Quando si effettua la connessione a servizi, applicazioni o dispositivi esterni, l'operazione viene eseguita tramite l'account del computer locale. Per questo motivo, la registrazione di un nome SPN per Analysis Services in esecuzione con un account virtuale è in effetti la registrazione di un nome SPN per l'account del computer.  
  
 **Sintassi di esempio per un'istanza predefinita in esecuzione come NT Service\MSOLAPService**  
  
 In questo esempio viene mostrata la sintassi **setspn** per un'istanza predefinita di Analysis Services in esecuzione con l'account virtuale predefinito. Nell'esempio, il nome host del computer è **AW-SRV01**. Come accennato, per la registrazione del nome SPN deve essere specificato l' *account del computer* anziché l'account virtuale, **NT Service\MSOLAPService**.  
  
```  
Setspn -s MSOLAPSvc.3/AW-SRV01.AdventureWorks.com AW-SRV01  
```  
  
> [!NOTE]  
>  Ricordarsi di creare due registrazioni del nome SPN, una per il nome host NetBIOS e una seconda per il nome di dominio completo dell'host. In applicazioni client differenti vengono usare convenzioni di nomi host diversi per la connessione ad Analysis Services. La presenza di due registrazioni del nome SPN garantisce che sono state considerate entrambe le versioni del nome host.  
  
 **Sintassi di esempio per un'istanza denominata in esecuzione come NT Service\MSOLAP$\<nome-istanza >**  
  
 In questo esempio viene mostrata la sintassi **setspn** per un'istanza denominata in esecuzione con l'account virtuale predefinito. Nell'esempio, il nome host del computer è **AW-SRV02** e il nome dell'istanza è **AW-FINANCE**. Anche in questo caso è l'account del computer specificato per il nome SPN, anziché l'account virtuale **NT Service\MSOLAP$**\<nome-istanza >.  
  
```  
Setspn -s MSOLAPSvc.3/AW-SRV02.AdventureWorks.com:AW-FINANCE AW-SRV02  
```  
  
##  <a name="bkmk_domain"></a> Registrazione del nome SPN per un account di dominio  
 È pratica comune usare un account di dominio per eseguire un'istanza di Analysis Services.  
  
 Per istanze di Analysis Services eseguite in una rete o in un cluster hardware con carico bilanciato, è necessario un account di dominio, con ciascuna istanza del cluster in esecuzione con lo stesso account di dominio.  
  
 **Sintassi di esempio per un'istanza predefinita in esecuzione come utente di dominio**  
  
 Questo esempio mostra la sintassi **setspn** per un'istanza predefinita di Analysis Services in esecuzione con un account utente di dominio, **SSAS-Service**, nel dominio AdventureWorks.  
  
```  
Setspn -s msolapsvc.3/AW-SRV01.Adventureworks.com AdventureWorks\SSAS-Service  
```  
  
> [!TIP]  
>  Verificare se il nome SPN è stato creato per il server Analysis Services eseguendo `Setspn -L <domain account>` o `Setspn -L <machinename>`, a seconda della modalità di registrazione del nome SPN. Dovrebbe essere msolapsvc.3/<nomehost\<hostname > nell'elenco.  
  
##  <a name="bkmk_builtin"></a> Registrazione del nome SPN per un account predefinito  
 Anche se questa pratica non è consigliata, le installazioni precedenti di Analysis Services sono talvolta configurate per l'esecuzione con account predefiniti come Servizio di rete, Servizio locale o Sistema locale.  
  
 **Sintassi di esempio per un'istanza predefinita in esecuzione con un account predefinito**  
  
 La registrazione del nome SPN per un servizio in esecuzione con un account predefinito o SID per servizio è equivalente alla sintassi SPN usata per l'account virtuale. Anziché il nome account, usare l'account del computer:  
  
```  
Setspn -s MSOLAPSvc.3/AW-SRV01.AdventureWorks.com AW-SRV01  
```  
  
##  <a name="bkmk_spnNamed"></a> Registrazione del nome SPN per un'istanza denominata  
 Nelle istanze denominate di Analysis Services vengono usate assegnazioni di porta dinamiche che vengono rilevate dal servizio SQL Server Browser. Quando si usano un'istanza denominata, registrare un nome SPN sia per il servizio SQL Server Browser sia per l'istanza denominata di Analysis Services. Per altre informazioni, vedere [È necessario un nome SPN per il servizio SQL Server Browser quando si stabilisce una connessione a un'istanza denominata di SQL Server Analysis Services o di SQL Server](http://support.microsoft.com/kb/950599).  
  
 **Esempio di sintassi SPN per il servizio SQL Server Browser in esecuzione come LocalService**  
  
 La classe del servizio è **MSOLAPDisco.3**. Per impostazione predefinita, questo servizio viene eseguito come NT AUTHORITY\LocalService, pertanto la registrazione del nome SPN viene impostata per l'account del computer. In questo esempio, l'account del computer è **AW-SRV01**, che corrisponde al nome del computer.  
  
```  
Setspn -S MSOLAPDisco.3/AW-SRV01.AdventureWorks.com AW-SRV01  
```  
  
##  <a name="bkmk_spnCluster"></a> Registrazione del nome SPN per un cluster SSAS  
 Per i cluster di failover Analysis Services, il nome host deve essere il nome virtuale assegnato al cluster. Si tratta del nome di rete SQL Server, specificato durante l'installazione di SQL Server quando si è installato Analysis Services in un cluster WSFC esistente. È possibile trovare questo nome in Active Directory, oltre che in **Gestione cluster di failover** | **Ruolo** | **Risorse** . Il nome del server nella scheda Risorse è il nome da usare come "nome virtuale" nel comando SPN.  
  
 **Sintassi SPN per un cluster di Analysis Services**  
  
```  
Setspn -s msolapsvc.3/<virtualname.FQDN > <domain user account>  
```  
  
 I nodi di un cluster Analysis Services devono usare la porta predefinita (TCP 2383) e devono essere eseguiti con lo stesso account utente di dominio in modo che ogni nodo abbia lo stesso SID. Per altre informazioni, vedere [Come eseguire il clustering di SQL Server Analysis Services](http://msdn.microsoft.com/library/dn736073.aspx) .  
  
##  <a name="bkmk_spnHTTP"></a> Registrazione del nome SPN per le istanze di SSAS configurate per l'accesso HTTP  
 A seconda dei requisiti della soluzione, è possibile configurare Analysis Services per l'accesso HTTP. Se la soluzione include IIS come componente di livello intermedio e l'autenticazione Kerberos è un requisito della soluzione, potrebbe essere necessario registrare manualmente un nome SPN per IIS. Per altre informazioni, vedere "Configurare le impostazioni del computer che esegue IIS" nella [come configurare SQL Server 2008 Analysis Services e SQL Server 2005 Analysis Services per usare l'autenticazione Kerberos](http://support.microsoft.com/kb/917409).  
  
 Per quanto riguarda la registrazione del nome SPN per l'istanza di Analysis Services, non esiste alcuna differenza tra un'istanza configurata per TCP o HTTP. La connessione ad Analysis Services da IIS, usando l'estensione ISAPI MSMDPUMP, è sempre TCP.  
  
 Pertanto, per registrare il nome SPN è possibile usare le istruzioni delle sezioni precedenti per l'istanza predefinita o denominata. Quando si specifica il nome host, assicurarsi di usare il nome host specificato nel file msmdpump.ini quanto è stato configurato il servizio per l'accesso HTTP.  
  
 Per altre informazioni sull'accesso HTTP, vedere [Configurare l'accesso HTTP ad Analysis Services in Internet Information Services &#40;IIS&#41; 8.0](../../analysis-services/instances/configure-http-access-to-analysis-services-on-iis-8-0.md).  
  
##  <a name="bkmk_spnFixedPorts"></a> Registrazione del nome SPN per le istanze di SSAS in attesa su porte fisse  
 Non è possibile specificare un numero di porta nella registrazione del nome SPN di Analysis Services. Se Analysis Services è stato installato come istanza predefinita ed è stato configurato per l'attesa su una porta fissa, è necessario a questo punto configurarlo per l'attesa sulla porta predefinita (TCP 2383). Per le istanze denominate, è necessario usare il servizio SQL Server Browser e le assegnazioni di porta dinamiche.  
  
 Un'istanza di Analysis Services può restare in ascolto solo su una singola porta. L'utilizzo di più porte non è supportato. Per altre informazioni sulla configurazione della porta, vedere [Configure the Windows Firewall to Allow Analysis Services Access](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Delega dell'identità e autenticazione di Microsoft Business Intelligence](http://go.microsoft.com/fwlink/?LinkID=286576)   
 [Autenticazione reciproca tramite Kerberos](http://go.microsoft.com/fwlink/?LinkId=299283)   
 [Come configurare SQL Server 2008 Analysis Services e SQL Server 2005 Analysis Services per usare l'autenticazione Kerberos](http://support.microsoft.com/kb/917409)   
 [Sintassi SetSPN dei nomi dell'entità servizio (SPN, Setspn.exe)](http://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx)   
 [Quale nome SPN usare e come si crea](http://social.technet.microsoft.com/wiki/contents/articles/717.service-principal-names-spns-setspn-syntax-setspn-exe.aspx)   
 [SetSPN](http://technet.microsoft.com/library/cc731241\(WS.10\).aspx)   
 [Guida dettagliata agli account di servizio](http://technet.microsoft.com/library/dd548356\(WS.10\).aspx)   
 [Configurare account di servizio e autorizzazioni di Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)   
 [Come usare i nomi SPN quando si configurano le applicazioni Web ospitate in Internet Information Services](http://support.microsoft.com/kb/929650)   
 [quali sono le novità negli account di servizio](http://technet.microsoft.com/library/dd367859\(WS.10\).aspx)   
 [Configurare l'autenticazione Kerberos per prodotti SharePoint 2010 (white paper)](http://technet.microsoft.com/library/ff829837.aspx)  
  
  
