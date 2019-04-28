---
title: Configurare Analysis Services per la delega vincolata Kerberos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 6d751477-6bf1-48b4-8833-5a631bbe7650
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 20e8a9d7b360b9b161d994805ff713840962be41
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62730894"
---
# <a name="configure-analysis-services-for-kerberos-constrained-delegation"></a>Configurare Analysis Services per la delega vincolata Kerberos
  Quando si configura Analysis Services per l'autenticazione Kerberos, è probabile che si desideri ottenere uno o entrambi i seguenti risultati: che Analysis Services rappresenti un'identità utente per l'esecuzione di query sui dati oppure che Analysis Services deleghi un'identità utente per un servizio di livello inferiore. Ogni scenario prevede requisiti di configurazione lievemente diversi. Entrambi gli scenari richiedono che si verifichi la correttezza della configurazione.  
  
> [!TIP]  
>  **[!INCLUDE[msCoName](../../includes/msconame-md.md)] Kerberos Configuration Manager per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]** è uno strumento di diagnostica che semplifica la risoluzione dei problemi di connettività correlati a Kerberos con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [Microsoft Kerberos Configuration Manager per SQL Server](https://www.microsoft.com/download/details.aspx?id=39046).  
  
 In questo argomento sono incluse le sezioni seguenti:  
  
-   [Consentire ad Analysis Services di rappresentare un'identità utente](#bkmk_impersonate)  
  
-   [Configurare Analysis Services per la delega trusted](#bkmk_delegate)  
  
-   [Verificare l'identità rappresentata o delegata](#bkmk_test)  
  
> [!NOTE]  
>  La delega non è necessaria se la connessione ad Analysis Services è un hop singolo o se per la soluzione vengono usate credenziali archiviate fornite dal servizio di archiviazione sicura di SharePoint o da Reporting Services. Se tutte le connessioni sono connessioni dirette da Excel a un database di Analysis Services oppure si basano su credenziali archiviate, è possibile usare Kerberos (o NTLM) senza dovere configurare la delega vincolata.  
>   
>  La delega vincolata Kerberos è necessaria se l'identità dell'utente deve passare tra più connessioni di computer (note come "doppio hop"). Quando l'accesso ai dati di Analysis Services dipende dall'identità dell'utente e la richiesta di connessione proviene da un servizio di delega, usare l'elenco di controllo disponibile nella sezione successiva per accertarsi che Analysis Services sia in grado di rappresentare il chiamante originale. Per altre informazioni sui flussi di autenticazione di Analysis Services, vedere la pagina relativa all' [autenticazione di Microsoft Business Intelligence e alla delega dell'identità](https://go.microsoft.com/fwlink/?LinkID=286576).  
>   
>  Ai fini della sicurezza, Microsoft consiglia sempre le deleghe vincolate rispetto a quelle non vincolate. Le deleghe non vincolate rappresentano un rischio maggiore per la sicurezza poiché consentono all'identità del servizio di rappresentare un altro utente in *qualsiasi* computer, servizio o applicazione a downstream (rispetto ai servizi definiti in modo esplicito tramite la delega vincolata).  
  
##  <a name="bkmk_impersonate"></a> Consentire ad Analysis Services di rappresentare un'identità utente  
 Per consentire ai servizi di livello superiore come Reporting Services, IIS o SharePoint di rappresentare un'identità utente in Analysis Services, è necessario configurare la delega vincolata Kerberos per tali servizi. In questo scenario, Analysis Services rappresenta l'utente corrente usando l'identità fornita dal servizio di delega e restituisce i risultati in base all'appartenenza dell'identità in questione ai ruoli.  
  
|Attività|Descrizione|  
|----------|-----------------|  
|Passaggio 1: Verificare che gli account siano idonei per la delega|Assicurarsi che gli account usati per eseguire i servizi siano provvisti delle proprietà corrette in Active Directory. Gli account di servizio in Active Directory non devono essere contrassegnati come account sensibili o essere esplicitamente esclusi dagli scenari di delega. Per altre informazioni, vedere [Informazioni sugli account utente](https://go.microsoft.com/fwlink/?LinkId=235818).<br /><br /> **\*\* Importanti \* \***  a livello generale, tutti gli account e i server devono appartenere allo stesso dominio di Active Directory o a domini trusted nella stessa foresta. Tuttavia, poiché Windows Server 2012 supporta la delega tra i limiti di dominio, è possibile configurare la delega vincolata Kerberos in un limite di dominio se il livello funzionale del dominio è Windows Server 2012. Un'altra alternativa consiste nel configurare Analysis Services per l'accesso HTTP e usare i metodi di autenticazione di IIS per la connessione client. Per altre informazioni, vedere [Configurare l'accesso HTTP ad Analysis Services in Internet Information Services &#40;IIS&#41; 8.0](configure-http-access-to-analysis-services-on-iis-8-0.md)(Autenticazione di Microsoft Business Intelligence e la delega dell'identità).|  
|Passaggio 2: Registrare il nome SPN|Prima di impostare una delega vincolata, è necessario registrare un nome SPN per l'istanza di Analysis Services. Il nome SPN di Analysis Services sarà necessario quando si configura la delega vincolata Kerberos per i servizi di livello intermedio. Per istruzioni, vedere [SPN registration for an Analysis Services instance](spn-registration-for-an-analysis-services-instance.md) .<br /><br /> Un nome SPN specifica l'identità univoca di un servizio in un dominio configurato per l'autenticazione Kerberos. Le connessioni client in cui viene usata la sicurezza integrata spesso richiedono un nome SPN nell'ambito dell'autenticazione SSPI. La richiesta viene inoltrata a un controller di dominio Active Directory e la delega vincolata Kerberos concede un ticket se al nome SPN presentato dal client corrisponde una registrazione del nome SPN in Active Directory.|  
|Passaggio 3: Configurare la delega vincolata|Dopo avere convalidato gli account che si desidera usare e averne registrato i relativi nomi SPN, il passaggio successivo consiste nel configurare i servizi di livello superiore, quali IIS, Reporting Services o i servizi Web di SharePoint, per la delega vincolata, specificando il nome SPN di Analysis Services come servizio specifico per cui la delega è consentita.<br /><br /> I servizi eseguiti in SharePoint, ad esempio Excel Services o Reporting Services in modalità SharePoint, spesso ospitano cartelle di lavoro e report che usano dati tabulari o multidimensionali di Analysis Services. La configurazione della delega vincolata per tali servizi è una normale attività necessaria per supportare l'aggiornamento dei dati da Excel Services. I collegamenti riportati di seguito forniscono istruzioni per i servizi di SharePoint e per altri servizi che con tutta probabilità presentano una richiesta di connessione dati a valle per i dati di Analysis Services:<br /><br /> [Delega dell'identità per Excel Services (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=299826) o [How to configure Excel Services in SharePoint Server 2010 for Kerberos authentication](https://support.microsoft.com/kb/2466519)<br /><br /> [Delega dell'identità per PerformancePoint Services (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=299827)<br /><br /> [Delega dell'identità per SQL Server Reporting Services (SharePoint Server 2010)](https://go.microsoft.com/fwlink/?LinkId=299828)<br /><br /> Per IIS 7.0, vedere [Configure Windows Authentication (IIS 7)](https://technet.microsoft.com/library/cc754628\(v=ws.10\).aspx) [Configurare l'autenticazione di Windows (IIS 7)] o [How to configure SQL Server 2008 Analysis Services and SQL Server 2005 Analysis Services to use Kerberos authentication](https://support.microsoft.com/kb/917409)(Come configurare SQL Server 2008 Analysis Services e SQL Server 2005 Analysis Services per usare l'autenticazione Kerberos).|  
|Passaggio 4: Test delle connessioni|Durante i test, connettersi da computer remoti usando identità differenti ed eseguire le query su Analysis Services usando le stesse applicazioni degli utenti aziendali. È possibile usare SQL Server Profiler per il monitoraggio della connessione. Nella richiesta verrà visualizzata l'identità dell'utente. Per altre informazioni, vedere [Verificare l'identità rappresentata o delegata](#bkmk_test) in questa sezione.|  
  
##  <a name="bkmk_delegate"></a> Configurare Analysis Services per la delega trusted  
 La configurazione di Analysis Services per la delega vincolata Kerberos consente al servizio di rappresentare un'identità client per un servizio di livello inferiore, ad esempio il motore di database relazionale, in modo che sia possibile eseguire query sui dati come se il client fosse connesso direttamente.  
  
 Gli scenari di delega per Analysis Services sono limitati ai modelli tabulari configurati per la modalità `DirectQuery`. Questo è l'unico scenario in cui Analysis Services può passare credenziali delegate a un altro servizio. In tutti gli altri scenari, ad esempio gli scenari di SharePoint descritti nella sezione precedente, Analysis Services si trova all'estremità ricevente della catena della delega. Per altre informazioni su DirectQuery, vedere [Modalità DirectQuery &#40;SSAS tabulare&#41;](../tabular-models/directquery-mode-ssas-tabular.md).  
  
> [!NOTE]  
>  È un luogo comune ritenere che l'archiviazione ROLAP, le operazioni di elaborazione o l'accesso a partizioni remote rappresentino i requisiti per la delega vincolata. Non è così. Tutte queste operazioni vengono eseguite direttamente dall'account del servizio (definito anche account di elaborazione) per proprio conto. La delega non è necessaria per queste operazioni in Analysis Services, visto che le autorizzazioni per tali operazioni vengono concesse direttamente all'account del servizio. Ad esempio, per consentire al servizio di elaborare i dati, è sufficiente concedere le autorizzazioni db_datareader nel database relazionale. Per altre informazioni sulle operazioni server e le autorizzazioni, vedere [Configurare gli account del servizio &#40;Analysis Services&#41;](configure-service-accounts-analysis-services.md).  
  
 In questa sezione viene illustrato come configurare Analysis Services per la delega trusted. Dopo aver completato questa attività, Analysis Services potrà passare le credenziali delegate a SQL Server, a supporto della modalità DirectQuery usata nelle soluzioni tabulari.  
  
 Prima di iniziare:  
  
-   Verificare che Analysis Services sia avviato.  
  
-   Verificare che il nome SPN registrato per Analysis Services sia valido. Per istruzioni, vedere [SPN registration for an Analysis Services instance](spn-registration-for-an-analysis-services-instance.md)  
  
 Quando entrambi i prerequisiti vengono soddisfatti, continuare con la procedura seguente. Si noti che è necessario essere un amministratore di dominio per configurare la delega vincolata.  
  
1.  In Utenti e computer di Active Directory, individuare l'account del servizio con cui viene eseguito Analysis Services. Fare clic con il pulsante destro del mouse sull'account del servizio e scegliere **Proprietà**.  
  
     A fini illustrativi, le seguenti catture di schermata usano OlapSvc e SQLSvc per rappresentare rispettivamente Analysis Services e SQL Server.  
  
     OlapSvc è l'account che verrà configurato per la delega vincolata in SQLSvc. Al termine di questa attività, OlapSvc disporrà delle autorizzazioni necessarie per passare le credenziali delegate su un ticket di servizio a SQLSvc, rappresentando il chiamante originale al momento di richiedere i dati.  
  
2.  Nella scheda Delega selezionare **Utente attendibile per la delega solo ai servizi specificati**, seguito da **Usa solo Kerberos**. Fare clic su **Aggiungi** per specificare il servizio per il quale Analysis Services è autorizzato a delegare le credenziali.  
  
     La scheda Delega è disponibile solo se l'account utente (OlapSvc) viene assegnato a un servizio (Analysis Services) e il servizio dispone di un nome SPN registrato. Per registrare il nome SPN è necessario che il servizio sia in esecuzione.  
  
     ![SSAS_Kerberos_1_AccountProperties](../media/ssas-kerberos-1-accountproperties.gif "SSAS_Kerberos_1_AccountProperties")  
  
3.  Nella pagina Aggiungi servizi, fare clic su **Utenti o computer**.  
  
     ![SSAS_Kerberos_2_](../media/ssas-kerberos-2.gif "SSAS_Kerberos_2_")  
  
4.  Nella pagina Seleziona utenti o computer immettere l'account usato per eseguire l'istanza di SQL Server che fornisce i dati ai database del modello tabulare di Analysis Services. Fare clic su **OK** per accettare l'account del servizio.  
  
     Se non è possibile selezionare l'account desiderato, verificare che SQL Server sia in esecuzione e disponga di un nome SPN registrato per tale account. Per altre informazioni sui nomi SPN per il motore di database, vedere [Registrazione di un nome dell'entità servizio per le connessioni Kerberos](../../database-engine/configure-windows/register-a-service-principal-name-for-kerberos-connections.md).  
  
     ![SSAS_Kerberos_3_SelectUsers](../media/ssas-kerberos-3-selectusers.gif "SSAS_Kerberos_3_SelectUsers")  
  
5.  L'istanza di SQL Server dovrebbe ora apparire in Aggiungi servizi. Nell'elenco saranno inoltre presente gli altri eventuali servizi che usano l'account in questione. Scegliere l'istanza di SQL Server da usare. Fare clic su **OK** per accettare l'istanza.  
  
     ![SSAS_Kerberos_4_](../media/ssas-kerberos-4.gif "SSAS_Kerberos_4_")  
  
6.  La pagina delle proprietà dell'account del servizio di Analysis Services dovrebbe apparire analoga a quella nella cattura di schermata seguente. Scegliere **OK** per salvare le modifiche.  
  
     ![SSAS_Kerberos_5_Finished](../media/ssas-kerberos-5-finished.gif "SSAS_Kerberos_5_Finished")  
  
7.  Verificare che la delega avvenga in modo corretto eseguendo la connessione a un computer client remoto, con un'identità diversa ed eseguendo una query sul modello tabulare. L'identità utente dovrebbe essere presente nella richiesta in SQL Server Profiler.  
  
##  <a name="bkmk_test"></a> Verificare l'identità rappresentata o delegata  
 Usare SQL Server Profiler per monitorare l'identità dell'utente che esegue query sui dati.  
  
1.  Avviare **SQL Server Profiler** nell'istanza di Analysis Services e quindi avviare una nuova traccia.  
  
2.  In Selezione eventi, verificare che `Audit Login` e `Audit Logout` siano selezionati nella sezione Controllo di sicurezza.  
  
3.  Connettersi ad Analysis Services tramite un servizio di applicazione (ad esempio SharePoint o Reporting Services) da un computer client remoto. L'evento Audit Login visualizzerà l'identità dell'utente che si connette ad Analysis Services.  
  
 Per un test completo è necessario usare strumenti di monitoraggio della rete in grado di acquisire richieste e risposte Kerberos. A tale scopo è possibile usare l'utilità Network Monitor (netmon.exe), con filtro per Kerberos. Per altre informazioni sull'uso di Netmon 3.4 e altri strumenti per verificare l'autenticazione Kerberos, vedere [configurazione dell'autenticazione Kerberos: Configurazione di base (SharePoint Server 2010)](https://technet.microsoft.com/library/gg502602\(v=office.14\).aspx).  
  
 Vedere inoltre [La finestra di dialogo che più disorienta in Active Directory](http://windowsitpro.com/windows/most-confusing-dialog-box-active-directory) per una descrizione dettagliata di ciascuna opzione nella scheda Delega della finestra di dialogo delle proprietà dell'oggetto di Active Directory. Questo articolo spiega inoltre come usare LDP per eseguire i test e interpretarne i relativi risultati.  
  
## <a name="see-also"></a>Vedere anche  
 [Delega dell'identità e autenticazione di Microsoft Business Intelligence](https://go.microsoft.com/fwlink/?LinkID=286576)   
 [Autenticazione reciproca tramite Kerberos](https://go.microsoft.com/fwlink/?LinkId=299283)   
 [Connetti ad Analysis Services](connect-to-analysis-services.md)   
 [SPN registration for an Analysis Services instance](spn-registration-for-an-analysis-services-instance.md)   
 [Proprietà delle stringhe di connessione &#40;Analysis Services&#41;](connection-string-properties-analysis-services.md)  
  
  
