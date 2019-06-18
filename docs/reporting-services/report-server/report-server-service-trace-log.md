---
title: Report Server Service Trace Log
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server
ms.topic: conceptual
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.reviewer: ''
ms.custom: ''
ms.date: 04/23/2019
ms.openlocfilehash: d1efc5b57191ec17f610206115743b656d58d4b3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "65581391"
---
# <a name="report-server-service-trace-log"></a>Report Server Service Trace Log

Il log di traccia del server di report di [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] è un file di testo ASCII che contiene informazioni dettagliate relative alle operazioni del servizio del server di report.  Le informazioni nei file includono le operazioni eseguite dal servizio Web ReportServer, dal portale Web e dall'elaborazione in background. Nel file di log di traccia sono contenute inoltre informazioni ridondanti, che vengono registrate in altri file di log, e informazioni aggiuntive non disponibili altrove. Le informazioni contenute nel log di traccia sono utili se si esegue il debug di un'applicazione che include un server di report o se è necessario analizzare un problema specifico scritto nel log eventi o nel log di esecuzione, ad esempio durante la risoluzione dei problemi relativi alle sottoscrizioni.  

## <a name="bkmk_view_log"></a> Dove si trovano i file di log del server di report?

I file di log di traccia sono `ReportServerService_<timestamp>.log` e `Microsoft.ReportingServices.Portal.WebHost_<timestamp>.log` e si trovano nella cartella seguente:

`C:\Program Files\Microsoft SQL Server\MSRS13.MSSQLSERVER\Reporting Services\LogFiles` 

I log di traccia vengono creati quotidianamente, a partire dalla prima voce registrata dopo la mezzanotte (ora locale) e tutte le volte in cui il servizio viene riavviato. Il timestamp si basa su l'ora UTC (Coordinated Universal Time). Il file è in formato en-US Per impostazione predefinita, i log di traccia possono occupare uno spazio massimo di 32 MB e vengono eliminati dopo 14 giorni.  

## <a name="bkmk_trace_configuration_settings"></a> Impostazioni di configurazione della traccia

Il comportamento del log di traccia viene gestito nel file di configurazione **ReportingServicesService.exe.config**. Il file di configurazione si trova nel seguente percorso:  
  
 `\Program Files\Microsoft SQL Server\MSRS13.<instance name>\Reporting Services\ReportServer\bin`.  
  
 L'esempio seguente illustra la struttura XML delle impostazioni di **RStrace** . Il valore di **DefaultTraceSwitch** determina il tipo di informazioni aggiunte al log. A eccezione dell'attributo **Components** , i valori per **RStrace** sono uguali in tutti i file di configurazione.  
  
```
  \<system.diagnostics>
    <switches>
      <add name="DefaultTraceSwitch" value="3" />
    </switches>
  \</system.diagnostics>
  <RStrace>
    <add name="FileName" value="ReportServerService_" />
    <add name="FileSizeLimitMb" value="32" />
    <add name="KeepFilesForDays" value="14" />
    <add name="Prefix" value="appdomain, tid, time" />
    <add name="TraceListeners" value="file" />
    <add name="TraceFileMode" value="unique" />
    <add name="Components" value="all:3" />
  </RStrace>
```  
  
 Nella tabella seguente sono incluse informazioni su ogni impostazione.  
  
