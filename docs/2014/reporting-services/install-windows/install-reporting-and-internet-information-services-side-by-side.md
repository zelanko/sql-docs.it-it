---
title: Installare Reporting Services e Internet Information Services side-by-Side (modalità nativa SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- deploying [Reporting Services], IIS
ms.assetid: 9b651fa5-f582-4f18-a77d-0dde95d9d211
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 514774acc7255f2f499bfe7fdd6e731944ab67fe
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "67285051"
---
# <a name="install-reporting-services-and-internet-information-services-side-by-side-ssrs-native-mode"></a>Installare side-by-side Reporting Services e Internet Information Services (modalità nativa SSRS)
  È possibile installare ed eseguire [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] (SSRS) e Internet Information Services (IIS) nello stesso computer. La versione di IIS utilizzata determina i problemi di interoperabilità che è necessario risolvere.  
  
||  
|-|  
|[!INCLUDE[applies](../../includes/applies-md.md)][!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Modalità nativa|  
  
|Versione di IIS|Problemi|Descrizione|  
|-----------------|------------|-----------------|  
|IIS 6.0, 7.0, 8.0, 8.5|Richieste destinate a un'applicazione vengono accettate da un'applicazione diversa.<br /><br /> HTTP.SYS applica regole di precedenza per le prenotazioni URL. Le richieste inviate ad applicazioni con lo stesso nome di directory virtuale e che eseguono congiuntamente il monitoraggio della porta 80 potrebbero non raggiungere la destinazione desiderata se la prenotazione URL è debole rispetto alla prenotazione URL di un'altra applicazione.|In determinate condizioni, un endpoint registrato che prevale su un altro endpoint URL nello schema di prenotazione degli URL potrebbe ricevere richieste HTTP destinate all'altra applicazione.<br /><br /> L'utilizzo di nomi univoci per le directory virtuali per il servizio Web ReportServer e Gestione report consente di evitare questo conflitto.<br /><br /> Informazioni dettagliate su questo scenario vengono fornite nel presente argomento.|  
  
## <a name="precedence-rules-for-url-reservations"></a>Regole di precedenza per le prenotazioni URL  
 Prima di poter passare alla risoluzione dei problemi di interoperabilità tra IIS e [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], è necessario comprendere le regole di precedenza relative alle prenotazioni di URL. Le regole di precedenza possono essere generalizzate nell'affermazione in base alla quale una prenotazione URL che ha valori definiti in modo più esplicito ha la precedenza nella ricezione di richieste che corrispondono all'URL.  
  
-   Una prenotazione URL che specifica una directory virtuale è più esplicita di una prenotazione che la omette.  
  
-   Una prenotazione URL che specifica un solo indirizzo (come indirizzo IP, nome di dominio completo, nome di un computer di rete o nome host) è più esplicita rispetto a un carattere jolly.  
  
-   Una prenotazione URL che specifica un carattere jolly complesso è più esplicita rispetto a una prenotazione che utilizza un carattere jolly vulnerabile.  
  
 Negli esempi seguenti è mostrato un intervallo di prenotazioni URL, ordinate dalle più esplicite a quelle meno esplicite:  
  
|Esempio|Richiesta|  
|-------------|-------------|  
|http:\//123.234.345.456:80/Reports|Riceve tutte le richieste inviate a http:\//123.234.345.456/reports o http://\<nomecomputer>/Reports se un servizio dei nomi di dominio è in grado di risolvere l'indirizzo IP in tale nome host.|  
|http://+:80/reports|Riceve tutte le richieste inviate a qualsiasi indirizzo IP o nome host valido per tale computer finché l'URL contiene il nome della directory virtuale "reports".|  
|http:\//123.234.345.456:80|Riceve una richiesta che specifica http:\//123.234.345.456 o http://\<nomecomputer> se un servizio del nome di dominio è in grado di risolvere l'indirizzo IP in tale nome host.|  
|http://+:80|Riceve le richieste che non sono già state ricevute da altre applicazioni, per qualsiasi endpoint dell'applicazione di cui è stato eseguito il mapping all'opzione **Tutti assegnati**.|  
|http://*:80|Riceve le richieste che non sono già state ricevute da altre applicazioni, per gli endpoint dell'applicazione di cui è stato eseguito il mapping all'opzione **Non assegnati**.|  
  
 Un'indicazione di un conflitto di porte è la visualizzazione del messaggio di errore seguente: "System.IO.FileLoadException: Il processo non può accedere al file perché è in uso da un altro processo. (Eccezione da HRESULT: 0x80070020)".  
  
## <a name="url-reservations-for-iis-60-70-80-85-with-sssql14-reporting-services"></a>Prenotazioni URL per IIS 6.0, 7.0, 8.0, 8.5 con [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] Reporting Services  
 Stabilite le regole di precedenza descritte nella sezione precedente, è possibile iniziare a comprendere in che modo le prenotazioni URL definite per Reporting Services e IIS agevolino l'interoperabilità. Reporting Services riceve le richieste che specificano in modo esplicito i nomi delle directory virtuali per le proprie applicazioni, mentre IIS riceve tutte le richieste rimanenti che possono pertanto essere dirette ad applicazioni eseguite all'interno del modello di processo di IIS.  
  
|Applicazione|Prenotazione URL|Descrizione|Ricezione richiesta|  
|-----------------|---------------------|-----------------|---------------------|  
|Server di report|http://+:80/ReportServer|Carattere jolly complesso sulla porta 80, con directory virtuale del server di report.|Riceve sulla porta 80 tutte le richieste che specificano la directory virtuale del server di report. Il servizio Web ReportServer riceve tutte le richieste all'indirizzo http://\<nomecomputer>/reportserver.|  
|Gestione report|http://+:80/Reports|Carattere jolly complesso sulla porta 80, con directory virtuale Reports.|Riceve sulla porta 80 tutte le richieste che specificano la directory virtuale reports. Gestione report riceve tutte le richieste a\<http://nomecomputer>/Reports.|  
|IIS|http://*:80/|Carattere jolly vulnerabile sulla porta 80.|Riceve sulla porta 80 tutte le richieste rimanenti che non vengono ricevute da un'altra applicazione.|  
  
## <a name="side-by-side-deployments-of-sscurrent-and-sql-server-2005-reporting-services-on-iis-60-70-80-85"></a>Distribuzioni side-by-side di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e SQL Server 2005 Reporting Services in IIS 6.0, 7.0, 8.0, 8.5  
 I problemi di interoperabilità tra IIS e Reporting Services si verificano quando i nomi delle directory virtuali dei siti Web di IIS sono identici a quelli utilizzati da Reporting Services. Si supponga ad esempio di disporre della configurazione seguente:  
  
-   Un sito Web in IIS assegnato alla porta 80 e una directory virtuale denominata "Reports".  
  
-   Un' [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] istanza del server di report installata nella configurazione predefinita, in cui anche la prenotazione URL specifica la porta 80 e l'applicazione Gestione report USA anche "Reports" come nome della directory virtuale.  
  
 Data questa configurazione, una richiesta inviata a http://\<computername>:80/reports verrà ricevuta da Gestione report. L'applicazione cui si accede con la directory virtuale Reports in IIS non riceverà più richieste dopo l'installazione dell'istanza del server di report di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
 Se si eseguono distribuzioni side-by-side di versioni meno recenti e più recenti di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], è possibile che si verifichi il problema di routing descritto in precedenza, poiché tutte le versioni di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] utilizzano "ReportServer" e "Reports" come nomi delle directory virtuali per le applicazioni di server di report e Gestione report, aumentando la probabilità della presenza di directory virtuali "reports" e "reportserver" in IIS.  
  
 Per garantire che tutte le applicazioni ricevano richieste, adottare le linee guida seguenti:  
  
