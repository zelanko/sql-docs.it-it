---
title: Informazioni su prenotazioni e registrazione URL (Gestione configurazione SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- URL reservations
- URL registration
- Report Server service, URL reservations
ms.assetid: c2c460c3-e749-4efd-aa02-0f8a98ddbc76
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: f81ac60dbd6ea315bab70d2f65e4953b456f3034
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59968287"
---
# <a name="about-url-reservations-and-registration--ssrs-configuration-manager"></a>Informazioni su prenotazioni e registrazione URL (Gestione configurazione SSRS)
  Gli URL per le applicazioni di Reporting Services vengono definiti come prenotazioni URL in HTTP.SYS. Una prenotazione URL definisce la sintassi di un endpoint dell'URL in un'applicazione Web. Le prenotazioni URL vengono definite sia per il servizio Web ReportServer sia per Gestione report quando si configurano le applicazioni nel server di report. Le prenotazioni URL vengono create automaticamente quando si configurano gli URL tramite il programma di installazione o lo strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :  
  
-   Le prenotazioni URL vengono create dal programma di installazione utilizzando valori predefiniti. Se il programma di installazione utilizza la configurazione predefinita, vengono prenotati due URL, uno per il servizio Web ReportServer e l'altro per Gestione report. È possibile utilizzare lo strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per aggiungere altri URL o modificare quelli predefiniti creati dal programma di installazione.  
  
-   Lo strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] crea una prenotazione URL basata sull'URL specificato nella pagina **URL servizio Web** o **URL Gestione report** dello strumento.  
  
 Sia il programma di installazione che lo strumento assegneranno inoltre autorizzazioni per l'URL al servizio del server di report, verificheranno la presenza di istanze duplicate e aggiungeranno la prenotazione URL a HTTP.SYS. Non creare o modificare mai una prenotazione URL di Reporting Services utilizzando direttamente HttpCfg.exe o un altro strumento. Se si ignora un passaggio o si imposta un valore non valido, si verificheranno problemi di difficile identificazione o correzione.  
  
