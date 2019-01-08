---
title: Configurare un URL (Gestione configurazione SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- URL access [Reporting Services], syntax
ms.assetid: 851e163a-ad2a-491e-bc1e-4df92327092f
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 7ab343a4c6f70d97aa5e770b8ca21dd4d835f05c
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53375933"
---
# <a name="configure-a-url--ssrs-configuration-manager"></a>Configurare un URL (Gestione configurazione SSRS)
  Per poter utilizzare Gestione report o il servizio Web ReportServer, è necessario configurare almeno un URL per ogni applicazione. La configurazione degli URL è obbligatoria se [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è stato installato in modalità "solo file", ovvero se è stata selezionata l'opzione **Installa senza configurare il server** nella pagina Opzioni di installazione Server report dell'Installazione guidata. Se [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è stato installato con la configurazione predefinita, gli URL sono già configurati per ogni applicazione. Se si dispone di un server di report configurato per utilizzare la modalità integrata SharePoint e si esegue l'aggiornamento dell'URL del servizio Web ReportServer mediante lo strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , è necessario aggiornare anche l'URL in Amministrazione centrale SharePoint.  
  
 Per configurare gli URL, utilizzare lo strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , che consente di definire tutte le parti dell'URL. A differenza delle versioni precedenti, i siti Web di Internet Information Services (IIS) non forniscono più accesso alle applicazioni di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versioni successive.  
  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] fornisce valori predefiniti adatti per la maggior parte degli scenari di distribuzione, incluse le distribuzioni affiancate con altri servizi e applicazioni Web. Gli URL predefiniti includono i nomi di istanza, per ridurre il rischio di conflitti tra URL se si eseguono più istanze del server di report nello stesso computer.  
  
 In questo argomento sono incluse istruzioni per le attività seguenti:  
  
-   Creare un URL per il servizio Web ReportServer.  
  
-   Creare un URL per Gestione report.  
  
-   Impostare proprietà avanzate per gli URL per definire altri URL.  
  
 Per altre informazioni su come gli URL vengono archiviati e gestiti o problemi di interoperabilità, vedere [sulle prenotazioni e registrazione URL &#40;Gestione configurazione SSRS&#41; ](about-url-reservations-and-registration-ssrs-configuration-manager.md) e [installa Reporting Servizi e Internet Information Services Side-by-Side &#40;modalità nativa SSRS&#41;](install-reporting-and-internet-information-services-side-by-side.md)nelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione Online. Per esaminare alcuni esempi di URL utilizzati di frequente in un'installazione di Reporting Services, vedere [Esempi di URL](#URLExamples) in questo argomento.  
  
## <a name="prerequisites"></a>Prerequisiti  
 Prima di creare o modificare un URL, tenere presenti gli aspetti seguenti:  
  
-   È necessario essere un membro del gruppo Administrators locale nel computer server di report.  
  
-   Se IIS 6.0 o 7.0 è installato nello stesso computer, controllare i nomi delle directory virtuali in tutti i siti Web che utilizzano la porta 80. Se una o più directory virtuali utilizzano i nomi delle directory virtuali predefiniti di Reporting Services, ovvero "Report" e "ReportServer", scegliere nomi delle directory virtuali diversi per gli URL di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] da configurare.  
  
-   Per configurare gli URL, è necessario utilizzare lo strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Non utilizzare un'utilità di sistema. Non modificare mai prenotazioni URL direttamente nella sezione `URLReservations` del file RSReportServer.config. L'utilizzo dello strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è necessario per aggiornare la prenotazione URL sottostante archiviata internamente e per sincronizzare le impostazioni URL archiviate nel file RSReportServer.config.  
  
-   Scegliere un'ora con un'attività di report ridotta. Ogni volta che la prenotazione URL cambia, è possibile che venga eseguito il riciclo dei domini applicazione per il servizio Web ReportServer e per Gestione report.  
  
-   Per una panoramica della creazione di URL e l'utilizzo in [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], vedere [Configurare gli URL del server di report &#40;Gestione configurazione SSRS&#41;](configure-report-server-urls-ssrs-configuration-manager.md).  
  
### <a name="to-configure-a-url-for-the-report-server-web-service"></a>Per configurare un URL per il servizio Web ReportServer  
  
1.  Avviare lo strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e connettersi a un'istanza del server di report locale.  
  
2.  Fare clic su **URL servizio Web**.  
  
3.  Specificare la directory virtuale. Il nome della directory virtuale identifica l'applicazione che riceve la richiesta. Poiché un indirizzo e una porta IP possono essere condivisi da più applicazioni, il nome della directory virtuale specifica l'applicazione che riceve la richiesta.  
  
     Tale valore deve essere univoco per garantire che la richiesta raggiunga la destinazione prevista. Questo valore è obbligatorio. e supporta la distinzione tra maiuscole e minuscole. Tra un nome di directory virtuale e un'istanza di un'applicazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] esiste una corrispondenza uno-a-uno. Se si creano più URL per la stessa istanza dell'applicazione, è necessario utilizzare lo stesso nome di directory virtuale in tutti gli URL definiti per l'istanza dell'applicazione.  
  
     Per il servizio Web ReportServer il nome di directory virtuale predefinito è **ReportServer**.  
  
4.  Specificare l'indirizzo IP che identifica in modo univoco il computer server di report in rete. Se si desidera specificare un'intestazione host o definire URL aggiuntivi per la stessa istanza dell'applicazione, è necessario fare clic su **Avanzate**. Per indicazioni su come impostare le proprietà avanzate nell'URL, vedere le istruzioni fornite più avanti in questo argomento. Altrimenti, utilizzare la pagina **URL servizio Web** per impostare uno dei valori seguenti:  
  
    -   **Tutti assegnati** : specifica che qualunque indirizzo IP assegnato al computer può essere usato in un URL che punta a un'applicazione del server di report. Questo valore include anche i nomi host descrittivi, ad esempio i nomi computer, che possono essere risolti da un DNS in un indirizzo IP assegnato al computer. Si tratta del valore predefinito per un URL di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
    -   **Tutti non assegnati** : specifica che il server di report riceverà tutte le richieste che non sono state gestite da un'altra applicazione. È consigliabile evitare di specificare questa opzione. In caso contrario, è possibile che un'altra applicazione che dispone di una prenotazione URL più specifica intercetti le richieste destinate al server di report.  
  
    -   **127.0.0.1** : indirizzo IPv4 utilizzato per accedere a localhost. Tale indirizzo supporta l'amministrazione locale nel computer server di report. Se si seleziona solo questo valore, potranno accedere all'applicazione solo gli utenti connessi localmente al computer server di report.  
  
    -   **::1** : indirizzo di loopback in formato IPv6.  
  
    -   Nell'elenco vengono visualizzati anche indirizzi IP specifici. Gli indirizzi IP possono essere in formato IPv4 o IPv6. *Nnn.nnn.nnn.nnn* : indirizzo IPv4 a 32 bit di una scheda di rete nel computer. Gli indirizzi IPv6 sono a 128 bit, con otto campi a 4 byte separati dai due punti: \<prefisso>:*nnnn:nnnn:nnnn:nnnn:nnnn:nnnn*  
  
         Se sono presenti più schede o la rete supporta indirizzi IPv4 e IPv6, verranno visualizzati più indirizzi IP. Se si seleziona solo un indirizzo IP, l'accesso all'applicazione sarà limitato all'indirizzo IP specificato e a qualsiasi nome host di cui il DNS esegue il mapping all'indirizzo. Non è possibile utilizzare localhost per accedere a un server di report, né utilizzare gli indirizzi IP di altre schede di rete installate nel computer server di report. Si seleziona in genere questo valore per configurare più prenotazioni di URL che specificano anche indirizzi IP o nomi host espliciti, ad esempio uno per una scheda di rete utilizzata per le connessioni Intranet e un altro per le connessioni Extranet.  
  
5.  Specificare la porta. La porta 80 è la porta predefinita per [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] in [!INCLUDE[wiprlhlong](../../includes/wiprlhlong-md.md)] e Windows Server 2008, in quanto può essere condivisa con altre applicazioni. Se si desidera utilizzare un numero di porta personalizzato, sarà necessario specificarlo sempre nell'URL utilizzato per accedere al server di report. Per trovare una porta disponibile, è possibile utilizzare i metodi seguenti:  
  
    -   Al prompt dei comandi digitare il comando seguente per ottenere l'elenco delle porte TCP in uso:  
  
         `netstat -a -n -p tcp`  
  
    -   Per informazioni sulle assegnazioni di porta TCP e le differenze tra porte note (da 0 a 1023), porte registrate (da 1024 a 49151) e porte dinamiche o private (da 49152 a 65535), vedere l'articolo [Informazioni sull'assegnazione di porte TCP/IP](https://support.microsoft.com/kb/174904)nel sito Web del supporto tecnico Microsoft.  
  
    -   Se si utilizza Windows Firewall, è necessario aprire la porta. Per istruzioni, vedere [Configure a Firewall for Report Server Access](../report-server/configure-a-firewall-for-report-server-access.md).  
  
6.  Se necessario, verificare che in IIS (se installato) non sia presente una directory virtuale con lo stesso nome che si intende utilizzare.  
  
7.  Se è stato installato un certificato SSL, è possibile selezionarlo a questo punto per eseguire il binding dell'URL al certificato SSL installato nel computer.  
  
8.  Se si seleziona un certificato SSL, è eventualmente possibile specificare una porta personalizzata. L'impostazione predefinita è 443, ma è possibile utilizzare qualsiasi porta disponibile.  
  
9. Fare clic su **Applica** per creare l'URL.  
  
10. Eseguire il test dell'URL facendo clic sul collegamento nella sezione **URL** della pagina. Per poter eseguire il test dell'URL, è necessario creare e configurare il database del server di report. Per istruzioni, vedere [Creare un database del server di report in modalità nativa &#40;Gestione configurazione SSRS&#41;](ssrs-report-server-create-a-native-mode-report-server-database.md).  
  
11. Inoltre, se il server di report è configurato per utilizzare la modalità integrata SharePoint, configurare l'URL del servizio Web ReportServer in Amministrazione centrale SharePoint. Per altre informazioni su come aggiornare l'URL del servizio Web ReportServer in Amministrazione centrale SharePoint, vedere [configurazione e amministrazione di un Server di Report &#40;Reporting Services SharePoint Mode&#41; ](../configure-administer-report-server-reporting-services-sharepoint-mode.md) e [Reporting Services Report Server &#40;in modalità SharePoint&#41;](../reporting-services-report-server-sharepoint-mode.md).  
  
### <a name="to-create-a-url-reservation-for-report-manager"></a>Per creare una prenotazione URL per Gestione report  
  
1.  Avviare lo strumento di configurazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e connettersi all'istanza del server di report.  
  
2.  Fare clic su **URL Gestione report**.  
  
3.  Specificare la directory virtuale. Gestione report è in attesa sulla stessa porta e sullo stesso indirizzo IP del servizio Web ReportServer. Se Gestione report è stato configurato per puntare a un servizio Web ReportServer diverso, è necessario modificare le impostazioni URL di Gestione report nel file RSReportServer.config. Per istruzioni, vedere [configurare Gestione Report &#40;in modalità nativa&#41; ](../report-server/configure-web-portal.md) nelle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] documentazione Online.  
  
4.  Se è stato installato un certificato SSL, è possibile selezionarlo affinché tutte le richieste a Gestione report vengano indirizzate tramite HTTPS.  
  
     Se si seleziona un certificato SSL, è eventualmente possibile specificare una porta personalizzata. L'impostazione predefinita è 443, ma è possibile utilizzare qualsiasi porta disponibile.  
  
5.  Fare clic su **Applica** per creare l'URL.  
  
6.  Eseguire il test dell'URL facendo clic sul collegamento nella sezione **URL** della pagina.  
  
## <a name="setting-advanced-properties-to-specify-additional-urls"></a>Impostazione di proprietà avanzate per specificare altri URL  
 È possibile riservare più URL per il servizio Web ReportServer o Gestione report specificando porte o nomi host diversi, ovvero un indirizzo IP o un nome di intestazione host che può essere risolto da un DNS in un indirizzo IP assegnato al computer. Creando più URL, è possibile configurare percorsi di accesso diversi per la stessa istanza del server di report. Per attivare l'accesso Intranet ed Extranet a un server di report, ad esempio, è possibile utilizzare l'URL predefinito per l'accesso tramite Intranet e un altro nome host completo per l'accesso Extranet:  
  
-   http://myserver01/reportserver  
  
-   http://www.adventure-works.com/reportserver  
  
 Non è possibile impostare più nomi delle directory virtuali per la stessa istanza dell'applicazione. Di ogni istanza dell'applicazione di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] viene eseguito il mapping a un singolo nome di directory virtuale. Se si dispone di più istanze di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nello stesso computer, il nome della directory virtuale per un'applicazione deve includere il nome di istanza per garantire che ogni richiesta raggiunga la destinazione prevista.  
  
#### <a name="to-set-advanced-properties-on-a-url"></a>Per impostare proprietà avanzate in un URL  
  
1.  Nella pagina **URL servizio Web** o **URL Gestione report** fare clic su **Avanzate**.  
  
2.  Scegliere **Aggiungi**.  
  
3.  Fare clic su Indirizzo IP o Nome intestazione host. Nel caso di un'intestazione host, assicurarsi di specificare un nome che il servizio DNS sia in grado di risolvere. Se si specifica un nome di dominio pubblico, specificare l'intero URL, incluso http://www.  
  
4.  Specificare la porta. Se si specifica una porta personalizzata, l'URL dell'applicazione deve sempre includere il numero di porta.  
  
5.  Fare clic su **OK**.  
  
6.  Eseguire il test dell'URL aprendo una finestra del browser e immettendo l'URL.  
  
## <a name="urls-for-multiple-report-server-instances-on-the-same-computer"></a>URL per più istanze del server di report nello stesso computer  
 Se si riservano URL per più istanze di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], è necessario seguire le convenzioni di denominazione per evitare conflitti di denominazione. Per altre informazioni, vedere [Prenotazioni URL per le distribuzioni di più istanze del server di report &#40;Gestione configurazione SSRS&#41;](url-reservations-for-multi-instance-report-server-deployments.md).  
  
##  <a name="URLExamples"></a> Esempi di configurazioni di URL  
 Nell'elenco seguente sono inclusi alcuni esempi di URL di server di report:  
  
-   http://localhost/reportserver  
  
-   http://localhost/reportserver_SQLEXPRESS  
  
-   http://sales01/reportserver  
  
-   http://sales01:8080/reportserver  
  
-   https://sales.adventure-works.com/reportserver  
  
-   https://www.adventure-works.com:8080/reportserver01  
  
 Gli URL che utilizzano l'accesso a Gestione report condividono un formato simile e vengono in genere creati nello stesso sito Web che ospita il server di report. L'unica differenza è costituita dal nome di directory virtuale. In questo caso viene usato il nome **reports** , ma è possibile configurare qualsiasi nome:  
  
-   http://localhost/reports  
  
-   http://localhost/reports_SQLEXPRESS  
  
-   http://sales01/reports  
  
-   http://sales01:8080/reports  
  
-   https://sales.adventure-works.com/reports  
  
-   https://www.adventure-works.com:8080/reports  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../sql-server/install/reporting-services-configuration-manager-native-mode.md)   
 [Configurare gli URL del server di report &#40;Gestione configurazione SSRS&#41;](configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
