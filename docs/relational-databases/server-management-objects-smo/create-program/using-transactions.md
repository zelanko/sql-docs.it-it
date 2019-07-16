---
title: Utilizzo delle transazioni | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, transactions
- transactions [SMO]
- SMO [SQL Server], transactions
ms.assetid: 399aded8-bee3-4cfb-a671-1877c7d0de9f
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 53f5813aac141c82f87f3bec5164e5d617af6cce
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68098206"
---
# <a name="using-transactions"></a>Utilizzo di transazioni
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects (SMO), l'elaborazione delle transazioni viene eseguita mediante la connessione all'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizzando l'oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>. Il <xref:Microsoft.SqlServer.Management.Common.ServerConnection> oggetto fa riferimento il <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> proprietà del <xref:Microsoft.SqlServer.Management.Smo.Server> oggetto quando viene stabilita la connessione. Metodi come <xref:Microsoft.SqlServer.Management.Common.DataTransferProgressEventType.StartTransaction>, <xref:Microsoft.SqlServer.Management.Common.ServerConnection.RollBackTransaction%2A> e <xref:Microsoft.SqlServer.Management.Common.ServerConnection.CommitTransaction%2A> appartengono alla proprietà dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A>.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di programmi SMO](../../../relational-databases/server-management-objects-smo/create-program/creating-smo-programs.md)  
  
  
