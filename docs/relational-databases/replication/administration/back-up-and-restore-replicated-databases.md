---
title: Eseguire il backup e ripristino di database replicati | Microsoft Docs
description: Esaminare informazioni generali e collegamenti a informazioni aggiuntive sulle strategie di backup e ripristino per ogni tipo di replica in SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- backups [SQL Server replication]
- administering replication, restoring
- backing up replicated databases
- backups [SQL Server replication], about backups
- restoring replicated databases [SQL Server replication]
- recovery [SQL Server replication], about recovery
- restoring databases [SQL Server], replicated databases
- backing up databases [SQL Server], replicated databases
- restoring [SQL Server replication], about restoring
- recovery [SQL Server replication]
- replication [SQL Server], administering
- distribution databases [SQL Server replication], backing up
- restoring [SQL Server replication]
- administering replication, backing up
ms.assetid: 04588807-21e7-4bbe-9727-b72f692cffa7
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: df0207225a5663675ac65c740a1dd5782775d96e
ms.sourcegitcommit: 19ff45e8a2f4193fe8827f39258d8040a88befc7
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2020
ms.locfileid: "83808013"
---
# <a name="back-up-and-restore-replicated-databases"></a>Backup e ripristino di database replicati
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

  Il backup e il ripristino dei dati dei database replicati richiedono un'attenzione particolare. In questo argomento sono fornite informazioni introduttive e collegamenti ad informazioni più approfondite sulle strategie di backup e ripristino per ogni tipo di replica.  
  
 La replica supporta il ripristino dei database replicati nello stesso server e nello stesso database da cui è stato creato il backup. Se si ripristina un backup di un database replicato in un altro server o database, le impostazioni di replica non potranno essere mantenute. In questo caso sarà necessario ricreare tutte le pubblicazioni e le sottoscrizioni dopo il ripristino dei backup.  
  
> [!NOTE]  
>  È possibile ripristinare un database replicato in un server di standby se si utilizza il log shipping. Per altre informazioni, vedere [Log shipping e replica &#40;SQL Server&#41;](../../../database-engine/log-shipping/log-shipping-and-replication-sql-server.md).  
  
 Il backup dei database replicati e dei relativi sistemi associati deve essere eseguito periodicamente. Eseguire il backup dei database seguenti:  
  
-   Database di pubblicazione nel server di pubblicazione.  
  
-   Database di distribuzione nel server di distribuzione.  
  
-   Database di sottoscrizione in ogni Sottoscrittore.  
  
-   Database di sistema **master** e **msdb** nel server di pubblicazione, nel database di distribuzione e in tutti i Sottoscrittori. È necessario che il backup di questi database venga eseguito contemporaneamente e che venga inoltre eseguito nello stesso momento di quello del relativo database di replica. Eseguire, ad esempio, il backup dei database **master** e **msdb** nel server di pubblicazione nello stesso momento in cui si esegue il backup del database di pubblicazione. Se il database di pubblicazione viene ripristinato, verificare che i database **master** e **msdb** siano consistenti con il database di pubblicazione in termini di impostazioni e di configurazione della replica.  
  
 Se si eseguono backup regolari del log, le eventuali modifiche correlate alla replica dovrebbero essere incluse nei backup del log. Se non si eseguono i backup del log, è necessario eseguire un backup ogni volta che un'impostazione relativa alla replica viene modificata. Per altre informazioni, vedere [Common Actions Requiring an Updated Backup](../../../relational-databases/replication/administration/common-actions-requiring-an-updated-backup.md).  
  
## <a name="backup-and-restore-strategies"></a>Strategie di backup e ripristino  
 Le strategie di backup e ripristino di ogni nodo in una topologia di replica variano in base al tipo di replica utilizzata. Per informazioni sulle strategie di backup e ripristino per ogni tipo di replica, vedere gli argomenti seguenti:  
  
-   [Strategie di backup e ripristino della replica snapshot e della replica transazionale](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-snapshot-and-transactional-replication.md)  
  
-   [Strategie di backup e ripristino della replica di tipo merge](../../../relational-databases/replication/administration/strategies-for-backing-up-and-restoring-merge-replication.md)  
  
 Ogni strategia di recupero include la conservazione in un luogo sicuro di uno script corrente delle impostazioni di replica. Se si verifica un errore in un server oppure è necessario configurare un ambiente di prova, è possibile modificare lo script tramite la modifica dei riferimenti ai nomi di server e quindi utilizzarlo per ricreare le impostazioni di replica. Oltre a creare script per le impostazioni di replica correnti, è consigliabile creare script anche per l'attivazione e la disabilitazione della replica. Per informazioni sulla creazione di script per oggetti di replica, vedere [Scripting Replication](../../../relational-databases/replication/scripting-replication.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Backup e ripristino di database SQL Server](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Best Practices for Replication Administration](../../../relational-databases/replication/administration/best-practices-for-replication-administration.md)  
  
  
