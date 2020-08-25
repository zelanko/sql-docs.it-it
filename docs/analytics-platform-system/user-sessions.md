---
title: Sessioni utente
description: Sessioni utente nel data warehouse parallelo del sistema della piattaforma Analytics.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: a0e5b338cc616be214ef39527551ee4a6ffd8f56
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/25/2020
ms.locfileid: "74399402"
---
# <a name="user-sessions-in-analytics-platform-system"></a>Sessioni utente nel sistema della piattaforma Analytics
Un account di accesso con le autorizzazioni appropriate può gestire le sessioni di tutti gli account di accesso in un dispositivo SQL Server PDW, inclusa l'esecuzione di queste azioni:  
  
-   Visualizzare le sessioni correnti nell'appliance, incluse le sessioni attive e inattive.  
  
-   Visualizzare le query attive e recenti per una sessione.  
  
-   Terminare le sessioni attive.  
  
Queste azioni possono essere eseguite usando il monitoraggio dell' [Appliance usando la console di amministrazione](monitor-the-appliance-by-using-the-admin-console.md) o le [visualizzazioni di sistema](tsql-system-views.md) tramite i comandi SQL, come illustrato di seguito.  
  
Le autorizzazioni necessarie per gestire le sessioni mediante uno dei due metodi sono le stesse e sono descritte in [concedere le autorizzazioni per la gestione di account di accesso, utenti e ruoli del database](grant-permissions.md#grant-permissions-to-manage-logins-users-and-database-roles).  
  
## <a name="manage-sessions-by-using-the-admin-console"></a>Gestire le sessioni tramite la console di amministrazione  
  
### <a name="to-view-current-sessions-by-using-the-admin-console"></a>Per visualizzare le sessioni correnti tramite la console di amministrazione  
  
1.  Nel menu in alto fare clic su **sessioni**.  
  
2.  Nell'elenco risultante vengono visualizzate tutte le sessioni recenti. Per visualizzare solo le sessioni ' attive ' o ' inattive ', fare clic sull'intestazione della colonna **stato** per ordinare i risultati in base allo stato.  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-the-admin-console"></a>Per visualizzare le query attive e recenti per una sessione usando la console di amministrazione  
  
1.  Nel menu in alto fare clic su **sessioni**.  
  
2.  Nell'elenco dei risultati fare clic sull'ID di sessione della sessione desiderata.  
  
3.  L'elenco query risultante Mostra le query recenti per la sessione. Per informazioni sulla visualizzazione dei dettagli della query, vedere [monitoraggio delle query attive](monitoring-active-queries.md).  
  
### <a name="to-end-sessions-by-using-the-admin-console"></a>Per terminare le sessioni tramite la console di amministrazione  
  
1.  Nel menu in alto fare clic su **sessioni**.  
  
2.  Trovare l'ID sessione per la sessione da annullare.  
  
3.  Fare clic sulla **X** rossa a sinistra dell'ID sessione per terminare la sessione. Solo le sessioni con stato "attivo" o "inattivo" avranno una **X**rossa; è possibile terminare solo queste sessioni.  
  
## <a name="manage-sessions-by-using-system-views-and-sql-commands"></a>Gestire le sessioni usando le viste di sistema e i comandi SQL  
  
### <a name="to-view-current-sessions-by-using-system-views"></a>Per visualizzare le sessioni correnti utilizzando viste di sistema  
Utilizzare [sys. dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) per generare un elenco di sessioni correnti.  
  
In questo esempio vengono restituiti session_id, login_name e lo stato di tutte le sessioni con lo stato ' attivo ' o ' inattivo '.  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions WHERE status='Active' OR status='Idle';  
```  
  
### <a name="to-view-active-and-recent-queries-for-a-session-by-using-system-views"></a>Per visualizzare le query attive e recenti per una sessione utilizzando viste di sistema  
Per visualizzare le query attive e completate di recente associate a una sessione, è possibile usare le viste [sys. dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) e [sys. dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md) . Questa query restituisce un elenco di tutte le sessioni attive o inattive, oltre a tutte le query attive o recenti associate a ogni ID sessione.  
  
```sql  
SELECT es.session_id, es.login_name, es.status AS sessionStatus,   
er.request_id, er.status AS requestStatus, er.command   
FROM sys.dm_pdw_exec_sessions es   
LEFT OUTER JOIN sys.dm_pdw_exec_requests er   
ON (es.session_id=er.session_id)   
WHERE (es.status='Active' OR es.status='Idle') AND   
(er.status!= 'Completed' AND er.status!= 'Failed' AND er.status!= 'Cancelled');  
```  
  
### <a name="to-end-sessions-by-using-sql-commands"></a>Per terminare le sessioni usando i comandi SQL  
Usare il comando [Kill](../t-sql/language-elements/kill-transact-sql.md) per terminare una sessione corrente. È necessario l'ID sessione per il processo da terminare, che può essere ottenuto usando la vista [sys. dm_pdw_exec_sessions](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-sessions-transact-sql.md) .  
  
In questo esempio, selezionare i valori di login_name, session_id e stato per trovare una sessione in base al nome dell'account di accesso.  
  
```sql  
SELECT session_id, login_name, status FROM sys.dm_pdw_exec_sessions;  
```  
  
È possibile terminare le sessioni con stato ' attivo ' o ' inattivo ' usando il comando KILL.  
  
```sql  
KILL 'SID137';  
```  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
