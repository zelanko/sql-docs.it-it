---
title: Creare una sessione eventi estesi tramite l'editor di query | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- create extended events session
- extended events [SQL Server], create session
ms.assetid: cba0e02b-b201-4863-bf1b-9164e68e5fa8
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4a541c86029be9a438492a851c0eb16d18120f75
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66065025"
---
# <a name="create-an-extended-events-session-using-query-editor"></a>Creare una sessione Eventi estesi tramite l'editor di query
  È possibile creare una sessione Eventi estesi tramite l'editor di query o è possibile creare una sessione in Esplora oggetti. In Esplora oggetti, gli eventi estesi forniscono due interfacce utente che è possibile usare per creare, modificare e visualizzare i dati della sessione eventi, una procedura guidata che guida l'utente durante il processo di creazione della sessione eventi e una nuova interfaccia utente della sessione che fornisce opzioni di configurazione più avanzate. È possibile creare sessioni di eventi estesi per la diagnosi della traccia di SQL Server, che consente di risolvere problemi come i seguenti:  
  
-   Trovare le query con il costo più elevato  
  
-   Trovare le cause principali di contese di latch  
  
-   Trovare una query tramite cui vengono bloccate altre query  
  
-   Risolvere i problemi relativi all'utilizzo eccessivo della CPU causato dalla ricompilazione di query  
  