> [!NOTE]  
>  HTTP.SYS è un componente del sistema operativo che rimane in attesa delle richieste di rete e ne esegue quindi il routing a una coda di richieste. In questa versione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]HTTP.SYS definisce e gestisce la coda di richieste per il servizio Web ReportServer e per Gestione report. Internet Information Services (IIS) non viene più utilizzato per ospitare le applicazioni di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] o accedervi. Per ulteriori informazioni sulla funzionalità HTTP.SYS, vedere [HTTP Server API](https://go.microsoft.com/fwlink/?LinkId=92652) nel sito Web MSDN.  
  
##  <a name="ReportingServicesURLs"></a> URL in Reporting Services  
 In un'installazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è possibile accedere agli strumenti, alle applicazioni e agli elementi seguenti tramite URL:  
  
-   servizio Web ReportServer  
  
-   Gestione report  
  
-   Generatore report  
  
-   Report pubblicati in un server di report  
  
 Non accedere tramite URL come elementi autonomi ad altri elementi pubblicati indirizzabili tramite URL, quali modelli e origini dati condivise. Se presentati in una finestra del browser, tali elementi non vengono visualizzati in un formato significativo dal server di report.  
  
> [!NOTE]  
>  In questo argomento non viene descritto l'accesso tramite URL a Generatore report o a report specifici archiviati nel server di report. Per altre informazioni sull'accesso tramite URL a tali elementi, vedere [Accedere agli elementi del server di report usando l'accesso tramite URL](../access-report-server-items-using-url-access.md) nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
##  <a name="URLreservation"></a> Prenotazione e registrazione URL  
 Una prenotazione URL definisce gli URL che possono essere utilizzati per accedere a un'applicazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] riserverà uno o più URL per il servizio Web ReportServer e per Gestione report in HTTP.SYS e li registra quindi all'avvio del servizio. Gli URL di Generatore report e dei report sono basati sulla prenotazione URL del servizio Web ReportServer. Aggiungendo parametri all'URL, è possibile aprire Generatore report o i report tramite il servizio Web. Le prenotazioni e la registrazione vengono forniti da HTTP.SYS. Per ulteriori informazioni, vedere [Namespace Reservations, Registration, and Routing](https://go.microsoft.com/fwlink/?LinkId=92653) nel sito Web MSDN.  
  
 Una*prenotazione URL* è un processo tramite cui un endpoint dell'URL a un'applicazione Web viene creato e archiviato in HTTP.SYS. HTTP.SYS è il repository comune di tutte le prenotazioni URL definite in un computer e determina un set di regole comuni che garantiscono l'univocità delle prenotazioni URL.  
  
 La*registrazione URL* viene eseguita all'avvio del servizio. Viene creata la coda di richieste e HTTP.SYS inizia a eseguire il routing delle richieste alla coda. Prima che le richieste indirizzate all'endpoint URL vengano aggiunte alla coda, è necessario che l'endpoint sia registrato. All'avvio del servizio del server di report, verranno registrati tutti gli URL prenotati per tutte le applicazioni attivate. Di conseguenza, il servizio Web deve essere attivato affinché venga eseguita la registrazione. Se si imposta la proprietà **WebServiceAndHTTPAccessEnabled** su **False** nel facet Configurazione superficie di attacco per Reporting Services della gestione basata su criteri, l'URL per il servizio Web non verrà registrato all'avvio del servizio.  
  
 La registrazione degli URL viene annullata se si arresta il servizio o si ricicla il dominio applicazione di Gestione report o del servizio Web. Se si modifica una prenotazione URL mentre il servizio è in esecuzione, il server di report riciclerà immediatamente il dominio applicazione per consentire l'annullamento della registrazione dell'URL precedente e l'utilizzo del nuovo URL.  
  
 Il concetto di prenotazione URL e il modo in cui questa è correlata agli indirizzi URL utilizzati per le applicazioni di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] possono essere illustrati tramite alcuni semplici esempi. Un aspetto essenziale da osservare è che la prenotazione URL ha una sintassi diversa dall'URL usato per accedere all'applicazione:  
  
|Prenotazione URL in HTTP.SYS|URL|Spiegazione|  
|---------------------------------|---------|-----------------|  
|http://+:80/reportserver|http://\<nomecomputer > / reportserver<br /><br /> http://\<IPAddress>/reportserver<br /><br /> http://localhost/reportserver|La prenotazione URL specifica un carattere jolly (+) sulla porta 80. In questo modo nella coda del server di report viene inserita qualsiasi richiesta in ingresso che specifica un host per la risoluzione nel computer server di report sulla porta 80. Si noti che con tale prenotazione URL è possibile utilizzare il numero desiderato di URL per accedere al server di report.<br /><br /> Si tratta della prenotazione URL predefinita per un server di report [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per la maggior parte dei sistemi operativi.|  
|http://123.45.67.0:80/reportserver|http://123.45.67.0/reportserver|Questa prenotazione URL specifica un indirizzo IP ed è molto più restrittiva della prenotazione URL con carattere jolly. Solo gli URL che includono l'indirizzo IP possono essere utilizzati per la connessione al server di report. Specifica questa prenotazione URL, una richiesta a un server di report all'indirizzo http://\<nomecomputer > / reportserver o http://localhost/reportserver avrebbe esito negativo.|  
  
##  <a name="DefaultURLs"></a> URL predefiniti  
 Se [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] viene installato utilizzando la configurazione predefinita, il programma di installazione prenoterà gli URL per il servizio Web ReportServer e per Gestione report. È possibile accettare questi valori predefiniti anche quando si definiscono prenotazioni URL nello strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Gli URL predefiniti includono il nome di un'istanza se si installa [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] o se [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] viene installato come istanza denominata.  
  
> [!IMPORTANT]  
>  Il carattere dell'istanza è un carattere di sottolineatura (`_`).  
  
 Le prenotazioni URL includono un numero di porta. I sistemi operativi seguenti consentono la condivisione di una porta da parte di più applicazioni Web:  
  
1.  [!INCLUDE[win8srv](../../includes/win8srv-md.md)]  
  
2.  [!INCLUDE[winserver2008r2](../../includes/winserver2008r2-md.md)]  
  
3.  [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)]  
  
4.  [!INCLUDE[win7](../../includes/win7-md.md)]  
  
5.  [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)]  
  
|Tipo di istanza|Applicazione|URL predefinito|Prenotazione di URL effettiva in HTTP.SYS|  
|-------------------|-----------------|-----------------|----------------------------------------|  
|Istanza predefinita|servizio Web ReportServer|http://\<nomeserver > / reportserver|http://\<nomeserver >: 80/reportserver|  
|Istanza predefinita|Gestione report|http://\<nomeserver > / reportserver|http://\<nomeserver >: 80/reportserver|  
|Istanza denominata|servizio Web ReportServer|http://\<servername>/reportserver_\<instancename>|http://\<nomeserver >: 80/reportserver_\<NomeIstanza >|  
|Istanza denominata|Gestione report|http://\<nomeserver > / Reports _\<NomeIstanza >|http://\<nomeserver >: 80/reports_\<NomeIstanza >|  
|SQL Server Express|servizio Web ReportServer|http://\<servername>/reportserver_SQLExpress|http://\<nomeserver >: 80/reportserver_SQLExpress|  
|SQL Server Express|Gestione report|http://\<servername>/reports_SQLExpress|http://\<servername>:80/reports_SQLExpress|  
  
