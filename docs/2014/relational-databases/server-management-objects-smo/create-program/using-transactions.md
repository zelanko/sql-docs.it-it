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
manager: craigg
ms.openlocfilehash: 83baa905887609e89b372d4820346ab9aa97a056
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63192022"
---
# <a name="using-transactions"></a>Utilizzo di transazioni
  In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Management Objects (SMO), l'elaborazione delle transazioni viene eseguita mediante la connessione all'istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] utilizzando l'oggetto <xref:Microsoft.SqlServer.Management.Common.ServerConnection>. Quando <xref:Microsoft.SqlServer.Management.Common.ServerConnection> viene stabilita la connessione, <xref:Microsoft.SqlServer.Replication.ReplicationObject.ConnectionContext%2A> all'oggetto viene <xref:Microsoft.SqlServer.Management.Smo.Server> fatto riferimento dalla proprietà dell'oggetto. Metodi come <xref:Microsoft.SqlServer.Management.Common.DataTransferProgressEventType.StartTransaction>, <xref:Microsoft.SqlServer.Management.Common.ServerConnection.RollBackTransaction%2A> e <xref:Microsoft.SqlServer.Management.Common.ServerConnection.CommitTransaction%2A> appartengono alla proprietà dell'oggetto <xref:Microsoft.SqlServer.Management.Smo.Server.ConnectionContext%2A>.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di programmi SMO](creating-smo-programs.md)  
  
  
