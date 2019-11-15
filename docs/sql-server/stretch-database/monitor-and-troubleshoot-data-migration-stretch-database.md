---
title: Monitor and troubleshoot data migration (Monitorare e risolvere i problemi relativi alla migrazione dei dati)
ms.date: 06/14/2016
ms.service: sql-server-stretch-database
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Stretch Database, monitoring
- monitoring Stretch Database
ms.assetid: 06950858-8c02-4ec6-9c59-42b787316a2d
author: rothja
ms.author: jroth
ms.custom: seo-dt-2019
ms.openlocfilehash: d204c7acfbd8598a7cbb66a41dcf89915fc711ef
ms.sourcegitcommit: f688a37bb6deac2e5b7730344165bbe2c57f9b9c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/08/2019
ms.locfileid: "73843784"
---
# <a name="monitor-and-troubleshoot-data-migration-stretch-database"></a>Monitorare e risolvere i problemi relativi alla migrazione dei dati (Stretch Database)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md-winonly.md)]


  Per monitorare la migrazione dei dati in Monitoraggio di Stretch Database, selezionare **Attività | Stretch | Monitoraggio** per un database in SQL Server Management Studio.  
  
## <a name="check-the-status-of-data-migration-in-the-stretch-database-monitor"></a>Controllare lo stato della migrazione dei dati in Stretch Database Monitor  
 Selezionare **Attività | Stretch | Monitoraggio** per un database in SQL Server Management Studio per aprire Monitoraggio di Stretch Database e monitorare la migrazione dei dati.  
  
-   Nella parte superiore della finestra di monitoraggio vengono visualizzate informazioni generali sul database SQL Server abilitato per l'estensione e sul database Azure remoto.  
  
-   Nella parte inferiore viene visualizzato lo stato della migrazione dei dati per ogni tabella abilitata per l'estensione nel database.  
  
 ![Monitoraggio di Stretch Database](../../sql-server/stretch-database/media/stretch-monitor.PNG "Monitoraggio di Stretch Database")  
  
##  <a name="Migration"></a> Controllare lo stato della migrazione dei dati in una DMV  
 Aprire la DMV **sys.dm_db_rda_migration_status** per visualizzare il numero di batch e righe di dati di cui è stata eseguita la migrazione. Per altre informazioni, vedere [sys.dm_db_rda_migration_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/stretch-database-sys-dm-db-rda-migration-status.md).  
  
##  <a name="Firewall"></a> Risolvere i problemi relativi alla migrazione dei dati  
 **Non viene eseguita la migrazione in Azure delle righe dalla tabella abilitata per l'estensione. Qual è il problema?**  
 Esistono diversi problemi che possono influire sulla migrazione. Verificare quanto segue.  
  
-   Verificare la connettività di rete per il computer SQL Server.  
  
-   Verificare che il firewall di Azure non impedisca a SQL Server di connettersi all'endpoint remoto.  
  
-   Verificare lo stato dell'ultimo batch nella DMV **sys.dm_db_rda_migration_status** . Se si è verificato un errore, controllare i valori error_number, error_state, ed error_severity per il batch.  
  
    -   Per altre informazioni sulla vista, vedere [sys.dm_db_rda_migration_status &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/stretch-database-sys-dm-db-rda-migration-status.md).  
  
    -   Per altre informazioni sul contenuto di un messaggio di errore di SQL Server, vedere [sys.messages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/messages-for-errors-catalog-views-sys-messages.md).  
  
 **Il firewall di Azure blocca le connessioni dal server locale.**  
 Può essere necessario aggiungere una regola nelle impostazioni del firewall di Azure del server di Azure per consentire a SQL Server di comunicare con il server remoto di Azure.  
  
## <a name="see-also"></a>Vedere anche  
 [Gestione e risoluzione dei problemi di Stretch Database](../../sql-server/stretch-database/manage-and-troubleshoot-stretch-database.md)  
  
  
