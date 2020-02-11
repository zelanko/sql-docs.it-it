---
title: Monitorare i carichi
description: Monitorare i caricamenti attivi e recenti usando la console di amministrazione del sistema di piattaforma di analisi (APS) o le viste di sistema di data warehouse paralleli (PDW).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: b284fdcef506924c26e452196db6e9518faa1351
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "74400960"
---
# <a name="monitor-loads-into-parallel-data-warehouse"></a>Monitorare i caricamenti in parallelo data warehouse
Monitorare i carichi di [dwloader](dwloader.md) attivi e recenti usando la console di amministrazione del sistema di piattaforma di analisi (APS) o le [viste di sistema](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-reference-tsql-system-views/)di Parallel Data Warehouse (PDW). 
  
> [!TIP]  
> Alcuni caricamenti vengono avviati tramite istruzioni INSERT o business intelligence strumenti che utilizzano istruzioni SQL per eseguire il caricamento. 

<!-- MISSING LINKS
To monitor this type of load, see [Monitoring Active Queries](monitor-active-queries.md).  
-->
  
## <a name="prerequisites"></a>Prerequisites  
Indipendentemente dal metodo utilizzato per monitorare un carico, è necessario che l'account di accesso disponga dell'autorizzazione per accedere alle origini dati sottostanti. 

<!-- MISSING LINKS
For the permissions to grant, see "Use All of the Admin Console" in [Grant Permissions to Use the Admin Console](grant-permissions-admin-console.md). 

--> 
  
## <a name="monitoring-loads"></a>Monitoraggio di caricamenti  
Le sezioni seguenti descrivono come monitorare i carichi.  
  
### <a name="to-monitor-loads-by-using-the-admin-console"></a>Per monitorare i carichi tramite la console di amministrazione  
  
1.  Accedere alla console di amministrazione di. <!-- MISSING LINKS See [Monitor the Appliance by Using the Admin Console;](monitor-admin-console.md) for instructions. --> 
  
2.  Nel menu superiore fare clic su **carica**. Verrà visualizzata una tabella ordinabile che Mostra tutti i caricamenti recenti e attivi più informazioni aggiuntive, ad esempio se il carico è stato completato o è ancora attivo. Fare clic sulle intestazioni di colonna per ordinare le righe.  
  
3.  Per visualizzare ulteriori dettagli relativi a un carico specifico, fare clic sull' **ID** di carico nella colonna a sinistra. Nella visualizzazione dettagliata è possibile visualizzare lo stato di avanzamento di ogni passaggio del carico.  
  
Per informazioni sui metadati relativi al carico visualizzato nella console di amministrazione, vedere le viste di sistema seguenti:  
  
-   [sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)  
  
-   [sys.pdw_loader_run_stages](https://msdn.microsoft.com/library/mt203879.aspx)  
  
-   [sys.pdw_loader_backup_runs](../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)  
  
-   [sys.pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)  
  
### <a name="to-monitor-loads-by-using-system-views"></a>Per monitorare i caricamenti utilizzando viste di sistema  
Per monitorare i caricamenti attivi e recenti usando le visualizzazioni SQL Server PDW, seguire questa procedura. Per ogni vista di sistema utilizzata, vedere la documentazione relativa a tale vista per informazioni sulle colonne e i valori potenziali restituiti dalla vista.  
  
1.  Trovare la `request_id` per il caricamento nella vista [sys. dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md) trovando la riga di comando del caricatore nella `command` colonna per questa visualizzazione.  
  
    Ad esempio, il comando seguente restituisce il testo del comando e lo stato corrente, `request_id`oltre a.  
  
    ```sql  
    SELECT request_id, status, command FROM sys.dm_pdw_exec_requests;  
    ```  
  
2.  Utilizzare `request_id` per recuperare informazioni aggiuntive per il caricamento utilizzando le visualizzazioni [sys. pdw_loader_run_stages](../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md) e [sys. pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md) . Ad esempio, la query seguente restituisce le `run_id` informazioni e per le ore di inizio, fine e durata del carico, più eventuali errori e informazioni sul numero di righe elaborate:  
  
    ```sql  
    SELECT lbr.run_id,   
    er.submit_time, er.end_time, er.total_elapsed_time, er.error_id, lbr.rows_processed, lbr.rows_rejected, lbr.rows_inserted   
    FROM sys.dm_pdw_exec_requests er   
    LEFT OUTER JOIN   
    sys.pdw_loader_backup_runs lbr   
    ON (er.request_id=lbr.requst_id)   
    WHERE er.request_id='12738';  
    ```  
  
<!-- MISSING LINKS

## See Also  
[Common metadata query examples](metadata-query-examples.md)
-->  
  
