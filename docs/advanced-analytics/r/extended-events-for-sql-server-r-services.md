---
title: Eventi estesi per il monitoraggio dei processi R e Python
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: conceptual
author: dphansen
ms.author: davidph
ms.openlocfilehash: e0e685543fe1e99f7adbfeb69567c366b0714ef7
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/24/2019
ms.locfileid: "68470171"
---
# <a name="extended-events-for-sql-server-machine-learning-services"></a>Eventi estesi per SQL Server Machine Learning Services
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

SQL Server fornisce un set di eventi estesi da usare per la [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]risoluzione dei problemi relativi a, oltre ai processi Python o R inviati a. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]

**Si applica a:**  SQL Server 2016 R Services, SQL Server 2017 Machine Learning Services

## <a name="sql-server-events-for-machine-learning"></a>Eventi SQL Server per Machine Learning

Per visualizzare un elenco di eventi relativi a SQL Server, eseguire la query seguente da [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].

```sql
SELECT o.name AS event_name, o.description
FROM sys.dm_xe_objects o
JOIN sys.dm_xe_packages p
ON o.package_guid = p.guid
WHERE o.object_type = 'event'
AND p.name = 'SQLSatellite';
```

Per informazioni generali sull'uso di eventi estesi, vedere [strumenti degli eventi estesi](https://docs.microsoft.com/sql/relational-databases/extended-events/extended-events-tools).

> [!TIP]
> Per gli eventi estesi generati da SQL Server, provare il nuovo Profiler [XEvent di SSMS](https://docs.microsoft.com/sql/relational-databases/extended-events/use-the-ssms-xe-profiler). Questa nuova funzionalità di Management Studio Visualizza un visualizzatore Live per gli eventi estesi ed è meno intrusivo per l'SQL Server rispetto a una traccia di Profiler simile.

## <a name="additional-events-specific-to-machine-learning-components"></a>Eventi aggiuntivi specifici dei componenti di Machine Learning

Sono disponibili altri eventi estesi per i componenti correlati e usati da SQL Server Machine Learning Services, ad esempio [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)], e BXLServer, il processo satellite che avvia il runtime di R. Questi eventi estesi aggiuntivi vengono generati dai processi esterni e pertanto devono essere acquisiti utilizzando un'utilità esterna.

