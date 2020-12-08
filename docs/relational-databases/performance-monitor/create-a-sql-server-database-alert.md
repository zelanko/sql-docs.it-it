---
title: Creare un avviso del database di SQL Server | Microsoft Docs
description: È possibile usare Monitor di sistema per creare un avviso del database di SQL Server da generare quando viene raggiunto un valore soglia specificato per un contatore di Monitor di sistema.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- database performance [SQL Server], alerts
- alerts [SQL Server], creating
- thresholds [SQL Server]
- database alerts [SQL Server]
- tuning databases [SQL Server], alerts
- monitoring performance [SQL Server], alerts
- monitoring server performance [SQL Server], alerts
- database monitoring [SQL Server], alerts
- server performance [SQL Server], alerts
ms.assetid: 0511136a-1b6b-4095-aa45-39e77b67aba2
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 512c902e0b35e15b65866464500b4928e105d4ad
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/02/2020
ms.locfileid: "96506036"
---
# <a name="create-a-sql-server-database-alert"></a>Creare un avviso del database di SQL Server
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  È possibile utilizzare Monitoraggio di sistema per creare un avviso da generare quando viene raggiunto un valore soglia specificato per un contatore di Monitoraggio di sistema. In risposta all'avviso, Monitoraggio di sistema avvia un'applicazione, ad esempio un'applicazione personalizzata programmata per gestire la condizione dell'avviso. Ad esempio, è possibile creare un avviso che viene generato quando il numero di deadlock supera un determinato valore.  
  
 È inoltre possibile definire avvisi utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Per altre informazioni, vedere [Avvisi](../../ssms/agent/alerts.md).  
  
 Per altre informazioni sull'uso di Monitoraggio di sistema per impostare un avviso del database di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vedere [Impostazione di un avviso del database di SQL Server &#40;Windows&#41;](../../relational-databases/performance/set-up-a-sql-server-database-alert-windows.md).  
  
## <a name="see-also"></a>Vedere anche  
 [sp_add_alert &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)   
 [sys.sysperfinfo &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql.md)  
  
  
