---
description: Controlli e registrazione di Posta elettronica database
title: Controlli e registrazione di Posta elettronica database | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- auditing [SQL Server]
- Database Mail [SQL Server], auditing
- logs [Database Mail]
- audits [SQL Server], Database Mail
- Database Mail [SQL Server], logging
ms.assetid: 846589ee-5fe5-4ab3-b335-0c253e569f99
author: stevestein
ms.author: sstein
ms.openlocfilehash: 1fcb4dbe767c549987c6c54a056d0f33f3708a4b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499766"
---
# <a name="database-mail-log-and-audits"></a>Controlli e registrazione di Posta elettronica database
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  La funzionalità di registrazione di Posta elettronica database è stata progettata per fornire un modo per isolare e correggere i problemi. Posta elettronica database memorizza le informazioni del log nel database **msdb** . Le informazioni sul contenuto di Posta elettronica database, dello stato dei messaggi di posta elettronica e eventuali messaggi ricevuti, come ad esempio messaggi di errore, vengono registrati da Posta elettronica database e possono essere utilizzati per scopi di diagnosi e controllo.  
  
## <a name="database-mail-logs"></a>Log di Posta elettronica database  
 Le tabelle presenti nel database **msdb** registrano le informazioni provenienti dal [Programma esterno di Posta elettronica database](../../relational-databases/database-mail/database-mail-external-program.md). Le [Viste di Posta elettronica database &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mail-views-transact-sql.md) espongono le tabelle per la risoluzione dei problemi. Nella vista [sysmail_event_log &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sysmail-event-log-transact-sql.md) vengono visualizzati errori se Service Broker non è in grado di attivare il programma esterno, se il programma esterno rileva errori di rete oppure se il server SMTP (Simple Mail Transfer Protocol) rifiuta un messaggio di posta elettronica. Se il programma esterno non può connettersi alle tabelle di **msdb** , gli errori verranno registrati nel registro eventi applicazioni di Windows.  
  
 Le tabelle interne nel database **msdb** includono i messaggi di posta elettronica e gli allegati inviati da Posta elettronica database, insieme allo stato corrente di ogni messaggio. Le tabelle vengono aggiornate da Posta elettronica database all'elaborazione di ogni messaggio.  
  
## <a name="database-mail-auditing-tasks"></a>Attività di controllo di Posta elettronica database  
  
|Analisi e gestione dei log di Posta elettronica database|Collegamento all'argomento|  
|-|-|  
|Controllo dello stato di recapito di un singolo messaggio|[Controllare lo stato di messaggi di posta elettronica inviati con Posta elettronica database](../../relational-databases/database-mail/check-the-status-of-e-mail-messages-sent-with-database-mail.md)|  
|Pulizia dei messaggi di Posta elettronica database, allegati e voci di registro|[sysmail_delete_mailitems_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql.md)<br /><br /> [sysmail_delete_log_sp &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sysmail-delete-log-sp-transact-sql.md)|  
|Archiviazione di messaggi di Posta elettronica database e log|[Creare un processo di SQL Server Agent per l'archiviazione di messaggi e log eventi di Posta elettronica database](../../relational-databases/database-mail/create-a-sql-server-agent-job-to-archive-database-mail-messages-and-event-logs.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare l'utilizzo delle risorse &#40;Monitor di sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
