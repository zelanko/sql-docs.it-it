---
title: Monitorare le query attive
description: Usare la console di amministrazione e le viste di sistema data warehouse parallele per monitorare le query attive nel sistema della piattaforma di analisi.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 9157db745b999711966f0019747ba1d61823569e
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400918"
---
# <a name="monitoring-active-queries---parallel-data-warehouse"></a>Monitoraggio delle query attive-data warehouse parallele
Questo articolo illustra come usare la console di amministrazione e le viste di sistema SQL Server PDW per monitorare le query attive. Per informazioni su questi strumenti, vedere [monitorare l'appliance usando la console di amministrazione e le](monitor-the-appliance-by-using-the-admin-console.md) [visualizzazioni di sistema](tsql-system-views.md) .  
  
## <a name="prerequisites"></a>Prerequisiti  
Indipendentemente dal metodo utilizzato per monitorare le query attive, l'account di accesso deve disporre delle autorizzazioni descritte in "utilizzare tutta la console di amministrazione" in [concedere le autorizzazioni per l'utilizzo della console di amministrazione](grant-permissions.md#grant-permissions-to-use-the-admin-console).  
  
## <a name="monitor-active-queries"></a><a name="PermsAdminConsole"></a>Monitorare le query attive  
Per monitorare le query attive, è possibile usare sia la console di amministrazione che le viste di sistema SQL Server PDW. Seguire le istruzioni riportate di seguito.  
  
### <a name="to-monitor-active-queries-by-using-the-admin-console"></a>Per monitorare le query attive usando la console di amministrazione  
  
1.  Accedere alla console di amministrazione di. Per istruzioni, vedere [monitorare l'appliance usando la console di amministrazione](monitor-the-appliance-by-using-the-admin-console.md) .  
  
2.  Nel menu in alto fare clic su **query**. Viene visualizzata una tabella con le informazioni di base sulle query più recenti sul dispositivo, tra cui l'account di accesso che ha inviato la query, le ore di inizio e di fine per la query e lo stato corrente della query.  
  
3.  Per visualizzare il comando di query, posizionare il puntatore del mouse sull'ID di query nella colonna sinistra della riga.  
  
    Per visualizzare informazioni più dettagliate per una determinata query, fare clic sull'ID della query. Vengono visualizzate informazioni che includono la query completa e il piano di query, con informazioni sullo stato per ogni passaggio nell'esecuzione della query. Se sono stati restituiti errori, è anche possibile visualizzare informazioni dettagliate sugli errori. <!-- MISSING LINKS See [Understanding Query Plans &#40;SQL Server PDW&#41;](../sqlpdw/understanding-query-plans-sql-server-pdw.md) for information on how to interpret the query plan information available in the Admin Console.  -->
  
### <a name="to-monitor-active-queries-by-using-the-system-views"></a>Per monitorare le query attive utilizzando le viste di sistema  
La vista di sistema primaria utilizzata per il monitoraggio delle query è [sys. dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md). Utilizzare questa vista di sistema per trovare `request_id` per una query attiva o recente, in base al testo della query.  
  
Ad esempio, la query seguente consente di trovare `request_id` e l'oggetto corrente `status` per qualsiasi query che seleziona tutte le colonne della `memberAddresses` tabella.  
  
```sql  
SELECT request_id, command, status   
FROM sys.dm_pdw_exec_requests   
WHERE command   
LIKE '%SELECT * FROM db1..memberAddresses%';  
```  
  
Dopo che `request_id` è stato identificato per una query, utilizzare le altre informazioni della `dm_pdw_exec_requests` tabella per individuare l'elaborazione della query oppure utilizzare [sys. dm_pdw_request_steps](../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md) per visualizzare lo stato dei singoli passaggi di query per l'esecuzione della query.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