-   Per le installazioni di Reporting Services, utilizzare nomi delle directory virtuali che non siano già utilizzati da un sito Web di IIS sulla stessa porta di Reporting Services. Se si verifica un conflitto, installare Reporting Services in modalità "solo file", utilizzando l'opzione Installa senza configurare l'opzione server dell'Installazione guidata, in modo che sia possibile configurare le directory virtuali al termine dell'installazione. Un'indicazione della configurazione come conflitto è la visualizzazione del messaggio di errore seguente: System.IO.FileLoadException: Il processo non può accedere al file perché è in uso da un altro processo. (Eccezione da HRESULT: 0x80070020).  
  
-   Per installazioni da configurare manualmente, adottare le convenzioni di denominazione predefinite negli URL configurati. Se si installa [!INCLUDE[ssRSCurrent](../../includes/ssrscurrent-md.md)] come istanza denominata, includere il nome dell'istanza al momento della creazione di una directory virtuale.  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare gli URL del server di report &#40;Gestione configurazione SSRS&#41;](configure-report-server-urls-ssrs-configuration-manager.md)   
 [Configurare un URL &#40;Configuration Manager SSRS&#41;](configure-a-url-ssrs-configuration-manager.md)   
 [Installare Reporting Services server di report in modalità nativa](install-reporting-services-native-mode-report-server.md)  
  
  
