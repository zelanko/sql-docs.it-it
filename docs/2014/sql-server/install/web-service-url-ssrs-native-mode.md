---
title: URL servizio Web (modalità nativa SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- SQL12.rsconfigtool.reportservervirtualdirectory.F1
helpviewer_keywords:
- Reporting Services, Web service
ms.assetid: 9d210b5d-2a08-4e56-a4f5-c16715b00d79
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 01e5393ae638ddcecd04211a0a7e01e8116346a9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "71952357"
---
# <a name="web-service-url-ssrs-native-mode"></a>URL servizio Web (modalità nativa SSRS)
  Utilizzare la pagina URL servizio Web per configurare o modificare l'URL utilizzato per accedere al server di report. In base all'URL specificato, verrà creata una *prenotazione URL* . La prenotazione URL definisce la sintassi e le regole per tutti gli URL che sarà possibile utilizzare in seguito per accedere al servizio Web ReportServer e specifica il prefisso, l'host, la porta e la directory virtuale per il servizio Web ReportServer. A seconda di come si specifica l'host, per una singola prenotazione sono possibili più URL. Il valore predefinito per l'host specifica un carattere jolly complesso. Un carattere jolly complesso consente di specificare in un URL qualsiasi nome host che possa essere risolto nel computer che ospita il server di report. Per ulteriori informazioni sulla configurazione e le prenotazioni URL, vedere [configurare un url &#40;ssrs Configuration Manager&#41;](../../reporting-services/install-windows/configure-a-url-ssrs-configuration-manager.md) e [configurare gli URL del Server di Report &#40;SSRS Configuration Manager&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md).  
  
 [!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modalità nativa.  
  
 Per aprire questa pagina, avviare Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e fare clic su **URL servizio Web** nel riquadro di navigazione. Per altre informazioni, vedere [Gestione configurazione Reporting Services &#40;modalità nativa&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-native-mode.md).  
  
 In questa pagina sono disponibili i valori comunemente utilizzati negli URL del server di report. Se si desidera creare URL aggiuntivi, utilizzare intestazioni host o specificare l'indirizzo IP in un formato specifico, fare clic su **Avanzate**.  
  
 Dopo che si fa clic su **Applica**, in questa pagina verrà visualizzato un collegamento al servizio Web. Se si fa clic sul collegamento prima che venga creato il database del server di report, è probabile che venga visualizzato il messaggio di errore "Impossibile trovare la pagina". Una volta configurato il database, questo errore non verrà più visualizzato. Per altre informazioni, vedere [Creare un database del server di report in modalità nativa &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/ssrs-report-server-create-a-native-mode-report-server-database.md).  
  
 Se [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è stato reinstallato e vengono restituiti errori quando si tenta di utilizzare la porta 80 e il valore predefinito Tutti assegnati per l'indirizzo IP, è in genere possibile risolvere l'errore ricreando l'URL dopo il riavvio del servizio.  
  
## <a name="options"></a>Opzioni  
 **Directory virtuale**  
 Viene specificato il nome della directory virtuale per il servizio Web ReportServer. È possibile specificare un solo nome di directory virtuale per ogni istanza del servizio Web ReportServer presente nello stesso computer.  
  
 **Indirizzo IP**  
 Identifica il computer server di report in una rete TCP/IP. I valori validi includono:  
  
-   **Tutti assegnati** : specifica che qualunque indirizzo IP assegnato al computer può essere usato in un URL che punta a un'applicazione del server di report. Questo valore include anche i nomi host descrittivi, ad esempio i nomi computer, che possono essere risolti da un DNS in un indirizzo IP assegnato al computer. Si tratta del valore predefinito per un URL di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
-   **Non assegnati** : specifica che il server di report accetterà qualsiasi richiesta per cui non esiste una corrispondenza esatta per l'indirizzo IP o il nome host. Non utilizzare questo valore se è già in uso in un'altra applicazione Web. In caso contrario, verrà interrotta l'esecuzione del servizio per l'altra applicazione.  
  
-   **127.0.0.1** : utilizzato per accedere a localhost. Tale indirizzo supporta l'amministrazione locale nel computer server di report. Se si seleziona solo questo valore, potranno accedere all'applicazione solo gli utenti connessi localmente al computer server di report.  
  
-   *Nnn.nnn.nnn.nnn* : indirizzo IPv4 di una scheda di rete nel computer. Se la rete utilizza l'indirizzamento IPv6, l'indirizzo IP sarà un valore a 128 bit di campi da 8 4 byte simile al formato seguente: \<intestazione>:*nnnn: nnnn: nnnn: nnnn*  
  
     Se si dispone di più schede, verrà visualizzato un indirizzo IP per ognuna. Se si seleziona solo questo valore, l'accesso all'applicazione sarà limitato all'indirizzo IP specificato e a qualsiasi nome host di cui il DNS esegue il mapping all'indirizzo. Non è possibile utilizzare localhost per accedere a un server di report, né utilizzare gli indirizzi IP di altre schede di rete installate nel computer server di report.  
  
 **Porta TCP**  
 Consente di specificare la porta monitorata dal server di report per le richieste HTTP per gli URL che includono il nome della directory virtuale del server di report.  
  
 **Certificato SSL**  
 Consente di associare un certificato all'indirizzo IP specificato. Il certificato deve essere installato e configurato nel computer. Reporting Services non fornisce caratteristiche per la gestione di certificati. Il certificato deve essere rilasciato a un nome host o a un nome computer risolto nell'indirizzo IP. Per utilizzare, ad esempio, un certificato rilasciato a http://salesreports, l'indirizzo IP specificato deve essere risolto in un server denominato "SalesReports".  
  
 Se si utilizza un certificato, è necessario modificare l'impostazione di configurazione `UrlRoot` nel file RSReportServer.config in modo che specifichi il nome completo del computer per cui viene registrato il certificato. Per altre informazioni, vedere [Configurare connessioni SSL in un server di report in modalità nativa](../../reporting-services/security/configure-ssl-connections-on-a-native-mode-report-server.md) nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **Porta SSL**  
 Consente di specificare la porta per le connessioni SSL.  
  
 **URL**  
 Consente di visualizzare gli URL definiti per l'istanza corrente del server di report.  
  
 **Avanzate**  
 Fare clic su questa opzione per creare URL aggiuntivi per l'istanza dell'applicazione corrente.  
  
> [!NOTE]
>  Se si dispone di associazioni SSL esistenti e di prenotazioni di URL e si desidera modificare l'associazione SSL, ad esempio per utilizzare un'intestazione host o un certificato diverso, è consigliabile completare in ordine i passaggi seguenti:  
> 
>  1.  Innanzitutto rimuovere tutte le prenotazioni di URL.  
> 2.  Successivamente rimuovere tutte le associazioni SSL.  
> 3.  Infine ricreare gli URL e le associazioni SSL.  
> 
>  I passaggi precedenti possono essere completati utilizzando Gestione configurazione [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
> 
>  Microsoft Windows supporta un'associazione per ogni combinazione di indirizzo IP e porta. Se un server di report viene configurato in modo che venga utilizzato un valore di intestazione host specifico e il certificato relativo alla combinazione tra porta e indirizzo IP viene emesso con un valore di intestazione host diverso, nel browser verrà visualizzato un avviso in cui viene indicato che il certificato non corrisponde all'URL in uso.  
> 
>  Per risolvere questo problema, eliminare tutte le associazioni, quindi crearne di nuove con impostazioni univoche o configurare le registrazioni di URL di Reporting Services con caratteri jolly.  
  
## <a name="see-also"></a>Vedere anche  
 [Reporting Services Configuration Manager argomenti della Guida F1 &#40;modalità nativa di SSRS&#41;](../../../2014/sql-server/install/reporting-services-configuration-manager-f1-help-topics-ssrs-native-mode.md)   
 [Configurare gli URL del server di report &#40;Gestione configurazione SSRS&#41;](../../reporting-services/install-windows/configure-report-server-urls-ssrs-configuration-manager.md)  
  
  
