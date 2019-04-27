---
title: Avviare Monitoraggio mirroring del database (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- monitoring database mirroring [SQL Server]
- Database Mirroring Monitor [SQL Server], starting
- database mirroring [SQL Server], monitoring
ms.assetid: 53165335-97ca-4f88-8e78-22f1839dee98
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 7a48c6620d4395cd44aac6f43cd1817cfebf785e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62754894"
---
# <a name="start-database-mirroring-monitor-sql-server-management-studio"></a>Avviare Monitoraggio mirroring del database (SQL Server Management Studio)
  Monitoraggio mirroring del database è un componente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Monitoraggio avviato da [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
> [!NOTE]  
>  Il monitoraggio mirroring del database non è disponibile in tutte le edizioni di [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per un elenco delle funzionalità supportate dalle edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
### <a name="to-launch-the-database-mirroring-monitor"></a>Per avviare Monitoraggio mirroring del database  
  
1.  Dopo aver attivato la connessione all'istanza del server principale, in Esplora oggetti fare clic sul nome del server per espandere l'albero.  
  
2.  Espandere **Database**e selezionare il database da monitorare.  
  
3.  Fare clic con il pulsante destro del mouse sul database, selezionare **Attività**e quindi fare clic su **Avvia Monitoraggio mirroring del database**.  
  
4.  Nella finestra di dialogo **Monitoraggio mirroring del database** fare clic su **Registra database con mirroring** per registrare uno o più database con mirroring.  
  
    > [!NOTE]  
    >  Quando si registra un database in un partner, automaticamente verrà registrato anche nell'altro partner. Se il server di monitoraggio dispone già delle credenziali per la connessione all'istanza dell'altro partner, eseguirà automaticamente la connessione. In caso contrario tenterà di eseguire la connessione tramite l'autenticazione di Windows. Se si vuole modificare le credenziali usate per la connessione alle istanze del server, fare clic su **Quando viene scelto OK visualizza la finestra di dialogo Gestione connessioni a istanze server**.  
  
 Per altre informazioni su Monitoraggio mirroring del database, vedere [Panoramica di Monitoraggio mirroring del database](database-mirroring-monitor-overview.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Mirroring del database &#40;SQL Server&#41;](database-mirroring-sql-server.md)   
 [Stabilire una sessione di mirroring del database tramite autenticazione di Windows &#40;SQL Server Management Studio&#41;](establish-database-mirroring-session-windows-authentication.md)  
  
  
