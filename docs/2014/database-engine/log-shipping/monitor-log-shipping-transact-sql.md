---
title: Monitorare il log shipping (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server], status
- history tables [SQL Server]
- historical information [SQL Server], log shipping
- log shipping [SQL Server], monitoring
- alerts [SQL Server], log shipping
- status information [SQL Server], log shipping
- monitoring log shipping [SQL Server]
ms.assetid: acf3cd99-55f7-4287-8414-0892f830f423
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d480fe510b6d2e252faefaae13d7dd3776c8ec5d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62774885"
---
# <a name="monitor-log-shipping-transact-sql"></a>Monitorare il log shipping (Transact-SQL)
  Dopo aver configurato il log shipping, è possibile monitorare le informazioni relative allo stato di tutti i server di log shipping. La cronologia e lo stato delle operazioni di log shipping vengono salvati sempre in locale dai processi per il log shipping. La cronologia e lo stato dell'operazione di backup vengono memorizzati sul server primario, mentre la cronologia e lo stato delle operazioni di copia e ripristino sono memorizzati sul server secondario. Se è stato implementato un server di monitoraggio remoto, queste informazioni vengono memorizzate anche sul server di monitoraggio.  
  
 È possibile configurare avvisi che verranno attivati se le operazioni di log shipping non avvengono secondo la pianificazione. Gli errori sono generati da un processo per la gestione degli avvisi che controlla lo stato delle operazioni di backup e ripristino. È possibile definire avvisi che notifichino a un operatore quando si verificano questi errori. Se è configurato un server di monitoraggio, su di esso viene eseguito un processo per la gestione degli avvisi che genera errori per tutte le operazioni nella configurazione per il log shipping. Se non è specificato alcun server di monitoraggio, viene eseguito un processo per la gestione degli avvisi sull'istanza del server primario, che monitora l'operazione di backup. Se non è specificato alcun server di monitoraggio, su ogni istanza del server secondario viene eseguito un processo per la gestione degli avvisi per monitorare le operazioni di copia e ripristino locali.  
  
> [!IMPORTANT]  
>  Per eseguire il monitoraggio di una configurazione per il log shipping, è necessario aggiungere il server di monitoraggio quando si abilita il log shipping. Se un server di monitoraggio viene aggiunto in un momento successivo, sarà necessario rimuovere la configurazione per il log shipping e sostituirla con una configurazione nuova che includa un server di monitoraggio. Per altre informazioni, vedere [Configurare il log shipping &#40;SQL Server&#41;](configure-log-shipping-sql-server.md). Dopo avere configurato il server di monitoraggio, inoltre, non sarà possibile modificarlo senza prima rimuovere il log shipping.  
  
## <a name="history-tables-containing-monitoring-information"></a>Tabelle della cronologia contenenti informazioni di monitoraggio  
 Le tabelle della cronologia di monitoraggio includono i metadati memorizzati sul server di monitoraggio. Una copia delle informazioni specifiche relative a un determinato server primario o secondario vengono inoltre memorizzate in locale.  
  
 È possibile eseguire query su queste tabelle per monitorare lo stato di una sessione di log shipping. Ad esempio, per ottenere lo stato del log shipping, verificare lo stato e la cronologia dei processi di backup, di copia e di ripristino. È possibile visualizzare i dettagli specifici relativi agli errori e alla cronologia del log shipping eseguendo query sulle tabelle di monitoraggio seguenti.  
  
|Tabella|Descrizione|  
|-----------|-----------------|  
|[log_shipping_monitor_alert](/sql/relational-databases/system-tables/log-shipping-monitor-alert-transact-sql)|Memorizza l'ID del processo per la gestione degli avvisi.|  
|[log_shipping_monitor_error_detail](/sql/relational-databases/system-tables/log-shipping-monitor-error-detail-transact-sql)|Memorizza i dettagli relativi agli errori per i processi di log shipping. È possibile eseguire query su questa tabella per visualizzare gli errori relativi a una sessione di agente. Facoltativamente, è possibile ordinare gli errori in base alla data e all'ora di registrazione. Ogni errore viene registrato come una sequenza di eccezioni, mentre più errori (sequenze) possono essere ordinati per sessione di agente.|  
|[log_shipping_monitor_history_detail](/sql/relational-databases/system-tables/log-shipping-monitor-history-detail-transact-sql)|Include i dettagli della cronologia per gli agenti di log shipping. È possibile eseguire query su questa tabella per visualizzare i dettagli della cronologia di una sessione di agente.|  
|[log_shipping_monitor_primary](/sql/relational-databases/system-tables/log-shipping-monitor-primary-transact-sql)|Memorizza un record di monitoraggio per il database primario in ogni configurazione per il log shipping, incluse le informazioni relative all'ultimo file di backup e all'ultimo file ripristinato che siano utili per il monitoraggio.|  
|[log_shipping_monitor_secondary](/sql/relational-databases/system-tables/log-shipping-monitor-secondary-transact-sql)|Memorizza un record di monitoraggio per ogni database secondario, incluse le informazioni relative all'ultimo file di backup e all'ultimo file ripristinato che siano utili per il monitoraggio.|  
  
## <a name="stored-procedures-for-monitoring-log-shipping"></a>Stored procedure per il monitoraggio del log shipping  
 Le informazioni relative al monitoraggio e alla cronologia vengono archiviate nelle tabelle di **msdb**, accessibili con le stored procedure di log shipping. Eseguire le stored procedure sui server specificati nella tabella seguente.  
  
|Stored procedure|Descrizione|Eseguire la stored procedure su|  
|----------------------|-----------------|---------------------------|  
|[sp_help_log_shipping_monitor_primary](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-primary-transact-sql)|Restituisce i record di monitoraggio per il database primario specificato dalla tabella **log_shipping_monitor_primary** .|Server di monitoraggio o server primario|  
|[sp_help_log_shipping_monitor_secondary](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-secondary-transact-sql)|Restituisce i record di monitoraggio per il database secondario specificato dalla tabella **log_shipping_monitor_secondary** .|Server di monitoraggio oppure server secondario|  
|[sp_help_log_shipping_alert_job](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-alert-job-transact-sql)|Restituisce l'ID processo del processo per la gestione degli avvisi.|Server di monitoraggio, oppure server primario o secondario se non è definito alcun server di monitoraggio|  
|[sp_help_log_shipping_primary_database](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-primary-database-transact-sql)|Recupera le impostazioni del database primario e visualizza i valori dalle tabelle **log_shipping_primary_databases** e **log_shipping_monitor_primary** .|Server primario|  
|[sp_help_log_shipping_primary_secondary](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-primary-secondary-transact-sql)|Recupera i nomi dei database secondari per un database primario.|Server primario|  
|[sp_help_log_shipping_secondary_database](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-database-transact-sql)|Recupera le impostazioni del database secondario dalle tabelle **log_shipping_secondary**, **log_shipping_secondary_databases** e **log_shipping_monitor_secondary** .|Server secondario|  
|[sp_help_log_shipping_secondary_primary &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-secondary-primary-transact-sql)|Tramite questa stored procedure vengono recuperate le impostazioni di un database primario specificato nel server secondario.|Server secondario|  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare il report di log shipping &#40;SQL Server Management Studio&#41;](view-the-log-shipping-report-sql-server-management-studio.md)   
 [Stored procedure e tabelle per il log shipping](log-shipping-tables-and-stored-procedures.md)  
  
  
