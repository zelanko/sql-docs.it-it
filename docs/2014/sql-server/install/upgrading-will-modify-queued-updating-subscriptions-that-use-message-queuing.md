---
title: L'aggiornamento modificherà le sottoscrizioni ad aggiornamento in coda che utilizzano Accodamento messaggi | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- subscriptions [SQL Server replication]
- MSMQ [SQL Server replication]
- queues [SQL Server replication]
- queued updating subscriptions [SQL Server replication]
ms.assetid: 97944de3-fbad-4db1-939a-dcd550bf5893
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1c723050f9e860534c5298df9a487337e319ff91
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66091408"
---
# <a name="upgrading-will-modify-queued-updating-subscriptions-that-use-message-queuing"></a>In seguito all'aggiornamento le sottoscrizioni ad aggiornamento in coda che utilizzano MSMQ verranno modificate in modo da utilizzare code di SQL Server
  È possibile che una o più sottoscrizioni ad aggiornamento in coda utilizzino [!INCLUDE[msCoName](../../includes/msconame-md.md)] Message Queuing (noto anche come MSMQ). Accodamento messaggi non è più supportato dalla replica, quindi le sottoscrizioni verranno modificate in modo che utilizzino una coda di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 È consentito solo un valore **SQL** . Le pubblicazioni esistenti che utilizzano Accodamento messaggi vengono modificate durante l'aggiornamento in modo da utilizzare una coda di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se si dispone di applicazioni che dipendono da un aggiornamento in coda tramite Message Queuing, sarà necessario riscrivere tali applicazioni per includere una coda di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per ulteriori informazioni sulle sottoscrizioni ad aggiornamento in coda, vedere "Sottoscrizioni aggiornabili per la replica transazionale" nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Con l'aggiornamento, le code di sottoscrizione MSMQ vengono rimosse se il servizio di accodamento messaggi è in esecuzione durante l'aggiornamento di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Se il servizio di accodamento messaggi non è in esecuzione, rimuovere manualmente le code al termine dell'aggiornamento. Per ulteriori informazioni sulla rimozione di code, vedere la documentazione di Windows.  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento della replica](../../../2014/sql-server/install/replication-upgrade-issues.md)  
  
  
