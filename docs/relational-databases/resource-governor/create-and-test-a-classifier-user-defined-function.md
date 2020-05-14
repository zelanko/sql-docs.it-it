---
title: Creare e testare una funzione di classificazione definita dall'utente - Resource Governor
description: In questo argomento viene illustrato come creare e testare una funzione di classificazione definita dall'utente.
ms.custom: seo-dt-2019
ms.date: 07/11/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, classifier function create
- classifier function [SQL Server], test
- classifier function [SQL Server], create
- Resource Governor, classifier function test
ms.assetid: 7866b3c9-385b-40c6-aca5-32d3337032be
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: c11771790e91bb888df7e77749e6dc879081a46e
ms.sourcegitcommit: 553d5b21bb4bf27e232b3af5cbdb80c3dcf24546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/06/2020
ms.locfileid: "82849619"
---
# <a name="create-and-test-a-classifier-user-defined-function"></a>Creare e testare una funzione di classificazione definita dall'utente
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  In questo argomento viene illustrato come creare e testare una funzione di classificazione definita dall'utente. La procedura prevede l'esecuzione di istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] nell'editor di query di [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] .  
  
 Nell'esempio incluso nella procedura seguente vengono illustrate le diverse opzioni disponibili per la creazione di una funzione di classificazione definita dall'utente piuttosto complessa.  
  
 Nell'esempio:  
  
-   Vengono creati un pool di risorse (pProductionProcessing) e un gruppo del carico di lavoro (gProductionProcessing) per l'elaborazione in un ambiente di produzione durante un intervallo di tempo specificato.  
  
-   Vengono creati un pool di risorse (pOffHoursProcessing) e un gruppo del carico di lavoro (gOffHoursProcessing) per la gestione delle connessioni che non soddisfano i requisiti per l'elaborazione in un ambiente di produzione.  
  
-   Viene creata una tabella (TblClassificationTimeTable) nel database master per indicare date e ore di inizio e di fine da valutare rispetto a una data e un'ora di accesso. Tale tabella deve essere creata nel database master perché per le funzioni di classificazione Resource Governor utilizza l'associazione allo schema.  
  
    > [!NOTE]  
    >  Come procedura ottimale, è consigliabile non archiviare nel database master tabelle di grandi dimensioni aggiornate di frequente.  
  
 La funzione di classificazione prolunga i tempi di accesso. Una funzione eccessivamente complessa può provocare il timeout degli accessi o rallentare connessioni veloci.  
  
## <a name="to-create-the-classifier-user-defined-function"></a>Per creare la funzione di classificazione definita dall'utente  
  
1.  Creare e configurare i nuovi pool di risorse e i nuovi gruppi del carico di lavoro. Assegnare ogni gruppo del carico di lavoro al pool di risorse appropriato.  
  
    ```sql  
    --- Create a resource pool for production processing  
    --- and set limits.  
    USE master;  
    GO  
    CREATE RESOURCE POOL pProductionProcessing  
    WITH  
    (  
         MAX_CPU_PERCENT = 100,  
         MIN_CPU_PERCENT = 50  
    );  
    GO  
    
    --- Create a workload group for production processing  
    --- and configure the relative importance.  
    CREATE WORKLOAD GROUP gProductionProcessing  
    WITH  
    (  
         IMPORTANCE = MEDIUM  
    );  
    
    --- Assign the workload group to the production processing  
    --- resource pool.  
    USING pProductionProcessing  
    GO  
    
    --- Create a resource pool for off-hours processing  
    --- and set limits.  
    CREATE RESOURCE POOL pOffHoursProcessing  
    WITH  
    (  
         MAX_CPU_PERCENT = 50,  
         MIN_CPU_PERCENT = 0  
    );  
    GO  
    
    --- Create a workload group for off-hours processing  
    --- and configure the relative importance.  
    CREATE WORKLOAD GROUP gOffHoursProcessing  
    WITH  
    (  
         IMPORTANCE = LOW  
    )  
    --- Assign the workload group to the off-hours processing  
    --- resource pool.  
    USING pOffHoursProcessing;  
    GO  
    ```  
  
2.  Aggiornare la configurazione in memoria.  
  
    ```sql  
    ALTER RESOURCE GOVERNOR RECONFIGURE;  
    GO  
    ```  
  
