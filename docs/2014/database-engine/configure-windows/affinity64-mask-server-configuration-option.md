---
title: Opzione di configurazione del server affinity64 mask | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- processor affinity [SQL Server]
- affinity64 mask option
- binding processors [SQL Server]
ms.assetid: 75ed08c7-f85c-4e15-9ee1-e7bc545d3293
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 20e4cf3af48fa560293a9de05e768410d561a33b
ms.sourcegitcommit: 04dd0620202287869b23cc2fde998a18d3200c66
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/30/2018
ms.locfileid: "52641182"
---
# <a name="affinity64-mask-server-configuration-option"></a>Opzione di configurazione affinity64 mask
  L'opzione affinity64 mask associa i processori a thread specifici ed è simile all'opzione affinity mask. Utilizzare l'opzione affinity mask per associare i primi 32 processori e l'opzione affinity64 mask per associare i processori rimanenti del computer. L'opzione è disponibile solo nella versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]a 64 bit.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepNextAvoid](../../includes/ssnotedepnextavoid-md.md)] Usare invece [ALTER SERVER CONFIGURATION &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-server-configuration-transact-sql).  
  
## <a name="see-also"></a>Vedere anche  
 [Opzione di configurazione del server affinity mask](affinity-mask-server-configuration-option.md)   
 [Monitoraggio dell'utilizzo delle risorse &#40;Monitor di sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)   
 [Opzioni di configurazione del server &#40;SQL Server&#41;](server-configuration-options-sql-server.md)   
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)  
  
  
