---
title: Operazioni comuni che richiedono il backup del database | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- recovery [SQL Server replication], actions requiring a backup
- restoring [SQL Server replication], actions requiring a backup
- backups [SQL Server replication], actions requiring a backup
ms.assetid: a5975bf4-183e-42e3-b7d1-ad02f89d2e1d
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: bd7af8a1e1713f3f0013350517eeacd518e3e601
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/22/2020
ms.locfileid: "86918287"
---
# <a name="common-actions-requiring-an-updated-backup"></a>Operazioni comuni che richiedono il backup del database
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  Se si eseguono backup regolari del log, le eventuali modifiche correlate alla replica dovrebbero essere incluse nei backup del log. Se non si eseguono backup del log, effettuare un backup dei database di pubblicazione, di distribuzione e di sottoscrizione, nonché dei database **msdb**e **master** dopo avere apportato modifiche alla topologia o allo schema di replica.  
  
## <a name="publication-database"></a>Database di pubblicazione  
 È necessario eseguire il backup del database di pubblicazione in seguito al completamento delle operazioni seguenti:  
  
-   Creazione di nuove pubblicazioni.  
  
-   Modifica delle proprietà di una pubblicazione, inclusa l'applicazione di filtri.  
  
-   Aggiunta di articoli a una pubblicazione esistente.  
  
-   Reinizializzazione delle sottoscrizioni nell'intera pubblicazione.  
  
-   Modifica dello schema in una tabella pubblicata.  
  
-   Esecuzione di uno script su richiesta con [sp_addscriptexec &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addscriptexec-transact-sql.md).  
  
-   Modifica delle proprietà di un articolo.  
  
-   Eliminazione di pubblicazioni.  
  
-   Eliminazione di articoli.  
  
-   Disabilitazione della replica.  
  
## <a name="distribution-database"></a>Database di distribuzione  
 È necessario eseguire il backup del database di distribuzione in seguito al completamento delle operazioni seguenti:  
  
-   Creazione o modifica dei profili agenti di replica.  
  
-   Modifica dei parametri dei profili agenti di replica.  
  
-   Modifica delle proprietà degli agenti di replica (incluse le pianificazioni) per qualsiasi sottoscrizione push.  
  
-   Un nuovo intervallo di valori Identity viene assegnato dalla caratteristica di gestione automatica degli intervalli di valori Identity.  
  
## <a name="subscription-database"></a>Database di sottoscrizione  
 È necessario eseguire il backup del database di sottoscrizione in seguito al completamento delle operazioni seguenti:  
  
-   Modifica delle proprietà di una sottoscrizione.  
  
-   Modifica della priorità di una sottoscrizione di tipo merge nel server di pubblicazione.  
  
-   Eliminazione di sottoscrizioni.  
  
-   Disabilitazione della replica.  
  
## <a name="msdb-database"></a>Database msdb  
 È necessario eseguire il backup del database di sistema **msdb** nel nodo appropriato in seguito al completamento delle operazioni seguenti:  
  
-   Attivazione o disabilitazione della replica.  
  
-   Aggiunta o eliminazione di un database di distribuzione (nel server di distribuzione).  
  
-   Attivazione o disabilitazione di un database per la pubblicazione (nel server di pubblicazione).  
  
-   Creazione o modifica dei profili agenti di replica (nel server di distribuzione).  
  
-   Modifica dei parametri dei profili agenti di replica (nel server di distribuzione).  
  
-   Modifica delle proprietà degli agenti di replica (incluse le pianificazioni) per qualsiasi sottoscrizione push (nel server di distribuzione).  
  
-   Modifica delle proprietà degli agenti di replica (incluse le pianificazioni) per qualsiasi sottoscrizione pull (nel Sottoscrittore).  
  
-   Creazione di un pacchetto DTS associato a una pubblicazione transazionale che utilizza sottoscrizioni trasformabili (nel server di distribuzione e nel Sottoscrittore).  
  
-   Aggiunta o eliminazione di una sottoscrizione trasformabile (nel server di distribuzione e nel Sottoscrittore).  
  
## <a name="master-database"></a>Database master  
 È necessario eseguire il backup del database di sistema **master** nel nodo appropriato in seguito al completamento delle operazioni seguenti:  
  
-   Attivazione o disabilitazione della replica.  
  
-   Aggiunta o eliminazione di un database di distribuzione (nel server di distribuzione).  
  
-   Attivazione o disabilitazione di un database per la pubblicazione (nel server di pubblicazione).  
  
-   Aggiunta della prima pubblicazione o eliminazione dell'ultima pubblicazione in qualsiasi database (nel server di pubblicazione).  
  
-   Aggiunta della prima sottoscrizione o eliminazione dell'ultima sottoscrizione in qualsiasi database (nel Sottoscrittore).  
  
-   Attivazione o disabilitazione di un server di pubblicazione nel server di pubblicazione di distribuzione (nel server di pubblicazione e nel server di distribuzione).  
  
## <a name="see-also"></a>Vedere anche  
 [Backup e ripristino di database SQL Server](../../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Eseguire il backup e ripristino di database replicati](../../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)  
  
  