3.  Creare una tabella e definire le ore di inizio e di fine per l'intervallo di tempo di elaborazione nell'ambiente di produzione.  
  
    ```sql  
    USE master;  
    GO  
    CREATE TABLE tblClassificationTimeTable  
    (  
         strGroupName     sysname          not null,  
         tStartTime       time              not null,  
         tEndTime         time              not null  
    );  
    GO  
    --- Add time values that the classifier will use to  
    --- determine the workload group for a session.  
    INSERT into tblClassificationTimeTable VALUES('gProductionProcessing', '6:35 AM', '6:15 PM');  
    GO  
    ```  
  
4.  Creare la funzione di classificazione in modo che utilizzi funzioni e valori di data e ora da valutare rispetto ai valori di data e ora specificati nella tabella di ricerca. Per informazioni sull'utilizzo di tabelle di ricerca in una funzione di classificazione, vedere "Procedure consigliate per l'utilizzo di tabelle di ricerca in una funzione di classificazione" in questo argomento.  
  
    > [!NOTE]  
    >  [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] include un set più ampio di tipi di dati e funzioni di data e ora. Per altre informazioni, vedere [Funzioni e tipi di dati di data e ora &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md).  
  
    ```sql  
    CREATE FUNCTION fnTimeClassifier()  
    RETURNS sysname  
    WITH SCHEMABINDING  
    AS  
    BEGIN  
    /* We recommend running the classifier function code under 
    snapshot isolation level OR using NOLOCK hint to avoid blocking on 
    lookup table. In this example, we are using NOLOCK hint. */
         DECLARE @strGroup sysname  
         DECLARE @loginTime time  
         SET @loginTime = CONVERT(time,GETDATE())  
         SELECT TOP 1 @strGroup = strGroupName  
              FROM dbo.tblClassificationTimeTable WITH(NOLOCK)
              WHERE tStartTime <= @loginTime and tEndTime >= @loginTime  
         IF(@strGroup is not null)  
         BEGIN  
              RETURN @strGroup  
         END  
    --- Use the default workload group if there is no match  
    --- on the lookup.  
         RETURN N'gOffHoursProcessing'  
    END;  
    GO  
    ```  
  
5.  Registrare la funzione di classificazione e aggiornare la configurazione in memoria.  
  
    ```sql  
    ALTER RESOURCE GOVERNOR with (CLASSIFIER_FUNCTION = dbo.fnTimeClassifier);  
    ALTER RESOURCE GOVERNOR RECONFIGURE;  
    GO  
    ```  
  
## <a name="to-verify-the-resource-pools-workload-groups-and-the-classifier-user-defined-function"></a>Per verificare i pool di risorse, i gruppi del carico di lavoro e la funzione di classificazione definita dall'utente  
  
1.  Ottenere la configurazione dei pool di risorse e dei gruppi del carico di lavoro utilizzando la query seguente.  
  
    ```sql  
    USE master;  
    SELECT * FROM sys.resource_governor_resource_pools;  
    SELECT * FROM sys.resource_governor_workload_groups;  
    GO  
    ```  
  
2.  Verificare che la funzione di classificazione sia presente e abilitata utilizzando le query seguenti.  
  
    ```sql  
    --- Get the classifier function Id and state (enabled).  
    SELECT * FROM sys.resource_governor_configuration;  
    GO  
    --- Get the classifer function name and the name of the schema  
    --- that it is bound to.  
    SELECT   
          object_schema_name(classifier_function_id) AS [schema_name],  
          object_name(classifier_function_id) AS [function_name]  
    FROM sys.dm_resource_governor_configuration;  
    ```  
  
3.  Ottenere i dati di runtime correnti per i pool di risorse e i gruppi del carico di lavoro utilizzando la query seguente.  
  
    ```sql  
    SELECT * FROM sys.dm_resource_governor_resource_pools;  
    SELECT * FROM sys.dm_resource_governor_workload_groups;  
    GO  
    ```  
  
4.  Individuare le sessioni incluse in ciascun gruppo utilizzando la query seguente.  
  
    ```sql  
    SELECT s.group_id, CAST(g.name as nvarchar(20)), s.session_id, s.login_time, 
        CAST(s.host_name as nvarchar(20)), CAST(s.program_name AS nvarchar(20))  
    FROM sys.dm_exec_sessions AS s  
    INNER JOIN sys.dm_resource_governor_workload_groups AS g  
        ON g.group_id = s.group_id  
    ORDER BY g.name;  
    GO  
    ```  
  