Per ulteriori informazioni su come eseguire questa operazione, vedere la sezione [raccolta di eventi da processi esterni](#bkmk_externalevents).

##  <a name="bkmk_xeventtable"></a>Tabella degli eventi estesi

|event|Descrizione|Note|  
|-----------|-----------------|---------|  
|connection_accept|Si verifica quando viene accettata una nuova connessione. Questo evento viene usato per registrare tutti i tentativi di connessione.||  
|failed_launching|Avvio non riuscito.|Indica un errore.|  
|satellite_abort_connection|Record di interruzione della connessione.||  
|satellite_abort_received|Generato quando viene ricevuto un messaggio di interruzione su una connessione satellite.||  
|satellite_abort_sent|Generato quando viene inviato un messaggio di interruzione su una connessione satellite.||  
|satellite_authentication_completion|Generato quando viene completata l'autenticazione per una connessione su TCP o Namedpipe.||  
|satellite_authorization_completion|Generato quando viene completata l'autorizzazione per una connessione su TCP o Namedpipe.||  
|satellite_cleanup|Generato quando il satellite chiama la pulizia.|Generato solo da processi esterni. Vedere le istruzioni sulla raccolta di eventi da processi esterni.|  
|satellite_data_chunk_sent|Generato quando la connessione satellite completa l'invio di un singolo blocco di dati.|L'evento indica il numero di righe inviate, il numero di colonne, il numero di pacchetti SNI usati e il tempo trascorso in millisecondi per l'invio del blocco. Le informazioni possono aiutare a determinare il tempo necessario per passare tipi di dati diversi e il numero di pacchetti usati.|  
|satellite_data_receive_completion|Generato quando vengono ricevuti tutti i dati richiesti da una query sulla connessione satellite.|Generato solo da processi esterni. Vedere le istruzioni sulla raccolta di eventi da processi esterni.|  
|satellite_data_send_completion|Generato quando vengono ricevuti tutti i dati richiesti per una sessione sulla connessione satellite.||  
|satellite_data_send_start|Generato quando viene avviata la trasmissione dei dati.| La trasmissione dei dati viene avviata immediatamente prima dell'invio del primo blocco di dati.|  
|satellite_error|Usato per tenere traccia degli errori del satellite di sql.||  
|satellite_invalid_sized_message|La dimensione del messaggio non è valida.||  
|satellite_message_coalesced|Usato per tenere traccia dei messaggi che si uniscono a livello di rete.||  
|satellite_message_ring_buffer_record|Record del buffer circolare del messaggio.||  
|satellite_message_summary|Informazioni di riepilogo sui messaggi.||  
|satellite_message_version_mismatch|Il campo della versione del messaggio non corrisponde.||  
|satellite_messaging|Usato per tenere traccia degli eventi di messaggistica (associazione, annullamento dell'associazione e così via).||  
|satellite_partial_message|Usato per tenere traccia dei messaggi parziali a livello di rete.||  
|satellite_schema_received|Generato quando il messaggio dello schema viene ricevuto e letto da SQL.||  
|satellite_schema_sent|Generato quando il messaggio dello schema viene inviato tramite il satellite.|Generato solo da processi esterni. Vedere le istruzioni sulla raccolta di eventi da processi esterni.|  
|satellite_service_start_posted|Generato quando avviare il servizio messaggio viene registrato nel Launchpad.|questo evento indica a Launchpad di avviare il processo esterno e contiene un ID per la nuova sessione.|  
|satellite_unexpected_message_received|Generato quando viene ricevuto un messaggio imprevisto.|Indica un errore.|  
|stack_trace|Si verifica alla richiesta di un dump di memoria del processo.|Indica un errore.|  
|trace_event|Usato a scopo di monitoraggio|Questi eventi possono contenere SQL Server, Launchpad e i messaggi di traccia dei processi esterni. Questi includono l'output in stdout e stderr da R.|  
|launchpad_launch_start|Generato quando Launchpad avvia un satellite.|Generato solo da Launchpad Vedere le istruzioni sulla raccolta di eventi da launchpad.exe.|  
|launchpad_resume_sent|Generato quando Launchpad ha avviato il satellite e inviato un messaggio di ripristino a SQL Server.|Generato solo da Launchpad Vedere le istruzioni sulla raccolta di eventi da launchpad.exe.|  
|satellite_data_chunk_sent|Generato quando la connessione satellite completa l'invio di un singolo blocco di dati.|Contiene informazioni sul numero di colonne, numero di righe, numero di pacchetti e sul tempo impiegato per l'invio del blocco.|  
|satellite_sessionId_mismatch|L'ID della sessione del messaggio non è previsto.||  
  
###  <a name="bkmk_externalevents"></a>Raccolta di eventi da processi esterni

SQL Server Machine Learning Services avvia alcuni servizi che vengono eseguiti all'esterno del processo di SQL Server. Per acquisire gli eventi correlati a questi processi esterni, è necessario creare un file di configurazione di traccia degli eventi e inserire il file nella stessa directory del file eseguibile del processo.  
  
+ **[!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)]**   
  
    Per acquisire gli eventi correlati a Launchpad, inserire il file *config* nella directory Binn per l'istanza di SQL Server.  In un'installazione predefinita, si tratta di:

    `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\MSSQL\Binn`.  
  
+ **BXLServer** è il processo satellite che supporta l'estendibilità di SQL con linguaggi di script esterni, ad esempio R o Python. Viene avviata un'istanza separata di BxlServer per ogni istanza di linguaggio esterno.
  
    Per acquisire gli eventi correlati a BXLServer, inserire il file *config* nella directory di installazione di R o Python.  In un'installazione predefinita, si tratta di:
     
    **R:** `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64`.  

    **Python:** `C:\Program Files\Microsoft SQL Server\MSSQL_version_number.MSSQLSERVER\PYTHON_SERVICES\library\RevoScaleR\rxLibs\x64`.

Il nome del file di configurazione deve corrispondere a quello dell'eseguibile, usando il formato "[nome]. XEvent. xml". In altre parole, i file devono essere denominati come segue:

+ `Launchpad.xevents.xml`
+ `bxlserver.xevents.xml`

Il file di configurazione presenta il formato seguente:

```xml
\<?xml version="1.0" encoding="utf-8"?>  
<event_sessions>  
<event_session name="[session name]" maxMemory="1" dispatchLatency="1" MaxDispatchLatency="2 SECONDS">  
    <description owner="you">Xevent for launchpad or bxl server.</description>  
    <event package="SQLSatellite" name="[XEvent Name 1]" />  
    <event package="SQLSatellite" name="[XEvent Name 2]" />  
    <target package="package0" name="event_file">  
      <parameter name="filename" value="[SessionName].xel" />  
      <parameter name="max_file_size" value="10" />  
      <parameter name="max_rollover_files" value="10" />  
    </target>  
  </event_session>  
</event_sessions>  
```

+ Per configurare la traccia, modificare il segnaposto del *nome della sessione* , il segnaposto`[SessionName].xel`per il nome del file () e i nomi degli eventi che si desidera acquisire `[XEvent Name 1]`, `[XEvent Name 1]`ad esempio,,.  
+ È possibile che venga visualizzato un numero qualsiasi di tag del pacchetto eventi che verrà raccolto purché l'attributo Name sia corretto.

### <a name="example-capturing-launchpad-events"></a>Esempio: Acquisizione degli eventi Launchpad

Nell'esempio seguente viene illustrata la definizione di una traccia di eventi per il servizio Launchpad:

```xml
\<?xml version="1.0" encoding="utf-8"?>  
<event_sessions>  
<event_session name="sqlsatelliteut" maxMemory="1" dispatchLatency="1" MaxDispatchLatency="2 SECONDS">  
    <description owner="hay">Xevent for sql tdd runner.</description>  
    <event package="SQLSatellite" name="launchpad_launch_start" />  
    <event package="SQLSatellite" name="launchpad_resume_sent" />  
    <target package="package0" name="event_file">  
      <parameter name="filename" value="launchpad_session.xel" />  
      <parameter name="max_file_size" value="10" />  
      <parameter name="max_rollover_files" value="10" />  
    </target>  
  </event_session>  
</event_sessions>  
```

+ Inserire il file *config* nella directory Binn per l'istanza di SQL Server.
+ Questo file deve essere denominato `Launchpad.xevents.xml`.

### <a name="example-capturing-bxlserver-events"></a>Esempio: Acquisizione degli eventi BXLServer  

L'esempio seguente illustra la definizione di una traccia di eventi per l'eseguibile di BXLServer.
  
```xml
\<?xml version="1.0" encoding="utf-8"?>  
<event_sessions>  
 <event_session name="sqlsatelliteut" maxMemory="1" dispatchLatency="1" MaxDispatchLatency="2 SECONDS">  
    <description owner="hay">Xevent for sql tdd runner.</description>  
    <event package="SQLSatellite" name="satellite_abort_received" />  
    <event package="SQLSatellite" name="satellite_authentication_completion" />  
    <event package="SQLSatellite" name="satellite_cleanup" />  
    <event package="SQLSatellite" name="satellite_data_receive_completion" />  
    <event package="SQLSatellite" name="satellite_data_send_completion" />  
    <event package="SQLSatellite" name="satellite_data_send_start" />  
    <event package="SQLSatellite" name="satellite_schema_sent" />   
    <event package="SQLSatellite" name="satellite_unexpected_message_received" />    
    <event package="SQLSatellite" name="satellite_data_chunk_sent" />   
    <target package="package0" name="event_file">  
      <parameter name="filename" value="satellite_session.xel" />  
      <parameter name="max_file_size" value="10" />  
      <parameter name="max_rollover_files" value="10" />  
    </target>  
  </event_session>  
</event_sessions>  
```

+ Inserire il file *config* nella stessa directory dell'eseguibile di BXLServer.
+ Questo file deve essere denominato `bxlserver.xevents.xml`.

## <a name="see-also"></a>Vedere anche

[Report Management Studio personalizzati per Machine Learning Services](../../advanced-analytics/r/monitor-r-services-using-custom-reports-in-management-studio.md)