##  <a name="URLPermissionsAccounts"></a> Autenticazione e identità del servizio per gli URL di Reporting Services  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] specificano l'account del servizio del server di report. L'account con cui viene eseguito il servizio viene utilizzato per tutti gli URL creati per le applicazioni di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in esecuzione nella stessa istanza. L'identità del servizio dell'istanza del server di report viene archiviata nel file RSReportServer.config.  
  
 L'account del servizio non prevede alcun valore predefinito. È tuttavia obbligatorio definire un account del servizio durante l'esecuzione del programma di installazione, specificandolo nella sezione `URLReservation` del file RSReportServer.config, anche se il server viene installato in modalità "solo file". I valori validi per l'account del servizio includono un account utente di dominio, `LocalSystem` o `NetworkService`.  
  
 L'accesso anonimo è disabilitato perché la sicurezza predefinita è `RSWindowsNegotiate`. Per l'accesso Intranet, gli URL del server di report utilizzano nomi di computer di rete. Se si desidera configurare [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] per le connessioni Internet, è necessario utilizzare impostazioni diverse. Per altre informazioni sull'autenticazione, vedere [Autenticazione con il server di report](../security/authentication-with-the-report-server.md) nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
##  <a name="URLlocalAdmin"></a> URL per l'amministrazione locale  
 È possibile utilizzare http://localhost/reportserver o http://localhost/reports se è stato specificato un carattere jolly sicuro o vulnerabile per la prenotazione URL.  
  
 L'URL http://localhost viene interpretato come http://127.0.0.1. Se la prenotazione URL è stata associata a un nome di computer o a un singolo indirizzo IP, non è possibile utilizzare localhost se non si crea una prenotazione aggiuntiva per 127.0.0.1 nel computer locale. Analogamente, se localhost o 127.0.0.1 è disabilitato nel computer, non è possibile utilizzare l'URL.  
  
 [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] e [!INCLUDE[nextref_longhorn](../../includes/nextref-longhorn-md.md)] includono nuove caratteristiche di sicurezza per ridurre al minimo il rischio di eseguire inavvertitamente programmi con privilegi elevati. Per attivare l'amministrazione locale su tali sistemi operativi, è necessario eseguire operazioni aggiuntive. Per altre informazioni, vedere [Configurare un server di report in modalità nativa per gli amministratori locali &#40;SSRS&#41;](../report-server/configure-a-native-mode-report-server-for-local-administration-ssrs.md).  
  
##  <a name="URLSharePoint"></a> URL per il Server di Report in modalità integrata SharePoint  
 Se un server di report autonomo è configurato per l'esecuzione nell'ambito di una distribuzione più ampia di un prodotto o una tecnologia SharePoint, la creazione degli URL e delle directory virtuali sarà interessata dalle considerazioni seguenti:  
  
-   Gli URL per i report e gli altri elementi vengono identificati tramite l'URL dell'applicazione Web di SharePoint. Per l'accesso tramite URL a report specifici, utilizzare sempre un URL completo che includa il percorso del sito, la raccolta documenti, il nome dell'elemento e un'estensione di file, ad esempio rdl per un report. Quando si fa riferimento a origini dei dati condivise e a modelli nei report o si specifica il server e le cartelle di destinazione per le operazioni di pubblicazione in un server di report, è necessario specificare URL completi.  
  
-   L'estensione del file viene utilizzata per distinguere tra tipi diversi di elementi del server di report. Le estensioni valide comprendono rdl per le definizioni del report, smdl per i modelli di report e rsds per le origini dei dati condivise create per un sito di SharePoint.  
  
-   Anche se per i prodotti e le tecnologie SharePoint sono state definite prenotazioni URL, è possibile ignorare la prenotazione in caso di pubblicazione nel server. Per le applicazioni Web di SharePoint, la prenotazione URL è un'operazione interna.  
  
-   Per distribuzioni a server singolo in cui un server di report integrato e l'istanza della tecnologia SharePoint sono installati nello stesso computer, è possibile utilizzare http://localhost/reportserver. Se http://localhost viene usato per accedere all'applicazione Web di SharePoint, è necessario utilizzare un sito Web non predefinito o un'assegnazione di porta univoco per accedere a un server di report. Se, inoltre, il server di report è integrato con una farm di SharePoint, l'accesso tramite localhost a un server di report non verrà risolto per i nodi presenti nella distribuzione installati in computer remoti.  
  
-   Non è possibile configurare l'endpoint e la prenotazione URL per Gestione report per un server di report in esecuzione in modalità integrata SharePoint. Se si esegue tale configurazione, Gestione report non funzionerà in seguito alla distribuzione di un server di report in modalità integrata SharePoint. Gestione report non è supportato in tale modalità.  
  
 Se una distribuzione con scalabilità orizzontale di un server di report è stata integrata per l'esecuzione nell'ambito di una distribuzione più ampia di un prodotto o una tecnologia SharePoint, bilanciare il carico dei nodi del server di report e definire un URL di un singolo server virtuale per la distribuzione con scalabilità orizzontale. Le impostazioni di integrazione Server report consentono solo di specificare un URL di un singolo server di report. Nel caso di una distribuzione con scalabilità orizzontale, l'URL deve essere il punto di accesso per i nodi server nella distribuzione con scalabilità orizzontale.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare un URL &#40;Gestione configurazione SSRS&#41;](configure-a-url-ssrs-configuration-manager.md)   
 [Sintassi delle prenotazioni URL &#40;Gestione configurazione SSRS&#41;](url-reservation-syntax-ssrs-configuration-manager.md)  
  
  
