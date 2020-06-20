---
title: Utilizzo di transazioni | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: a075719c8ed31ffcc1c34f2d013a8beb0ae40dae
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85003713"
---
# <a name="using-transactions"></a>Utilizzo di transazioni
  In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects (SMO), l'elaborazione delle transazioni viene eseguita mediante la connessione all'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizzando l'oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>. <xref:Microsoft.SqlServer.Management.Common.ServerConnection> <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> <xref:Microsoft.SqlServer.Management.Smo.Server> Quando viene stabilita la connessione, all'oggetto viene fatto riferimento dalla proprietà dell'oggetto. Metodi come <xref:Microsoft.SqlServer.Management.Common.DataTransferProgressEventType.StartTransaction>, <xref:Microsoft.SqlServer.Management.Common.ServerConnection.RollBackTransaction%2A> e <xref:Microsoft.SqlServer.Management.Common.ServerConnection.CommitTransaction%2A> appartengono alla proprietà dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A>.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di programmi SMO](creating-smo-programs.md)  
  
  
