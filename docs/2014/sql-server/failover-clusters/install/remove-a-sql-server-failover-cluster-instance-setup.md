---
title: Rimuovere un'istanza del cluster di failover di SQL Server (programma di installazione) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- clusters [SQL Server], removing failover clustered instance
- failover clustering [SQL Server], removing failover clustered instance
- uninstalling failover clustered instances
- removing failover clustered instances
ms.assetid: bf63353b-69cf-4c5c-98ea-7b151e36537f
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 07b57b7ebea8a2bf5eaf381c09d7eb29dd6a4cd4
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52747403"
---
# <a name="remove-a-sql-server-failover-cluster-instance-setup"></a>Rimuovere un'istanza del cluster di failover di SQL Server (programma di installazione)
  Utilizzare questa procedura per disinstallare un'istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
> [!IMPORTANT]  
>  L'aggiornamento o la rimozione di un cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è riservata agli amministratori locali con autorizzazione di accesso come servizio su tutti i nodi del cluster di failover.  
  
 **Operazioni preliminari**  
  
 Si considerino gli aspetti seguenti prima di disinstallare un cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] :  
  
-   Se [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client viene disinstallato per errore, l'avvio delle risorse di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non riuscirà. Per reinstallare [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, eseguire il programma di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per installare i prerequisiti di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   Se si disinstalla un cluster di failover con più risorse cluster IP SQL, è necessario rimuovere le ulteriori risorse IP SQL utilizzando Cluster Administrator.  
  
 Per informazioni sulla sintassi del prompt dei comandi, vedere [installare SQL Server 2014 dal Prompt dei comandi](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
### <a name="to-uninstall-a-includessnoversionincludesssnoversion-mdmd-failover-cluster"></a>Per disinstallare un cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
  
1.  Per disinstallare un cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], utilizzare la funzionalità per la rimozione del nodo disponibile nel programma di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per rimuovere ogni nodo singolarmente. Per altre informazioni, vedere [Aggiungere o rimuovere nodi in un cluster di failover di SQL Server &#40;programma di installazione&#41;](add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Visualizzare e leggere i file di log del programma di installazione di SQL Server](../../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
