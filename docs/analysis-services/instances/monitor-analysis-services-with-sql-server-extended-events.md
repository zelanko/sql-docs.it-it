---
title: Monitorare Analysis Services con eventi estesi di SQL Server | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: dc51c444483dc9a89cf0b9edbd557c3dce11a054
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62709251"
---
# <a name="monitor-analysis-services-with-sql-server-extended-events"></a>Monitorare Analysis Services con eventi estesi di SQL Server
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas-all-aas.md)]
  Gli eventi estesi (*xEvents*) rappresentano un sistema di monitoraggio delle prestazioni e di traccia leggero, che usa una quantità molto limitata di risorse di sistema. Sono quindi uno strumento ideale per la diagnosi dei problemi, sia nei server di produzione che in quelli di prova. È anche un sistema altamente scalabile e che offre ampie possibilità di configurazione, oltre a essere più facile da usare in SQL Server 2016 grazie al nuovo supporto predefinito dello strumento. In SQL Server Management Studio, per le connessioni a istanze di Analysis Services, è possibile configurare, eseguire e monitorare una traccia in tempo reale, in modo simile all'uso di SQL Server Profiler. L'aggiunta di strumenti migliori dovrebbe rendere XEvents una sostituzione più ragionevole per SQL Server Profiler e creare maggiore simmetria per le modalità di diagnosi dei problemi nel motore di database e nei carichi di lavoro di Analysis Services.  
  
 Oltre a [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], per la configurazione delle sessioni di eventi estesi di  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è anche possibile usare la modalità precedente, tramite script XMLA, supportata nelle versioni precedenti.  
  
 Tutti gli eventi di Analysis Services possono essere acquisiti e indirizzati a consumer specifici, come definito in [Eventi estesi](../../relational-databases/extended-events/extended-events.md).  
  
