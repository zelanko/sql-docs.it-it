---
title: Monitorare i caricamenti per Parallel Data Warehouse | Microsoft Docs
description: Monitorare carichi attive e recenti usando la Console di amministrazione di Analitica Platform System (APS) o le viste di sistema di Data Warehouse (PDW) Parallel".
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 1eadf20e036c6c76cd3bece7c404fde2af4a7d70
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67960601"
---
# <a name="monitor-loads-into-parallel-data-warehouse"></a>Monitorare i caricamenti in Parallel Data Warehouse
Monitoraggio attiva e recente [dwloader](dwloader.md) carica utilizzando la Console di amministrazione di Analitica piattaforma di strumenti analitici o Parallel Data Warehouse (PDW) [viste di sistema](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-reference-tsql-system-views/). 
  
> [!TIP]  
> Alcuni carichi vengono avviate usando le istruzioni INSERT o strumenti di business intelligence che usano istruzioni SQL per eseguire il caricamento. 

<!-- MISSING LINKS
To monitor this type of load, see [Monitoring Active Queries](monitor-active-queries.md).  
-->
  
## <a name="prerequisites"></a>Prerequisiti  
Indipendentemente dal metodo usato per monitorare il carico, l'accesso deve disporre dell'autorizzazione per accedere alle origini dati sottostanti. 

<!-- MISSING LINKS
For the permissions to grant, see "Use All of the Admin Console" in [Grant Permissions to Use the Admin Console](grant-permissions-admin-console.md). 

--> 
  
## <a name="monitoring-loads"></a>Caricamenti di monitoraggio  
Le sezioni seguenti descrivono come monitorare i caricamenti.  
  
### <a name="to-monitor-loads-by-using-the-admin-console"></a>Per monitorare i caricamenti con la Console di amministrazione  
  
1.  Accedere alla Console di amministrazione. <!-- MISSING LINKS See [Monitor the Appliance by Using the Admin Console;](monitor-admin-console.md) for instructions. --> 
  
2.  Nel menu in alto fare clic su **caricamenti**. Si noterà una tabella ordinabile che mostra tutte le recenti e di caricamenti attivi oltre a informazioni aggiuntive, ad esempio se il carico è stata completata o è ancora attivo. Scegliere le intestazioni di colonna per ordinare le righe.  
  
3.  Per visualizzare dettagli aggiuntivi per un carico specifico, scegliere il carico **ID** nella colonna sinistra. Nella visualizzazione dettagliata, è possibile visualizzare lo stato di avanzamento a ogni passo del carico.  
  
Visualizzare le viste di sistema per informazioni sui metadati relative al carico che viene visualizzato nella Console di amministrazione:  
  
-   [sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)  
  
-   [sys.pdw_loader_run_stages](https://msdn.microsoft.com/library/mt203879.aspx)  
  
-   [sys.pdw_loader_backup_runs](../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)  
  
-   [sys.pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)  
  
### <a name="to-monitor-loads-by-using-system-views"></a>Per monitorare i caricamenti con viste di sistema  
Per monitorare i caricamenti attivi e recenti utilizzando le viste di SQL Server PDW, attenersi alla procedura seguente. Per ogni vista di sistema utilizzata, vedere la documentazione per la visualizzazione per informazioni sui potenziali valori restituiti dalla vista e le colonne.  
  
1.  Trovare il `request_id` per il caricamento nel [DM pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md) visualizzazione mediante la riga di comando di caricatore in ricerca il `command` colonna per la visualizzazione.  
  
    Ad esempio, il comando seguente restituisce il testo del comando e lo stato corrente, più il `request_id`.  
  
    ```sql  
    SELECT request_id, status, command FROM sys.dm_pdw_exec_requests;  
    ```  
  
2.  Usare la `request_id` per recuperare informazioni aggiuntive per il caricamento usando la [sys.pdw_loader_run_stages](../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md) , e [sys.pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md) viste. Ad esempio, la query seguente restituisce il `run_id` e informazioni sull'inizio, fine e tempi di durata del carico, più eventuali errori e informazioni sul numero di righe elaborate:  
  
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
  
