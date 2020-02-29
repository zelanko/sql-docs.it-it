---
title: Log di traccia del servizio del server di report | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- logs [Reporting Services], trace
- traces [Reporting Services]
- system information [Reporting Services]
- versions [Reporting Services]
ms.assetid: 2fde08b2-137d-4f4b-88e5-216030216e0d
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 76a3f406f04f2f34be2efdc046279edc51f30b4b
ms.sourcegitcommit: 2d4067fc7f2157d10a526dcaa5d67948581ee49e
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/28/2020
ms.locfileid: "78177202"
---
# <a name="report-server-service-trace-log"></a>Report Server Service Trace Log
  Il log di traccia del server di report di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] è un file di testo ASCII che contiene informazioni dettagliate relative alle operazioni del servizio del server di report, ad esempio operazioni eseguite dal servizio Web ReportServer, da Gestione report e dall'elaborazione in background. Nel file di log di traccia sono contenute inoltre informazioni ridondanti, che vengono registrate in altri file di log, e informazioni aggiuntive non disponibili altrove. Le informazioni contenute nel log di traccia sono utili se si esegue il debug di un'applicazione che include un server di report o se è necessario analizzare un problema specifico scritto nel log eventi o nel log di esecuzione.

> [!NOTE]
>  Nelle versioni precedenti sono presenti più file di log di traccia, uno per ogni applicazione. I file seguenti sono obsoleti e non vengono più creati [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] in e versioni successive: ReportServerWebApp_*\<timestamp>*. log, ReportServer_*\<timestamp>*. log e ReportServerService_main_*\<timestamp>*. log.

 **Contenuto dell'argomento:**