> [!NOTE]  
>  Per sapere di più su xEvents per Analysis Services in SQL Server 2016, guardare questa [breve introduzione video](https://www.youtube.com/watch?v=ja2mOHWRVC0&index=1&list=PLv2BtOtLblH1YvzQ5YnjfQFr_oKEvMk19) o leggere il [post di blog di supporto](http://blogs.msdn.com/b/analysisservices/archive/2015/09/22/using-extended-events-with-sql-server-analysis-services-2016-cpt-2-3.aspx) .  
  
  
##  <a name="bkmk_ssas_extended_events_ssms"></a> Usare Management Studio per configurare Analysis Services  
 Sia per le istanze tabulari che per quelle multidimensionali, Management Studio include una nuova cartella Gestione che contiene le sessioni xEvents avviate dall'utente. È possibile eseguire più sessioni contemporaneamente. Nell'implementazione corrente, tuttavia, l'interfaccia utente degli eventi estesi di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] non supporta l'aggiornamento o la riproduzione di una sessione esistente.  
  
 ![ssas_extended_events_ssms_start](../../analysis-services/instances/media/ssas-extended-events-ssms-start.png "ssas_extended_events_ssms_start")  
  
 **Scegliere gli eventi**  
  
 Se si conoscono già gli eventi da acquisire, cercarli è il modo più semplice per aggiungerli alla traccia. In caso contrario, gli eventi seguenti sono comunemente usati per le operazioni di monitoraggio:  
  
-   **CommandBegin** e **CommandEnd**.  
  
-   **QueryBegin**, **QueryEnd**e **QuerySubcubeVerbose** (visualizza l'intera query MDX o DAX inviata al server), oltre a **ResourceUsage** per statistiche sulle risorse usate dalla query e il numero di righe restituite.  
  
-   **ProgressReportBegin** e **ProgressReportEnd** (per operazioni di elaborazione).  
  
-   **AuditLogin** e **AuditLogout** (acquisisce l'identità dell'utente con cui un'applicazione client si connette ad Analysis Services).  
  
 **Scelta della modalità di archiviazione dei dati**  
  
 È possibile visualizzare una sessione in tempo reale in una finestra in Management Studio oppure salvarla in un file per analisi successive tramite Power Query o Excel.  
  
-   **event_file** archivia i dati della sessione in un file con estensione xel.  
  
-   **event_stream** abilita l'opzione **Controlla i dati dinamici** in Management Studio.  
  
-   **ring_buffer** archivia i dati della sessione in memoria fino a quando il server è in esecuzione. In caso di riavvio del server, i dati della sessione vengono eliminati.  
  
 **Aggiungere campi evento**  
  
 Assicurarsi di configurare la sessione in modo da includere campi evento, per poter visualizzare facilmente le informazioni di interesse.  
  
 **Configura** è un'opzione all'estrema destra della finestra di dialogo.  
  
 ![ssas-xevents-configure](../../analysis-services/instances/media/ssas-xevents-configure.PNG "ssas-xevents-configure")  
  
 Nella configurazione, nella scheda Campi evento, selezionare **TextData** in modo da visualizzare il campo accanto all'evento per mostrare i valori restituiti, incluse le query in esecuzione nel server.  
  
 Dopo aver configurato gli eventi desiderati e la modalità di archiviazione dei dati per una sessione, è possibile fare clic sul pulsante di script per inviare la configurazione a una delle destinazioni supportate, tra cui un file, una nuova query in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e gli Appunti.  
  
 **Aggiornare le sessioni**  
  
 Dopo aver creato la sessione, assicurarsi di aggiornare la cartella Sessioni in Management Studio per visualizzare la sessione appena creata. Se è stata configurata l'opzione event_stream, è possibile fare clic con il pulsante destro del mouse sul nome della sessione e scegliere **Controlla dati dinamici** per monitorare l'attività del server in tempo reale.  
  
##  <a name="bkmk_script_start"></a> Script XMLA per avviare eventi estesi in Analysis Services  
 La traccia di eventi estesi viene abilitata utilizzando una specifica XMLA simile per creare un comando script dell'oggetto come illustrato di seguito:  
  
```  
<Execute ...>  
   <Command>  
      <Batch ...>  
         <Create ...>  
            <ObjectDefinition>  
               <Trace>  
                  <ID>trace_id</ID>  
                  <Name>trace_name</Name>  
                  <ddl300_300:XEvent>  
                     <event_session ...>  
                        <event package="AS" name="AS_event">  
                           <action package="PACKAGE0" .../>  
                        </event>  
                        <target package="PACKAGE0" name="asynchronous_file_target">  
                           <parameter name="filename" value="data_filename.xel"/>  
                           <parameter name="metadatafile" value="metadata_filename.xem"/>  
                        </target>  
                     </event_session>  
                  </ddl300_300:XEvent>  
               </Trace>  
            </ObjectDefinition>  
         </Create>  
      </Batch>  
   </Command>  
   <Properties></Properties>  
</Execute>  
  
```  
  
 A seconda delle necessità di traccia, gli elementi seguenti devono essere definiti dall'utente:  
  
 *trace_id*  
 Consente di definire l'identificatore univoco per questa traccia.  
  
 *trace_name*  
 Nome fornito a questa traccia; generalmente una definizione leggibile della traccia. È pratica comune usare il valore *trace_id* come nome.  
  
 *AS_event*  
 Evento di Analysis Services da esporre. Vedere [Eventi di traccia di Analysis Services](https://docs.microsoft.com/bi-reference/trace-events/analysis-services-trace-events) per i nomi degli eventi.  
  
 *data_filename*  
 Nome del file in cui sono contenuti i dati degli eventi. Nel nome è incluso un suffisso timestamp per evitare la sovrascrittura dei dati qualora la traccia venga inviata ripetutamente.  
  
 *metadata_filename*  
 Nome del file in cui sono contenuti i metadati degli eventi. Nel nome è incluso un suffisso timestamp per evitare la sovrascrittura dei dati qualora la traccia venga inviata ripetutamente.  
  
  
##  <a name="bkmk_script_stop"></a> Script XMLA per arrestare eventi estesi in Analysis Services  
 Per arrestare l'oggetto traccia di eventi estesi è necessario eliminare tale oggetto utilizzando una specifica XMLA simile per eliminare un comando script dell'oggetto come illustrato di seguito:  
  
```  
<Execute xmlns="urn:schemas-microsoft-com:xml-analysis">  
   <Command>  
      <Batch ...>  
         <Delete ...>  
            <Object>  
               <TraceID>trace_id</TraceID>  
            </Object>  
         </Delete>  
      </Batch>  
   </Command>  
   <Properties></Properties>  
</Execute>  
  
```  
  
 A seconda delle necessità di traccia, gli elementi seguenti devono essere definiti dall'utente:  
  
 *trace_id*  
 Consente di definire l'identificatore univoco della traccia da eliminare.  
  
  
## <a name="see-also"></a>Vedere anche  
 [Eventi estesi](../../relational-databases/extended-events/extended-events.md)  
  
  