|Impostazione|Descrizione|Valori|  
|-------------|-----------------|------------|  
|**RStrace**|Specifica gli spazi dei nomi utilizzati per errori e traccia.||  
|**DefaultTraceSwitch**|Specifica il livello delle informazioni da includere nel log di traccia ReportServerService. Ogni livello include anche le informazioni raccolte da tutti i livelli inferiori. Non è consigliabile disabilitare la funzionalità di traccia.|I valori validi sono:<br /><br /> <br /><br /> 0= Disabilita la funzionalità di traccia. Il file di log ReportServerService è abilitato per impostazione predefinita. Per disattivarlo, impostare il livello di traccia su 0.<br /><br /> 1= Eccezioni e riavvii<br /><br /> 2= Eccezioni, riavvii, avvisi<br /><br /> 3= Eccezioni, riavvii, avvisi, messaggi di stato (valore predefinito)<br /><br /> 4= Modalità dettagliata|  
|**FileName**|Specifica la prima parte del nome del file di log. Il resto del nome viene completato con il valore specificato da **Prefix** .||  
|**FileSizeLimitMb**|Specifica il limite massimo per le dimensioni del log di traccia. Il file è misurato in megabyte.<br /><br /> È possibile controllare le dimensioni del file impostando i livelli di traccia da 0 a 4 per definire la quantità di contenuto registrata. È inoltre possibile specificare i componenti per la traccia. Se il valore massimo del file di log viene raggiunto prima della data di scadenza di 14 giorni, le voci meno recenti verranno sostituite con le voci più recenti.|I valori validi sono compresi tra 0 e il valore integer massimo. Il valore predefinito è (32). Se si specifica 0 o un numero negativo, il server di report lo considera come 1.|  
|**KeepFilesForDays**|Specifica dopo quanti giorni un file di log di traccia viene eliminato.|I valori validi sono compresi tra 0 e il valore integer massimo. Il valore predefinito è 14. Se si specifica 0 o un numero negativo, il server di report lo considera come 1.|  
|**Prefix**|Specifica un valore generato che consente di distinguere ogni istanza del log dalle altre.|Per impostazione predefinita, ai nomi file dei log di traccia vengono aggiunti valori timestamp. Questo valore è impostato su "appdomain, tid, time". Non modificare questa impostazione.|  
|**TraceListeners**|Specifica una destinazione per l'output del contenuto del log di traccia. È possibile specificare più destinazioni, separandole con una virgola.|I valori validi sono:<br /><br /> <br /><br /> DebugWindow<br /><br /> File (valore predefinito)<br /><br /> StdOut|  
|**TraceFileMode**|Specifica se i log di traccia devono contenere dati per un periodo di 24 ore. È consigliabile utilizzare un solo log di traccia al giorno per ogni componente.|Questo valore è impostato su "Unique" (valore predefinito). Non modificare questo valore.|  
|**Categoria del componente**|Specifica i componenti per i quali vengono generate informazioni nel log di traccia e il livello di traccia nel formato seguente:<br /><br /> \<categoria componente>:\<livellotraccia><br /><br /> È possibile specificare tutti i componenti o solo alcuni (**all**, **RunningJobs**, **SemanticQueryEngine**, **SemanticModelGenerator**). Se non si desidera generare informazioni per un componente specifico, è possibile disabilitare la traccia per tale componente (ad esempio "SemanticModelGenerator:0"). Non disabilitare la funzionalità di traccia per il componente **all**.<br /><br /> È possibile impostare "SemanticQueryEngine:4" se si desidera visualizzare le istruzioni Transact-SQL che vengono generate per ogni query semantica. Le istruzioni Transact-SQL vengono registrate nel log di traccia. Nell'esempio seguente viene illustrata l'impostazione di configurazione per l'aggiunta delle istruzioni Transact-SQL al log:<br /><br /> \<add name="Components" value="all,SemanticQueryEngine:4" />|Le categorie dei componenti possono essere impostate nei modi seguenti:<br /><br /> <br /><br /> Il valore**All** viene usato per tracciare l'attività generale del server di report per tutti i processi che non sono suddivisi in categorie specifiche.<br /><br /> Il valore**RunningJobs** viene usato per tracciare un report o un'operazione di sottoscrizione in corso.<br /><br /> Il valore**SemanticQueryEngine** viene usato per tracciare una query semantica elaborata quando un utente esegue un'esplorazione dei dati ad hoc in un report basato su modello.<br /><br /> Il valore**SemanticModelGenerator** viene usato per tracciare la generazione del modello.<br /><br /> Il valore**http** viene usato per abilitare il file di log HTTP del server di report. Per ulteriori informazioni, vedere [Report Server HTTP Log](../../reporting-services/report-server/report-server-http-log.md).|  
|Valore**tracelevel** per categorie di componenti|\<categoria componente>:\<livellotraccia><br /><br /> <br /><br /> Se non si aggiunge un livello di traccia dopo il nome del componente, verrà usato il valore specificato per **DefaultTraceSwitch** . Ad esempio, se si specifica "all,RunningJobs,SemanticQueryEngine,SemanticModelGenerator", per tutti i componenti verrà utilizzato il livello di traccia predefinito.|I valori validi del livello di traccia sono i seguenti:<br /><br /> <br /><br /> 0= Disabilita la funzionalità di traccia<br /><br /> 1= Eccezioni e riavvii<br /><br /> 2= Eccezioni, riavvii, avvisi<br /><br /> 3= Eccezioni, riavvii, avvisi, messaggi di stato (valore predefinito)<br /><br /> 4= Modalità dettagliata<br /><br /> Il valore predefinito per il server di report è: "all:3".|  
  
## <a name="bkmk_add_custom"></a> Aggiunta di un'impostazione di configurazione personalizzata per specificare il percorso del file di dump  
È possibile aggiungere un'impostazione personalizzata per definire la directory di archiviazione utilizzata dallo strumento Dr. Watson per Windows per archiviare i file di dump. L'impostazione personalizzata è **Directory**. L'esempio seguente illustra come specificare questa impostazione di configurazione nella sezione **RStrace** :  

```
<add name="Directory" value="U:\logs\" />  
```  
  
Per ulteriori informazioni, vedere l' [articolo della Knowledge Base 913046](https://support.microsoft.com/?kbid=913046) nel sito Web [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
##  <a name="bkmk_log_file_fields"></a> Campi del file di log

Nei log di traccia sono disponibili i campi seguenti:  
  
- Informazioni sul sistema, quali il sistema operativo, la versione, il numero di processori e la memoria.  
  
- [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] e sulla versione.  
  
- Eventi registrati nel registro applicazioni.  
  
- Eccezioni generate dal server di report.  
  
- Avvisi di risorse insufficienti registrati da un server di report.  
  
- Buste SOAP in ingresso e buste SOAP in uscita riepilogate.  
  
- Informazioni sull'intestazione HTTP, sull'analisi dello stack e sulla traccia di debug.  
  
 Esaminando le informazioni dei log di traccia è possibile stabilire se ha avuto luogo un recapito di report, chi ha ricevuto il report e quanti tentativi di recapito sono stati eseguiti. Nei log di traccia vengono inoltre registrati l'attività di esecuzione del report e le variabili di ambiente attive durante l'elaborazione del report, nonché gli errori e le eccezioni. È possibile, ad esempio, trovare errori di timeout nel report, indicati dalla voce **ThreadAbortExceptions** .  

## <a name="previous-versions"></a>Versioni precedenti

Nelle versioni precedenti di [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)]sono presenti più file di log di traccia, uno per ogni applicazione. I file seguenti sono obsoleti e non vengono più creati in [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] e versioni successive:
+ ReportServerWebApp_ *\<timestamp>* .log
+ ReportServer_ *\<timestamp>* .log
+ ReportServerService_main_ *\<timestamp>* .log
  
## <a name="see-also"></a>Vedere anche

- [File di log e origini di Reporting Services](../../reporting-services/report-server/reporting-services-log-files-and-sources.md)   
- [Guida di riferimento a errori ed eventi &#40;Reporting Services&#41;](../../reporting-services/troubleshooting/errors-and-events-reference-reporting-services.md)  

Altre domande? [Visitare il forum su Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)