-   Risolvere problemi relativi ai deadlock  
  
 Per informazioni su come creare una sessione eventi estesi usando la Creazione guidata nuova sessione, vedere [Creare una sessione Eventi estesi usando la procedura guidata &#40;Esplora oggetti&#41;](../ssms/object/object-explorer.md). Per informazioni su come creare una sessione eventi estesi usando l'interfaccia utente Nuova sessione, vedere [Creare una sessione Eventi estesi usando la finestra di dialogo Nuova sessione](../../2014/database-engine/create-an-extended-events-session-using-the-new-session-dialog.md).  
  
##  <a name="BeforeYouBegin"></a> Autorizzazioni  
 Per creare una sessione Eventi estesi, è necessario disporre dell'autorizzazione ALTER ANY EVENT SESSION.  
  
## <a name="creating-an-extended-events-session-using-query-editor"></a>Creazione di una sessione Eventi estesi tramite l'editor di query  
  
#### <a name="to-create-an-extended-events-session"></a>Per creare una sessione Eventi estesi  
  
1.  Nella procedura seguente viene illustrato come creare una sessione Eventi estesi utilizzando l'editor di query in [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
     Determinare gli eventi che si desidera utilizzare nella sessione. Per visualizzare tutti gli eventi disponibili, insieme alla parola chiave e al canale, utilizzare la query seguente:  
  
    > [!NOTE]  
    >  Per informazioni sulle parole chiave e i canali, vedere [Pacchetti degli eventi estesi di SQL Server](../relational-databases/extended-events/sql-server-extended-events-packages.md).  
  
    ```  
    SELECT p.name, c.event, k.keyword, c.channel, c.description FROM  
       (  
       SELECT event_package = o.package_guid, o.description,   
       event=c.object_name, channel = v.map_value  
       FROM sys.dm_xe_objects o  
       LEFT JOIN sys.dm_xe_object_columns c ON o.name = c.object_name  
       INNER JOIN sys.dm_xe_map_values v ON c.type_name = v.name   
       AND c.column_value = cast(v.map_key AS nvarchar)  
       WHERE object_type = 'event' AND (c.name = 'CHANNEL' or c.name IS NULL)  
       ) c LEFT JOIN   
       (  
       SELECT event_package = c.object_package_guid, event = c.object_name,   
       keyword = v.map_value  
       FROM sys.dm_xe_object_columns c INNER JOIN sys.dm_xe_map_values v   
       ON c.type_name = v.name AND c.column_value = v.map_key   
       AND c.type_package_guid = v.object_package_guid  
       INNER JOIN sys.dm_xe_objects o ON o.name = c.object_name   
       AND o.package_guid = c.object_package_guid  
       WHERE object_type = 'event' AND c.name = 'KEYWORD'   
       ) k  
       ON  
       k.event_package = c.event_package AND (k.event=c.event or k.event IS NULL)  
       INNER JOIN sys.dm_xe_packages p ON p.guid = c.event_package  
    ORDER BY keyword desc, channel, event  
    ```  
  
2.  In una nuova finestra di query aggiungere le istruzioni seguenti per creare una sessione eventi, sostituendo *session_name* con il nome che si vuole usare per la sessione:  
  
    > [!IMPORTANT]  
    >  Nei passaggi da 2 a 6 di questa procedura viene descritta ogni sezione della definizione della sessione eventi. Tutte le istruzioni vengono aggiunte a una singola finestra di query prima dell'esecuzione. Per un esempio completo, vedere la sezione Esempio di questo argomento.  
  
    ```  
    CREATE EVENT SESSION session_name   
    ON SERVER  
    ```  
  
3.  Aggiungere gli eventi da monitorare, nel formato *nome_pacchetto*.*nome_evento*. Per ogni evento, aggiungere una riga simile alla seguente:  
  
    ```  
    ADD EVENT package_name.event_name  
    ```  
  
     Ad esempio:  
  
    ```  
    ADD EVENT sqlserver.file_read_completed,  
    ADD EVENT sqlserver.file_write_completed  
    ```  
  
4.  (Facoltativo) Dopo avere aggiunto un evento, è possibile aggiungere azioni da eseguire. È inoltre possibile aggiungere predicati. I predicati vengono utilizzati per stabilire i criteri relativi a quando le informazioni sull'evento devono essere utilizzate dalla destinazione. Le azioni vengono aggiunte utilizzando una clausola ACTION, mentre i predicati vengono aggiunti utilizzando una clausola WHERE. Ad esempio, per aggiungere un'azione e un predicato in cui viene acquisito il testo [!INCLUDE[tsql](../includes/tsql-md.md)] per l'evento sqlserver.file_read_completed, quando l'ID del file corrisponde a 1, includere l'istruzione seguente:  
  
    ```  
    ADD EVENT sqlserver.file_read_completed  
       (ACTION (sqlserver.sql_text)  
       WHERE file_id = 1),  
    ```  
  
    -   Per visualizzare le azioni disponibili, utilizzare la query seguente:  
  
        ```  
        SELECT p.name AS 'package_name', xo.name AS 'action_name', xo.description, xo.object_type  
        FROM sys.dm_xe_objects AS xo  
        JOIN sys.dm_xe_packages AS p  
           ON xo.package_guid = p.guid  
        WHERE xo.object_type = 'action'  
        AND (xo.capabilities & 1 = 0   
        OR xo.capabilities IS NULL)  
        ORDER BY p.name, xo.name  
        ```  
  
    -   Per visualizzare i predicati disponibili per un evento, usare la query seguente, sostituendo *event_name* con il nome dell'evento per cui si vuole aggiungere un predicato:  
  
        ```  
        SELECT *  
        FROM sys.dm_xe_object_columns  
        WHERE object_name = 'event_name'  
        AND column_type = 'data'  
        ```  
  
         Ad esempio:  
  
        ```  
        SELECT *   
        FROM sys.dm_xe_object_columns   
        WHERE object_name = 'file_read_completed'  
        AND column_type = 'data'  
        ```  
  
         Tenere presente che è anche possibile aggiungere origini di predicati globali. Un'origine di predicato globale può essere utilizzata in qualsiasi espressione di predicato. Per visualizzare le origini di predicati globali disponibili, utilizzare la query seguente:  
  
        ```  
        SELECT p.name AS package_name, xo.name AS predicate_name  
           , xo.description, xo.object_type  
        FROM sys.dm_xe_objects AS xo  
        JOIN sys.dm_xe_packages AS p  
           ON xo.package_guid = p.guid  
        WHERE xo.object_type = 'pred_source'  
        ORDER BY p.name, xo.name  
        ```  
  
         È ad esempio possibile utilizzare l'espressione di predicato seguente per specificare che devono essere raccolti dati per un evento solo le prime cinque volte che l'evento si verifica.  
  
        ```  
        WHERE package0.counter <= 5  
        ```  
  
5.  Aggiungere la destinazione desiderata, dove verranno elaborati e utilizzati i dati degli eventi. Utilizzare il seguente formato:  
  
    ```  
    ADD TARGET package_name.target_name  
    ```  
  
     Nell'esempio seguente viene aggiunta la destinazione file asincrona:  
  
    ```  
    ADD TARGET package0.asynchronous_file_target  
       (SET filename = 'c:\temp\xelog.xel', metadatafile = 'c:\temp\xelog.xem')  
    ```  
  
     Per visualizzare l'elenco di destinazioni disponibili, utilizzare la query seguente:  
  
    ```  
    SELECT p.name AS 'package_name', xo.name AS 'target_name'  
       , xo.description, xo.object_type   
    FROM sys.dm_xe_objects AS xo  
    JOIN sys.dm_xe_packages AS p  
       ON xo.package_guid = p.guid  
    WHERE xo.object_type = 'target'  
    AND (xo.capabilities & 1 = 0  
    OR xo.capabilities IS NULL)  
    ORDER BY p.name, xo.name  
    ```  
  
    > [!NOTE]  
    >  Per informazioni sui diversi tipi di destinazione, vedere [Destinazioni degli eventi estesi di SQL Server](../../2014/database-engine/sql-server-extended-events-targets.md).  
  
6.  Rivedere e aggiungere eventuali opzioni di configurazione aggiuntive. È ad esempio possibile configurare opzioni come la modalità di memorizzazione degli eventi, il tempo di permanenza degli eventi nel buffer in memoria o l'avvio automatico della sessione eventi all'avvio di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Le opzioni sono descritte nell'argomento [ALTER EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-event-session-transact-sql). Tenere presente che, se queste opzioni non vengono specificate, vengono assegnati valori predefiniti.  
  
7.  Avviare la sessione.  
  
    > [!NOTE]  
    >  Per altre informazioni su come visualizzare i risultati della sessione, vedere l'argomento corrispondente per il tipo di destinazione usato nel nodo [Destinazioni degli eventi estesi di SQL Server](../../2014/database-engine/sql-server-extended-events-targets.md) della documentazione online.  
  
 Nell'esempio seguente viene creata una sessione Eventi estesi denominata IOActivity che consente di acquisire le informazioni seguenti:  
  
-   Dati degli eventi per le letture di file completate, incluso il testo [!INCLUDE[tsql](../includes/tsql-md.md)] associato per le letture di file in cui l'ID del file corrisponde a 1.  
  
-   Dati degli eventi per le scritture di file completate.  
  
-   Dati degli eventi relativi a quando i dati vengono scritti dalla cache del log al file di log fisico.  
  
 L'output viene inviato dalla sessione a una destinazione file.  
  
```  
CREATE EVENT SESSION IOActivity  
ON SERVER  
  
ADD EVENT sqlserver.file_read_completed  
   (  
   ACTION (sqlserver.sql_text)  
   WHERE file_id = 1),  
ADD EVENT sqlserver.file_write_completed,  
ADD EVENT sqlserver.databases_log_flush  
  
ADD TARGET package0.asynchronous_file_target   
   (SET filename = 'c:\temp\xelog.xel', metadatafile = 'c:\temp\xelog.xem')  
```  
  
## <a name="see-also"></a>Vedere anche  
 [CREATE EVENT SESSION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-event-session-transact-sql)   
 [Destinazioni degli eventi estesi di SQL Server](../../2014/database-engine/sql-server-extended-events-targets.md)   
 [Pacchetti degli eventi estesi di SQL Server](../relational-databases/extended-events/sql-server-extended-events-packages.md)  
  
  
