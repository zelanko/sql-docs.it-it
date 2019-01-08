---
title: Le sessioni utente nel sistema di piattaforma Analitica | Microsoft Docs"
description: Sessioni utente del sistema di piattaforma Analitica Parallel Data warehouse.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 33bf052e27640ee08784927351579378bffbec2b
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52419222"
---
# <a name="user-sessions-in-analytics-platform-system"></a>Sessioni utente nel sistema di piattaforma Analitica
Un account di accesso con le autorizzazioni appropriate possono gestire le sessioni di tutti gli account di accesso in un'appliance di SQL Server PDW, inclusa l'esecuzione di queste azioni:  
  
-   Visualizzare le sessioni correnti nell'appliance, tra cui sessioni sia attive e inattive.  
  
-   Visualizzare le query attive e recenti per una sessione.  
  
-   Terminare le sessioni attive.  
  
È possibile eseguire queste azioni usando il [monitorare l'Appliance usando la Console di amministrazione](monitor-the-appliance-by-using-the-admin-console.md) oppure [viste di sistema](tsql-system-views.md) tramite i comandi SQL, come illustrato di seguito.  
  
Le autorizzazioni necessarie per gestire le sessioni tramite uno dei due metodi sono gli stessi e sono descritte nel [concedere autorizzazioni per gestire gli account di accesso, utenti e ruoli del Database](grant-permissions.md#grant-permissions-to-manage-logins-users-and-database-roles).  
  
## <a name="manage-sessions-by-using-the-admin-console"></a>Gestire le sessioni tramite la Console di amministrazione  
  
### <a name="to-view-current-sessions-by-using-the-admin-console"></a>Per visualizzare le sessioni correnti tramite la Console di amministrazione  
  
1.  Nel menu in alto fare clic su **sessioni**.  
  
2.  L'elenco risulta Mostra tutte le sessioni recenti. Per visualizzare solo le sessioni 'Active' o "Tempo di inattività", scegliere il **stato** intestazione di colonna per ordinare i risultati in base allo stato.  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-the-admin-console"></a>Per visualizzare le query attive e recenti per una sessione tramite la Console di amministrazione  
  
1.  Nel menu in alto fare clic su **sessioni**.  
  
2.  Nell'elenco dei risultati, fare clic sull'ID sessione della sessione desiderata.  
  
3.  L'elenco di query risultante mostra la query recenti per la sessione. Per informazioni sulla visualizzazione dei dettagli della query, vedere [monitoraggio delle query attive](monitoring-active-queries.md).  
  
### <a name="to-end-sessions-by-using-the-admin-console"></a>Per terminare le sessioni tramite la Console di amministrazione  
  
1.  Nel menu in alto fare clic su **sessioni**.  
  
2.  Trovare l'ID di sessione per la sessione da annullare.  
  
3.  Fare clic su rossa **X** a sinistra dell'ID di sessione per terminare la sessione. Solo le sessioni con stato 'Attivo' o 'Inattive' avranno una linea rossa **X**; solo tali sessioni possono essere terminate.  
  
## <a name="manage-sessions-by-using-system-views-and-sql-commands"></a>Gestire le sessioni utilizzando viste di sistema e i comandi SQL  
  
### <a name="to-view-current-sessions-by-using-system-views"></a>Per visualizzare le sessioni correnti tramite viste di sistema  
Uso [DM pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) per generare un elenco delle sessioni correnti.  
  
Questo esempio restituisce il session_id login_name e stato per tutte le sessioni con stato 'Active' o 'Idle'.  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions WHERE status='Active' OR status='Idle';  
```  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-system-views"></a>Per visualizzare le query attive e recenti per una sessione utilizzando viste di sistema  
Consente di visualizzare le query attive e completate di recente associate a una sessione, il [DM pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) e [DM pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md) viste. Questa query restituisce un elenco di tutte le sessioni attive o inattive, oltre a eventuali query attive o recenti associata a ogni ID di sessione.  
  
```sql  
SELECT es.session_id, es.login_name, es.status AS sessionStatus,   
er.request_id, er.status AS requestStatus, er.command   
FROM sys.dm_pdw_exec_sessions es   
LEFT OUTER JOIN sys.dm_pdw_exec_requests er   
ON (es.session_id=er.session_id)   
WHERE (es.status='Active' OR es.status='Idle') AND   
(er.status!= 'Completed' AND er.status!= 'Failed' AND er.status!= 'Cancelled');  
```  
  
### <a name="to-end-sessions-by-using-sql-commands"></a>Per terminare le sessioni tramite i comandi SQL  
Usare la [KILL](../t-sql/language-elements/kill-transact-sql.md) comando per terminare una sessione corrente. È necessario l'ID di sessione per il processo da terminare, che può essere ottenuto usando il [DM pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) visualizzazione.  
  
In questo esempio, selezionare il login_name session_id e valori di stato per individuare una sessione in base al nome di account di accesso.  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions;  
```  
  
È possibile terminare le sessioni con stato 'Attivo' o 'Tempo di inattività' usando il comando KILL.  
  
```sql  
KILL 'SID137';  
```  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
