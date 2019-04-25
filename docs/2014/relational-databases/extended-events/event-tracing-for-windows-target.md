---
title: Destinazione di Event Tracing for Windows| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xevents
ms.topic: conceptual
helpviewer_keywords:
- event tracing for windows target
- ETW target
- targets [SQL Server extended events], event tracing for windows target
ms.assetid: ca2bb295-b7f6-49c3-91ed-0ad4c39f89d5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e855b9de09727a4437cad99a2534aee9d960298b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62519305"
---
# <a name="event-tracing-for-windows-target"></a>destinazione di Event Tracing for Windows
  Prima di utilizzare Event Tracing for Windows (ETW) come destinazione, è consigliabile acquisire familiarità con tale funzionalità. L'analisi ETW è utilizzata in abbinamento a Eventi estesi o come un consumer di eventi estesi. I collegamenti esterni seguenti rappresentano un punto iniziale per ottenere informazioni di base su ETW:  
  
-   [Eventi di Windows](https://go.microsoft.com/fwlink/?LinkId=92380)  
  
-   [Migliorare il debug e la regolazione delle prestazioni con ETW](https://go.microsoft.com/fwlink/?LinkId=92381)  
  
 Sebbene possa essere aggiunta a numerose sessioni, la destinazione ETW è una destinazione singleton. Se un evento viene generato in più sessioni, verrà propagato alla destinazione ETW solo una volta per ogni occorrenza. Il motore di Eventi estesi è limitato a un'unica istanza per processo.  
  
> [!IMPORTANT]  
>  Affinché la destinazione ETW funzioni, l'account di avvio del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] deve essere membro del gruppo Performance Log Users.  
  
 La configurazione degli eventi presente in una sessione ETW è controllata dal processo che ospita il motore di Eventi estesi. Il motore controlla gli eventi da generare e le condizioni che devono essere soddisfatte perché l'evento si verifichi.  
  
 Dopo avere eseguito un'associazione a una sessione di Eventi estesi, il che allega per la prima volta la destinazione ETW per la durata di un processo, la destinazione ETW apre una sola sessione ETW sul provider [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se una sessione ETW esiste già, la destinazione ETW ottiene un riferimento alla sessione esistente. Questa sessione ETW è condivisa in tutte le istanze [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] su un dato computer. Questa sessione ETW riceve tutti gli eventi da sessioni che possiedono la destinazione ETW.  
  
 Poiché ETW ha bisogno che i provider siano abilitati per utilizzare gli eventi e trasmetterli verso il basso a ETW, tutti i pacchetti di Eventi estesi sono attivati nella sessione. Quando un evento è generato, la destinazione ETW invia l'evento alla sessione sulla quale è abilitato il provider per l'evento.  
  
 La destinazione ETW supporta la pubblicazione sincrona di eventi sul thread che genera l'evento. Tale destinazione tuttavia non supporta la pubblicazione asincrona di eventi.  
  
 La destinazione ETW non supporta il controllo da controller ETW esterni, ad esempio Logman.exe. Per produrre tracce di ETW, una sessione dell'evento deve essere creata con la destinazione ETW. Per altre informazioni, vedere [CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql).  
  
> [!NOTE]  
>  Abilitando la destinazione ETW, viene creata una sessione ETW denominata XE_DEFAULT_ETW_SESSION. Se esiste già una sessione con il nome XE_DEFAULT_ETW_SESSION, viene utilizzata senza la modifica di alcuna proprietà della sessione esistente. La sessione XE_DEFAULT_ETW_SESSION viene condivisa tra tutte le istanze di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Dopo aver avviato XE_DEFAULT_ETW_SESSION, è necessario arrestarla tramite un controller ETW, quale lo strumento Logman. Ad esempio, è possibile eseguire il comando seguente al prompt dei comandi: `logman stop XE_DEFAULT_ETW_SESSION -ets`.  
  
 Nella tabella seguente vengono descritte le opzioni disponibili per la configurazione della destinazione ETW.  
  
|Opzione|Valori consentiti|Descrizione|  
|------------|--------------------|-----------------|  
|default_xe_session_name|Qualsiasi stringa contenente fino a 256 caratteri. Questo valore è facoltativo.|Nome della sessione di Eventi estesi. Per impostazione predefinita è XE_DEFAULT_ETW_SESSION.|  
|default_etw_session_logfile_path|Qualsiasi stringa contenente fino a 256 caratteri. Questo valore è facoltativo.|Percorso del file di log per la sessione di Eventi estesi. Per impostazione predefinita è %TEMP%\ XEEtw.etl.|  
|default_etw_session_logfile_size_mb|Qualsiasi valore intero senza segno. Questo valore è facoltativo.|Dimensioni del file di log, in megabyte (MB), per la sessione di Eventi estesi. Il valore predefinito è 20 MB.|  
|default_etw_session_buffer_size_kb|Qualsiasi valore intero senza segno. Questo valore è facoltativo.|Dimensioni del buffer in memoria, in kilobyte (MB), per la sessione di Eventi estesi. Il valore predefinito è 128 MB.|  
|tentativi|Qualsiasi valore intero senza segno.|Numero di tentativi di pubblicazione dell'evento al sottosistema ETW prima di eliminare l'evento. Il valore predefinito è 0.|  
  
 La configurazione di queste impostazioni è facoltativa. La destinazione ETW utilizza valori predefiniti per queste impostazioni.  
  
 La destinazione ETW è responsabile per:  
  
-   Creazione della sessione ETW predefinita.  
  
-   Registrazione di tutti i pacchetti di Eventi estesi con ETW. Ciò assicura che gli eventi non siano eliminati da ETW.  
  
-   Gestione dell'invio del flusso di eventi a ETW. La destinazione ETW crea un evento ETW con i dati di Eventi estesi e lo invia alla sessione ETW appropriata. Se l'evento è più grande della dimensione del buffer o se i dati non possono adattarsi a un evento ETW, ETW suddivide l'evento in frammenti.  
  
-   Conservazione dei pacchetti di Eventi estesi sempre abilitata.  
  
 I seguenti percorsi predefiniti dei file sono utilizzati da ETW:  
  
-   Il percorso del file di output per ETW è %TEMP%\XEEtw.etl.  
  
    > [!IMPORTANT]  
    >  Impossibile modificare il percorso del file dopo l'inizio della prima sessione.  
  
-   I file Managed Object Format (MOF) si trovano in *\<percorso di installazione>* \Microsoft SQL Server\Shared. Per altre informazioni, vedere [Managed Object Format (MOF)](https://go.microsoft.com/fwlink/?LinkId=92851) su MSDN.  
  
## <a name="adding-the-target-to-a-session"></a>Aggiunta della destinazione a una sessione  
 Per aggiungere la destinazione ETW a una sessione di Eventi estesi, è necessario includere l'istruzione seguente quando si crea o modifica una sessione eventi:  
  
```  
ADD TARGET package0.etw_classic_sync_target  
```  
  
 Per altre informazioni su un esempio completo che mostra come usare la destinazione ETW e come visualizzare i dati, vedere [Monitorare l'attività del sistema mediante gli eventi estesi](monitor-system-activity-using-extended-events.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Destinazioni degli eventi estesi di SQL Server](../../database-engine/sql-server-extended-events-targets.md)   
 [sys.dm_xe_session_targets &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-xe-session-targets-transact-sql)   
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql)   
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql)  
  
  
