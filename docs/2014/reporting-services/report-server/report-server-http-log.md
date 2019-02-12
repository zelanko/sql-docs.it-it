---
title: Log HTTP del server di report | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- HTTP [Reporting Services]
ms.assetid: 6cc433b7-165c-4b16-9034-79256dd6735f
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 9eb3cd35267075b6228df993f31dbec021b681bf
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/11/2019
ms.locfileid: "56031372"
---
# <a name="report-server-http-log"></a>Log HTTP del server di report
  Nei file di log HTTP del server di report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] viene mantenuto un record per ogni richiesta HTTP e relativa risposta gestite dal server di report. Poiché gli errori di overflow e di timeout relativi alle richiesta ed errori non raggiungono il server di report, non vengono registrati nel file di log.  
  
 Per impostazione predefinita, la registrazione HTTP non è abilitata. Per abilitare la registrazione HTTP, modificare il **Reportingservicesservice** file di configurazione per usare questa funzionalità nell'installazione.  
  
## <a name="viewing-log-information"></a>Visualizzazione delle informazioni sul log di esecuzione  
 Il log è un file di testo ASCII, che può essere visualizzato mediante qualsiasi editor di testo. Il file di log HTTP del server di report è equivalente al file di log esteso W3C presente in IIS e utilizza campi simili ed è pertanto possibile utilizzare visualizzatori del file di log di IIS esistenti per leggerlo. Nella tabella seguente vengono fornite informazioni aggiuntive sul file di log HTTP:  
  
|||  
|-|-|  
|**Nome file**|Per impostazione predefinita, il nome del file di log è<br /><br /> `ReportServerService_HTTP_<timestamp>.log.`<br /><br /> È possibile personalizzare il prefisso del nome del file modificando l'attributo HttpTraceFileName nel file ReportingServicesService.exe.config. Il timestamp si basa su l'ora UTC (Coordinated Universal Time).|  
|**Percorso del file**|I file vengono scritti nel percorso seguente:<br /><br /> `\Microsoft SQL Server\<SQL Server Instance>\Reporting Services\LogFiles`|  
|**Formato del file**|Il file è in formato en-US ed è un file di testo ASCII.|  
|**Creazione di file e la conservazione**|Per creare un log HTTP, è necessario innanzitutto riabilitarlo nel file di configurazione e riavviare il servizio. Il file viene quindi creato quando il server di report gestisce una richiesta HTTP. Se le impostazioni sono state configurate ma il file di log non viene visualizzato, aprire un report o avviare un'applicazione del server di report (ad esempio Gestione report) per generare una richiesta HTTP per creare il file.<br /><br /> Una nuova istanza del file di log verrà creata dopo ogni riavvio del servizio e ogni successiva richiesta HTTP al server di report.<br /><br /> Per impostazione predefinita, i log di traccia possono occupare uno spazio massimo di 32 MB e vengono eliminati dopo 14 giorni.|  
  
## <a name="configuration-settings-for-report-server-http-log"></a>Impostazioni di configurazione per il log HTTP del server di report  
 Per configurare il log HTTP del Server di Report, utilizzare Blocco note per modificare la **Reportingservicesservice** file. Il percorso del file di configurazione è \Programmi\Microsoft SQL Server\MSSQL.n\Reporting Services\ReportServer\Bin.  
  
 Per abilitare il server HTTP, aggiungere `http:4` alla sezione RStrace del file ReportingServicesService.exe.config. Tutte le altre voci del file di log HTTP sono facoltative. Nell'esempio seguente sono incluse tutte le impostazioni in modo che sia possibile incollare la sezione intera sulla sezione Rstrace e successivamente eliminare le impostazioni non necessarie.  
  
```  
   <RStrace>  
         <add name="FileName" value="ReportServerService_" />  
         <add name="FileSizeLimitMb" value="32" />  
         <add name="KeepFilesForDays" value="14" />  
         <add name="Prefix" value="tid, time" />  
         <add name="TraceListeners" value="debugwindow, file" />  
         <add name="TraceFileMode" value="unique" />  
         <add name="HttpTraceFileName" value="ReportServerService_HTTP_" />  
         <add name="HttpTraceSwitches" value="date,time, clientip,username,serverip,serverport,host,method,uristem,uriquery,protocolstatus,bytesreceived,timetaken,protocolversion,useragent,cookiereceived,cookiesent,referrer" />  
         <add name="Components" value="all:3,http:4" />  
   </RStrace>  
```  
  
## <a name="log-file-fields"></a>Campi del file di log  
 Nella tabella seguente vengono descritti i campi procedure disponibili nel log. L'elenco di campi è configurabile ed è possibile specificare i campi da includere tramite l'impostazione di configurazione `HTTPTraceSwitches`. Il **predefinite** consente di specificare se il campo verrà incluso nel file di registro automaticamente se non si specifica di colonna `HTTPTraceSwitches`.  
  
|Campo|Descrizione|Impostazione predefinita|  
|-----------|-----------------|-------------|  
|HttpTraceFileName|Questo valore è facoltativo. Il valore predefinito è ReportServerServiceHTTP_. È possibile specificare un valore diverso se desidera utilizzare una convenzione di denominazione del file diversa (ad esempio per includere il nome del server se i file di log vengono salvati in una posizione centrale).|Yes|  
|HTTPTraceSwitches|Questo valore è facoltativo. Se lo si specifica, è possibile configurare i campi utilizzati nel file di log in formato delimitato da virgole.|No|  
|date|Data di esecuzione dell'attività.|No|  
|Time|Ora di esecuzione dell'attività.|No|  
|ClientIp|Indirizzo IP del client che ha eseguito l'accesso al server di report.|Yes|  
|UserName|Nome dell'utente che ha eseguito l'accesso al server di report.|No|  
|ServerPort|Numero della porta utilizzata per la connessione.|No|  
|Host|Contenuto dell'intestazione host.|No|  
|Metodo|Azione o metodo SOAP chiamato dal client.|Yes|  
|UriStem|Risorsa cui è stato eseguito l'accesso.|Yes|  
|UriQuery|Query utilizzata per accedere alla risorsa.|No|  
|ProtocolStatus|Codice di stato HTTP.|Yes|  
|BytesReceived|Numero di byte ricevuti dal server.|No|  
|TimeTaken|Tempo (in millisecondi) dall'istante in cui HTTP.SYS restituisce i dati della richiesta fino al momento in cui il server completa l'ultimo invio, ad eccezione del tempo di trasmissione della rete.|No|  
|ProtocolVersion|Versione del protocollo utilizzata dal client.|No|  
|UserAgent|Tipo di browser utilizzato dal client.|No|  
|CookieReceived|Contenuto del cookie ricevuto dal server.|No|  
|CookieSent|Contenuto del cookie inviato dal server.|No|  
|Referrer|Sito precedente visitato dal client.|No|  
  
## <a name="see-also"></a>Vedere anche  
 [Report Server Service Trace Log](report-server-service-trace-log.md)   
 [File di log e origini di Reporting Services](../report-server/reporting-services-log-files-and-sources.md)   
 [Guida di riferimento a errori ed eventi &#40;Reporting Services&#41;](../troubleshooting/errors-and-events-reference-reporting-services.md)  
  
  
