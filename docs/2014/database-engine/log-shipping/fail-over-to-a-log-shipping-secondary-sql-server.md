---
title: Failover su un database secondario per il log shipping (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- primary databases [SQL Server]
- secondary data files [SQL Server], manual fail over
- log shipping [SQL Server], failover
- failover [SQL Server], log shipping
ms.assetid: edfe5d59-4287-49c1-96c9-dd56212027bc
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 64fa315457361e8d160735f38156e79ea667a4da
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62774191"
---
# <a name="fail-over-to-a-log-shipping-secondary-sql-server"></a>Failover su un database secondario per il log shipping (SQL Server)
  L'esecuzione del failover in un database secondario per il log shipping è utile in caso di errore o di manutenzione dell'istanza del server primario.  
  
## <a name="preparing-for-a-controlled-failover"></a>Preparazione di un failover controllato  
 I database primario e secondario non sono in genere sincronizzati, in quanto il database primario continua a essere aggiornato dopo l'ultimo processo di backup. In alcuni casi, inoltre, i backup del log delle transazioni recenti non sono stati copiati nelle istanze del server secondario oppure è possibile che alcuni backup del log copiati non siano stati ancora applicati al database secondario. Se possibile, è consigliabile iniziare con la sincronizzazione di tutti i database secondari con il database primario.  
  
 Per informazioni sui processi per il log shipping, vedere [Informazioni sul log shipping &#40;SQL Server&#41;](about-log-shipping-sql-server.md).  
  
## <a name="failing-over"></a>Esecuzione del failover  
 Per eseguire il failover su un database secondario, eseguire le operazioni seguenti:  
  
1.  Copiare i file di backup non ancora copiati dalla condivisione di backup alla cartella di destinazione della copia in ogni server secondario.  
  
2.  Applicare in sequenza i backup del log delle transazioni non ancora applicati a ogni database secondario. Per altre informazioni, vedere [Applicazione dei backup di log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/apply-transaction-log-backups-sql-server.md).  
  
3.  Se il database primario è accessibile, eseguire il backup del log delle transazioni attivo e applicarlo ai database secondari.  
  
     Se l'istanza del server primario originale non è danneggiata, eseguire il backup della parte finale del log delle transazioni del database primario tramite WITH NORECOVERY. In questo modo il database resta nella stato di ripristino e pertanto non disponibile agli utenti. Infine è possibile eseguirne il rollforward applicando i backup del log delle transazioni del database primario da sostituire.  
  
     Per altre informazioni, vedere [Backup di log delle transazioni &#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md).  
  
4.  Dopo la sincronizzazione dei server secondari, è possibile eseguire il failover su qualsiasi server recuperando il relativo database secondario e reindirizzando i client a quell'istanza del server. L'operazione di recupero consente di rendere consistente il database e di portarlo online.  
  
    > [!NOTE]  
    >  Quando si rende disponibile un database secondario, è necessario assicurarsi che i relativi metadati siano coerenti con quelli del database primario originale. Per ulteriori informazioni, vedere [gestire i metadati quando si rende disponibile un database in un'altra istanza del Server &#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md).  
  
5.  Dopo il recupero di un database secondario, è possibile riconfigurarlo affinché funga da database primario per altri database secondari.  
  
     Se non è disponibile un altro database secondario, vedere [Configurare il log shipping &#40;SQL Server&#41;](configure-log-shipping-sql-server.md).  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Attività correlate  
  
-   [Modificare i ruoli tra i server primario e secondario per il log shipping &#40;SQL Server&#41;](change-roles-between-primary-and-secondary-log-shipping-servers-sql-server.md)  
  
-   [Gestione di account di accesso e di processi dopo un cambio di ruolo &#40;SQL Server&#41;](../../sql-server/failover-clusters/management-of-logins-and-jobs-after-role-switching-sql-server.md)  
  
## <a name="see-also"></a>Vedi anche  
 [Tabelle e stored procedure per il log shipping](log-shipping-tables-and-stored-procedures.md)   
 [Informazioni sul &#40;di log shipping SQL Server&#41;](about-log-shipping-sql-server.md)   
 [Backup della parte finale del log &#40;SQL Server&#41;](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)  
  
  
