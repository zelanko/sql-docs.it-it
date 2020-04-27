---
title: Risolvere i problemi relativi a un'operazione di aggiunta file non riuscita (Gruppi di disponibilità AlwaysOn) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- secondary databases [SQL Server], Availability Groups
- Availability Groups [SQL Server], troubleshooting
ms.assetid: 31ceaebf-864b-4dd0-9112-0d047b0316ad
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6940e9e40a09e5bd0c7afc591b34c17129350d74
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62813441"
---
# <a name="troubleshoot-a-failed-add-file-operation-alwayson-availability-groups"></a>Risolvere i problemi relativi a una operazione di aggiunta file non riuscita (Gruppi di disponibilità AlwaysOn)
  In alcune distribuzioni del gruppo di disponibilità AlwaysOn i percorsi di file nel sistema in cui è ospitata la replica primaria sono diversi da quelli nei sistemi in cui è ospitata una replica secondaria. Se il percorso di file di un'operazione di aggiunta di file non esiste in una replica secondaria, tale operazione non verrà completata nel database primario. Tuttavia, l'operazione di aggiunta di file determinerà la sospensione del database secondario. Questa situazione, a sua volta, potrebbe causare l'attivazione dello stato NON IN SINCRONIZZAZIONE della replica secondaria.  
  
> [!NOTE]  
>  Se possibile, è consigliabile che il percorso del file di un determinato database secondario, inclusa la lettera di unità, sia identico a quello del database primario corrispondente.  
  
## <a name="problem-resolution"></a>Risoluzione dei problemi  
 Per risolvere questo problema, il proprietario del database deve completare i passaggi seguenti:  
  
1.  Rimuovere il database secondario dal gruppo di disponibilità. Per altre informazioni, vedere [Rimuovere un database secondario da un gruppo di disponibilità &#40;SQL Server&#41;](remove-a-secondary-database-from-an-availability-group-sql-server.md).  
  
2.  Sul database secondario esistente, ripristinare un backup completo del filegroup che contiene il file aggiunto al database secondario, utilizzando WITH NORECOVERY e WITH MOVE (specificando il percorso di file sull'istanza del server che ospita la replica secondaria). Per altre informazioni, vedere [Ripristinare un database in una nuova posizione &#40;SQL Server&#41;](../../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md).  
  
3.  Eseguire il backup del log delle transazioni che contiene l'operazione di aggiunta file nel database primario e ripristinare manualmente il backup del log nel database secondario con WITH NORECOVERY e WITH MOVE.  
  
4.  Preparare il database secondario per creare di nuovo un join del gruppo di disponibilità, ripristinando, WITH NO RECOVERY, qualsiasi altro backup del log in sospeso dal database primario.  
  
5.  Unire nuovamente in join il database secondario al gruppo di disponibilità. Per altre informazioni, vedere [Creare un join di un database secondario a un gruppo di disponibilità &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Preparare manualmente un database secondario per un gruppo di disponibilità &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)   
 [Risolvere i problemi relativi agli utenti isolati &#40;SQL Server&#41;](../../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)   
 [Risolvere i problemi di Gruppi di disponibilità AlwaysOn &#40;di configurazione SQL Server eliminati&#41;](troubleshoot-always-on-availability-groups-configuration-sql-server.md)  
  
  
