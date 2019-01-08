---
title: Monitorare le query attive - Parallel Data Warehouse | Microsoft Docs
description: Usare le viste di sistema della Console di amministrazione e Parallel Data Warehouse per monitorare le query attive nel sistema di piattaforma Analitica.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: d2b1ee84b2ae738d7790e1238176331a221ac473
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52409868"
---
# <a name="monitoring-active-queries---parallel-data-warehouse"></a>Monitoraggio delle query attive - Parallel Data Warehouse
Questo articolo illustra come usare la Console di amministrazione e le viste di sistema di SQL Server PDW per monitorare le query attive. Visualizzare [monitorare l'Appliance usando la Console di amministrazione](monitor-the-appliance-by-using-the-admin-console.md) e [viste di sistema](tsql-system-views.md) per informazioni su questi strumenti.  
  
## <a name="prerequisites"></a>Prerequisiti  
Indipendentemente dal metodo usato per monitorare le query attive, l'accesso deve disporre delle autorizzazioni descritte in "Utilizzo tutti della Console di amministrazione" nella [concedere autorizzazioni per usare la Console di amministrazione](grant-permissions.md#grant-permissions-to-use-the-admin-console).  
  
## <a name="PermsAdminConsole"></a>Monitoraggio query attive  
Sia la Console di amministrazione e le viste di sistema di SQL Server PDW sono utilizzabile per monitorare le query attive. Seguire le istruzioni seguenti.  
  
### <a name="to-monitor-active-queries-by-using-the-admin-console"></a>Per monitorare le query attive tramite la Console di amministrazione  
  
1.  Accedere alla Console di amministrazione. Visualizzare [monitorare l'Appliance usando la Console di amministrazione](monitor-the-appliance-by-using-the-admin-console.md) per le istruzioni.  
  
2.  Nel menu in alto fare clic su **query**. Si noterà una tabella con le informazioni di base sulle query più recente nell'appliance, tra cui l'account di accesso che ha inviato la query, l'ora di inizio e fine per la query e lo stato corrente della query.  
  
3.  Per visualizzare il comando di query, posizionare il puntatore del mouse sull'ID di query nella colonna a sinistra per quella riga.  
  
    Per visualizzare che informazioni più dettagliate per una determinata query, fare clic su ID di query. Verranno visualizzate informazioni tra cui la query completa e il piano di query, con informazioni sullo stato per ogni passaggio nell'esecuzione della query. Se sono stati restituiti gli eventuali errori, è anche possibile visualizzare informazioni dettagliate sugli errori. <!-- MISSING LINKS See [Understanding Query Plans &#40;SQL Server PDW&#41;](../sqlpdw/understanding-query-plans-sql-server-pdw.md) for information on how to interpret the query plan information available in the Admin Console.  -->
  
### <a name="to-monitor-active-queries-by-using-the-system-views"></a>Monitorare le query attive tramite le viste di sistema  
La vista di sistema principale utilizzata per monitorare le query viene [DM pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md). Utilizzare questa vista di sistema per trovare il `request_id` per una query attiva o recente, basata su testo della query.  
  
Ad esempio, la query seguente trova la `request_id` corrente `status` per qualsiasi query che seleziona tutte le colonne dal `memberAddresses` tabella.  
  
```sql  
SELECT request_id, command, status   
FROM sys.dm_pdw_exec_requests   
WHERE command   
LIKE '%SELECT * FROM db1..memberAddresses%';  
```  
  
Dopo il `request_id` è stata identificata per una query, usare le altre informazioni nel `dm_pdw_exec_requests` per scoprire l'elaborazione della query di tabella oppure utilizzare [DM pdw_request_steps](../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md) per visualizzare lo stato delle singole query passaggi per l'esecuzione della query.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