5.  Individuare le richieste incluse in ciascun gruppo utilizzando la query seguente.  
  
    ```sql  
    SELECT r.group_id, g.name, r.status, r.session_id, r.request_id, 
        r.start_time, r.command, r.sql_handle, t.text   
    FROM sys.dm_exec_requests AS r  
    INNER JOIN sys.dm_resource_governor_workload_groups AS g  
        ON g.group_id = r.group_id  
    CROSS APPLY sys.dm_exec_sql_text(r.sql_handle) AS t  
    ORDER BY g.name;  
    GO  
    ```  
  
6.  Individuare le richieste in esecuzione nella funzione di classificazione utilizzando la query seguente.  
  
    ```sql  
    SELECT s.group_id, g.name, s.session_id, s.login_time, s.host_name, s.program_name   
    FROM sys.dm_exec_sessions AS s  
    INNER JOIN sys.dm_resource_governor_workload_groups AS g  
        ON g.group_id = s.group_id  
           AND 'preconnect' = s.status  
    ORDER BY g.name;  
    GO  
  
    SELECT r.group_id, g.name, r.status, r.session_id, r.request_id, r.start_time, 
        r.command, r.sql_handle, t.text   
    FROM sys.dm_exec_requests AS r  
    INNER JOIN sys.dm_resource_governor_workload_groups AS g  
        ON g.group_id = r.group_id  
           AND 'preconnect' = r.status  
     CROSS APPLY sys.dm_exec_sql_text(r.sql_handle) AS t  
    ORDER BY g.name;  
    GO  
    ```  
  
## <a name="best-practices-for-using-lookup-tables-in-a-classifier-function"></a>Procedure consigliate per l'utilizzo di tabelle di ricerca in una funzione di classificazione  
  
1.  Non utilizzare una tabella di ricerca, a meno che non sia strettamente necessario. Se è necessario usare una tabella di ricerca, può essere hardcoded nella funzione stessa. È necessario tuttavia tenere presente la complessità e le modifiche dinamiche della funzione di classificazione.  
  
2.  Limitare l'I/O eseguito per le tabelle di ricerca.  
  
    1.  Usare `TOP 1` per restituire solo una riga.  
  
    2.  Ridurre al minimo il numero di righe della tabella.  
  
    3.  Includere tutte le righe della tabella in una sola pagina o in un numero ridotto di pagine.  
  
    4.  Verificare che le righe individuate utilizzando le operazioni Index Seek utilizzino il numero massimo consentito di colonne di ricerca.  
  
    5.  Se si prevede di utilizzare più tabelle con join, eseguire la denormalizzazione in una sola tabella.  
  
3.  Evitare blocchi nella tabella di ricerca.  
  
    1.  Usare l'hint `NOLOCK` per evitare i blocchi o usare `SET LOCK_TIMEOUT` nella funzione con un valore massimo di 1.000 millisecondi.  
  
    2.  Nel database master devono essere presenti una o più tabelle. Si tratta dell'unico database che verrà recuperato in caso di tentativo di connessione dei computer client.  
  
    3.  Fornire sempre un nome completo per la tabella con lo schema. Non è necessario specificare il nome del database, poiché deve essere utilizzato il database master.  
  
    4.  Nessun trigger nella tabella.  
  
    5.  In fase di aggiornamento dei contenuti della tabella, accertarsi di usare una transazione con livello di isolamento dello snapshot nella funzione di classificazione per evitare che il writer blocchi i lettori. Un altro metodo per evitare questo problema consiste nell'utilizzare l'hint `NOLOCK` .  
  
    6.  Se possibile, disabilitare la funzione di classificazione in fase di modifica dei contenuti della tabella.  
  
        > [!WARNING]  
        >  È consigliabile attenersi scrupolosamente a queste procedure consigliate. In caso non sia possibile seguire le procedure, contattare il supporto Microsoft per evitare in modo proattivo che si verifichino problemi in futuro.  
  
## <a name="see-also"></a>Vedere anche  
 [Resource Governor](../../relational-databases/resource-governor/resource-governor.md)   
 [Abilitare Resource Governor](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [Pool di risorse di Resource Governor](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [Gruppo di carico di lavoro di Resource Governor](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [Configurare Resource Governor utilizzando un modello](../../relational-databases/resource-governor/configure-resource-governor-using-a-template.md)   
 [Visualizzare proprietà di Resource Governor](../../relational-databases/resource-governor/view-resource-governor-properties.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
