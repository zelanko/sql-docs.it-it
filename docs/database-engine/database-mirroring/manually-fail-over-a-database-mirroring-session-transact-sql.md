---
title: Failover manuale in una sessione di mirroring del database (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: high-availability
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- failover [SQL Server], database mirroring
- manual failover [SQL Server]
- database mirroring [SQL Server], failover
ms.assetid: 36218d61-b5f5-4194-905a-608e0e903db4
author: MikeRayMSFT
ms.author: mikeray
manager: jroth
ms.openlocfilehash: cff69cccd05d48df6affeca17a6799f82e26e1f5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66795397"
---
# <a name="manually-fail-over-a-database-mirroring-session-transact-sql"></a>Failover manuale in una sessione di mirroring del database (Transact-SQL)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Quando il database con mirroring è sincronizzato, ovvero è in stato SYNCHRONIZED, il proprietario del database può iniziare il failover manuale al server mirror. Il failover manuale può essere avviato solo dal server principale.  
  
### <a name="to-manually-fail-over-a-database-mirroring-session"></a>Per eseguire il failover manuale in una sessione di mirroring del database  
  
1.  Connettersi al server principale.  
  
2.  Impostare il contesto del database sul database **master** :  
  
     **USE master;**  
  
3.  Eseguire l'istruzione seguente sul server principale:  
  
     [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md) *nome_database* SET PARTNER FAILOVER, dove *nome_database* rappresenta il database con mirroring.  
  
     Verrà avviata una transizione immediata del server mirror al ruolo principale.  
  
 Nel server principale precedente i client verranno disconnessi dal database e verrà eseguito il rollback delle transazioni di cui è in corso la migrazione.  
  
> [!NOTE]  
>  Le transazioni preparate utilizzando [!INCLUDE[msCoName](../../includes/msconame-md.md)] Distributed Transaction Coordinator ma delle quali non sia stato ancora eseguito il commit quando si verifica un failover sono considerate interrotte dopo il failover del database.  
  
## <a name="see-also"></a>Vedere anche  
 [Mirroring del database di ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-database-mirroring.md)   
 [Eseguire il failover manuale di una sessione di mirroring del database &#40;SQL Server Management Studio&#41;](../../database-engine/database-mirroring/manually-fail-over-a-database-mirroring-session-sql-server-management-studio.md)   
 [Cambio di ruolo durante una sessione di mirroring del database &#40;SQL Server&#41;](../../database-engine/database-mirroring/role-switching-during-a-database-mirroring-session-sql-server.md)  
  
  