-   [Dove si trovano i file di log del server di report?](#bkmk_view_log)

-   [Impostazioni di configurazione della traccia](#bkmk_trace_configuration_settings)

-   [Aggiunta di un'impostazione di configurazione personalizzata per specificare il percorso di un file di dump](#bkmk_add_custom)

-   [Campi del file di log](#bkmk_log_file_fields)

##  <a name="bkmk_view_log"></a>Dove si trovano i file di log del server di report?
 I file di log di traccia sono denominati `ReportServerService_<timestamp>.log` e si trovano nella cartella seguente:

 `C:\Program Files\Microsoft SQL Server\MSRS12.MSSQLSERVER\Reporting Services\LogFiles`

 I log di traccia vengono creati quotidianamente, a partire dalla prima voce registrata dopo la mezzanotte (ora locale) e tutte le volte in cui il servizio viene riavviato. Il timestamp si basa su l'ora UTC (Coordinated Universal Time). Il file è in formato en-US Per impostazione predefinita, i log di traccia possono occupare uno spazio massimo di 32 MB e vengono eliminati dopo 14 giorni.

 Visualizzare un breve video che illustra l'uso di Microsoft Power Query per visualizzare i file di log di [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] .

 ![visualizzare un video sui log di Power Query e SSRS](../media/generic-video-thumbnail.png "visualizzare un video sui log di Power Query e SSRS")

##  <a name="bkmk_trace_configuration_settings"></a>Impostazioni di configurazione della traccia
 Il comportamento del log di traccia viene gestito nel file di configurazione **ReportingServicesService. exe. config**. Il file di configurazione si trova nel percorso della cartella seguente:

 `\Program Files\Microsoft SQL Server\MSRS12.<instance name>\Reporting Services\ReportServer\bin`.

 Nell'esempio seguente viene illustrata la struttura XML delle impostazioni `RStrace`. Il valore di `DefaultTraceSwitch` determina il tipo di informazioni aggiunte al log. Con l'eccezione dell'attributo `Components`, i valori per `RStrace` sono uguali in tutti i file di configurazione.

```
<system.diagnostics>
      <switches>
          <add name="DefaultTraceSwitch" value="3" />
      </switches>
</system.diagnostics>
<RStrace>
      <add name="FileName" value="ReportServerService_" />
      <add name="FileSizeLimitMb" value="32" />
      <add name="KeepFilesForDays" value="14" />
      <add name="Prefix" value="tid, time" />
      <add name="TraceListeners" value="file" />
      <add name="TraceFileMode" value="unique" />
      <add name="Components" value="all" />
</RStrace>
```

 Nella tabella seguente sono incluse informazioni su ogni impostazione.

|Impostazione|Descrizione|
|-------------|-----------------|
|`RStrace`|Specifica gli spazi dei nomi utilizzati per errori e traccia.|
|`DefaultTraceSwitch`|Specifica il livello delle informazioni da includere nel log di traccia ReportServerService. Ogni livello include anche le informazioni raccolte da tutti i livelli inferiori. Non è consigliabile disabilitare la funzionalità di traccia. I valori validi sono:<br /><br /> 0= Disabilita la funzionalità di traccia. Il file di log ReportServerService è abilitato per impostazione predefinita. Per disattivarlo, impostare il livello di traccia su 0.<br /><br /> 1= Eccezioni e riavvii<br /><br /> 2= Eccezioni, riavvii, avvisi<br /><br /> 3= Eccezioni, riavvii, avvisi, messaggi di stato (valore predefinito)<br /><br /> 4= Modalità dettagliata|
|**FileName**|Specifica la prima parte del nome del file di log. Il resto del nome viene completato con il valore specificato da `Prefix`.|
|**FileSizeLimitMb**|Specifica il limite massimo per le dimensioni del log di traccia. Il file è misurato in megabyte. I valori validi sono compresi tra 0 e il valore integer massimo. Il valore predefinito è (32). Se si specifica 0 o un numero negativo, il server di report lo considera come 1.<br /><br /> È possibile controllare le dimensioni del file impostando i livelli di traccia da 0 a 4 per definire la quantità di contenuto registrata. È inoltre possibile specificare i componenti per la traccia. Se il valore massimo del file di log viene raggiunto prima della data di scadenza di 14 giorni, le voci meno recenti verranno sostituite con le voci nuove.|
|**KeepFilesForDays**|Specifica dopo quanti giorni un file di log di traccia viene eliminato. I valori validi sono compresi tra 0 e il valore integer massimo. Il valore predefinito è 14. Se si specifica 0 o un numero negativo, il server di report lo considera come 1.|
|`Prefix`|Specifica un valore generato che distingue ogni istanza del log dalle altre. Per impostazione predefinita, ai nomi file dei log di traccia vengono aggiunti valori timestamp. Questo valore è impostato su "tid, time". Non modificare questa impostazione.|
|**TraceListeners**|Specifica una destinazione per l'output del contenuto del log di traccia. È possibile specificare più destinazioni, separandole con una virgola. I valori validi sono:<br /><br /> DebugWindow<br /><br /> File (valore predefinito)<br /><br /> StdOut|
|**TraceFileMode**|Specifica se i log di traccia devono contenere dati per un periodo di 24 ore. È consigliabile utilizzare un solo log di traccia al giorno per ogni componente. Questo valore è impostato su "Unique" (valore predefinito). Non modificare questo valore.|
|`Components`|Specifica i componenti per i quali vengono generate informazioni nel log di traccia e il livello di traccia nel formato seguente:<br /><br /> 
  \<categoria componente>:\<livellotraccia><br /><br /> Le categorie dei componenti possono essere impostate nei modi seguenti:<br />Il valore `All` viene utilizzato per tracciare l'attività generale del server di report per tutti i processi che non sono suddivisi in categorie specifiche.<br />Il valore `RunningJobs` viene utilizzato per tracciare un report o un'operazione di sottoscrizione in corso.<br />Il valore `SemanticQueryEngine` viene utilizzato per tracciare una query semantica elaborata quando un utente esegue un'esplorazione dei dati ad hoc in un report basato su modello.<br />Il valore `SemanticModelGenerator` viene utilizzato per tracciare la generazione del modello.<br />Il valore `http` viene utilizzato per abilitare il file di log HTTP del server di report. Per ulteriori informazioni, vedere [Report Server HTTP Log](report-server-http-log.md).<br /><br /> <br /><br /> I valori validi del livello di traccia sono i seguenti:<br /><br /> 0= Disabilita la funzionalità di traccia<br /><br /> 1= Eccezioni e riavvii<br /><br /> 2= Eccezioni, riavvii, avvisi<br /><br /> 3= Eccezioni, riavvii, avvisi, messaggi di stato (valore predefinito)<br /><br /> 4= Modalità dettagliata<br /><br /> Il valore predefinito per il server di report è: "all:3".<br /><br /> È possibile specificare tutti i componenti o solo alcuni (`all`, `RunningJobs`, `SemanticQueryEngine`, `SemanticModelGenerator`). Se non si desidera generare informazioni per un componente specifico, è possibile disabilitare la traccia per tale componente (ad esempio "SemanticModelGenerator:0"). Non disabilitare la funzionalità di traccia per il componente `all`.<br /><br /> Se non si aggiunge un livello di traccia dopo il nome del componente, verrà utilizzato il valore specificato per `DefaultTraceSwitch`. Ad esempio, se si specifica "all,RunningJobs,SemanticQueryEngine,SemanticModelGenerator", per tutti i componenti verrà utilizzato il livello di traccia predefinito.<br /><br /> È possibile impostare "SemanticQueryEngine:4" se si desidera visualizzare le istruzioni Transact-SQL che vengono generate per ogni query semantica. Le istruzioni Transact-SQL vengono registrate nel log di traccia. Nell'esempio seguente viene illustrata l'impostazione di configurazione per l'aggiunta delle istruzioni Transact-SQL al log:<br /><br /> 
  \<add name="Components" value="all,SemanticQueryEngine:4" />|

##  <a name="bkmk_add_custom"></a> Aggiunta di un'impostazione di configurazione personalizzata per specificare il percorso del file di dump
 È possibile aggiungere un'impostazione personalizzata per definire la directory di archiviazione utilizzata dallo strumento Dr. Watson per Windows per archiviare i file di dump. L'impostazione personalizzata è `Directory`. Nell'esempio seguente viene illustrato come specificare questa impostazione di configurazione nella sezione `RStrace`:

```
<add name="Directory" value="U:\logs\" />
```

 Per ulteriori informazioni, vedere l' [articolo della Knowledge Base 913046](https://support.microsoft.com/?kbid=913046) nel sito Web [!INCLUDE[msCoName](../../includes/msconame-md.md)] .

##  <a name="bkmk_log_file_fields"></a> Campi del file di log
 Nei log di traccia sono disponibili i campi seguenti:

-   Informazioni sul sistema, quali il sistema operativo, la versione, il numero di processori e la memoria.

-   [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] e sulla versione.

-   Eventi registrati nel registro applicazioni.

-   Eccezioni generate dal server di report.

-   Avvisi di risorse insufficienti registrati da un server di report.

-   Buste SOAP in ingresso e buste SOAP in uscita riepilogate.

-   Informazioni sull'intestazione HTTP, sull'analisi dello stack e sulla traccia di debug.

 Esaminando le informazioni dei log di traccia è possibile stabilire se ha avuto luogo un recapito di report, chi ha ricevuto il report e quanti tentativi di recapito sono stati eseguiti. Nei log di traccia vengono inoltre registrati l'attività di esecuzione del report e le variabili di ambiente attive durante l'elaborazione del report, nonché gli errori e le eccezioni. È possibile, ad esempio, trovare errori di timeout nel report, indicati dalla voce `ThreadAbortExceptions`.

## <a name="see-also"></a>Vedere anche
 [Reporting Services file di log e origini](../report-server/reporting-services-log-files-and-sources.md) [errori ed eventi di riferimento &#40;Reporting Services&#41;](../troubleshooting/errors-and-events-reference-reporting-services.md)


