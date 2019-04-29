---
title: Oggetti di messaggistica di Posta elettronica database| Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Database Mail [SQL Server], host databases
- Database Mail [SQL Server], messaging objects
- mail host databases [SQL Server]
- host databases [Database Mail]
ms.assetid: 5aa2886e-1db1-4066-85df-57ccf4538c54
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3657e45d18ac84ad737a016150692730f736b55f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62917704"
---
# <a name="database-mail-messaging-objects"></a>Oggetti di messaggistica di Posta elettronica database
  Il database **msdb** funge da host della posta elettronica. Questo database include le stored procedure e gli oggetti di messaggistica per Posta elettronica database. In Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] è disponibile la Configurazione guidata posta elettronica database che consente di abilitare questo componente, creare e gestire profili e account e configurare le opzioni di Posta elettronica database.  
  
##  <a name="ComponentsAndConcepts"></a> Oggetti in un database **msdb**  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] deve essere abilitato nel database **msdb** . Posta elettronica database, tuttavia, non utilizza le funzionalità di rete di [!INCLUDE[ssSB](../../includes/sssb-md.md)] . Non è quindi necessario che gli utenti creino un endpoint di [!INCLUDE[ssSB](../../includes/sssb-md.md)] per l'utilizzo di Posta elettronica database. Il processo esterno di Posta elettronica database utilizza una connessione [!INCLUDE[vstecado](../../includes/vstecado-md.md)] standard per comunicare con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Quando abilitato, Posta elettronica database espone gli oggetti seguenti nel database **msdb** quando viene abilitata.  
  
 Tali oggetti rappresentano l'interfaccia per Posta elettronica database all'interno del database host della posta elettronica. Per implementare le funzionalità fornite dagli oggetti elencati sopra, vengono installati altri oggetti che sono tuttavia riservati per utilizzo interno.  
  
|Nome|Tipo|Descrizione|  
|----------|----------|-----------------|  
|[sysmail_allitems &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sysmail-allitems-transact-sql)|`View`|Elenca tutti i messaggi inviati a Posta elettronica database.|  
|[sysmail_event_log &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sysmail-event-log-transact-sql)|`View`|Elenca i messaggi relativi al comportamento di [Database Mail External Program](database-mail-external-program.md).|  
|[sysmail_faileditems &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sysmail-faileditems-transact-sql)|`View`|Informazioni relative ai messaggi che non è stato possibile inviare tramite Posta elettronica database.|  
|[sysmail_mailattachments &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sysmail-mailattachments-transact-sql)|`View`|Informazioni relative agli allegati ai messaggi di Posta elettronica database.|  
|[sysmail_sentitems &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sysmail-sentitems-transact-sql)|`View`|Informazioni relative ai messaggi inviati tramite Posta elettronica database.|  
|[sysmail_unsentitems &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sysmail-unsentitems-transact-sql)|`View`|Informazioni relative ai messaggi di cui è in corso un tentativo di invio da parte di Posta elettronica database.|  
|[sp_send_dbmail &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-send-dbmail-transact-sql)|`Stored Procedure`|Invia messaggi di posta elettronica tramite Posta elettronica database.|  
|[sysmail_delete_log_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-delete-log-sp-transact-sql)|`Stored Procedure`|Elimina i messaggi dal log di Posta elettronica database.|  
|[sysmail_delete_mailitems_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-delete-mailitems-sp-transact-sql)|`Stored Procedure`|Elimina gli elementi di posta dalla coda di Posta elettronica database.|  
|[sysmail_help_status_sp &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sysmail-help-status-sp-transact-sql)|`Stored Procedure`|Indica se Posta elettronica database è stato avviato.|  
|[sysmail_start_sp (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-start-sp-transact-sql)|`Stored Procedure`|Avvia gli oggetti Service Broker utilizzati dal programma esterno, che vengono avviati per impostazione predefinita.|  
|[sysmail_stop_sp (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sysmail-stop-sp-transact-sql)|`Stored Procedure`|Arresta gli oggetti Service Broker utilizzati dal programma esterno.|  
  

  
## <a name="see-also"></a>Vedere anche  
 [Posta elettronica database](database-mail.md)   
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)  
  
  
