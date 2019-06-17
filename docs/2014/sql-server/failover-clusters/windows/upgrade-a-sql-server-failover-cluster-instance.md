---
title: Aggiornare un Cluster di Failover SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- upgrading failover clusters
- clusters [SQL Server], upgrading
- failover clustering [SQL Server], upgrading
ms.assetid: daac41fe-7d0b-4f14-84c2-62952ad8cbfa
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a7a8d5f04808582bd56c106adce0df2c1f66aa77
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62913724"
---
# <a name="upgrade-a-sql-server-failover-cluster"></a>Aggiornare un cluster di failover di SQL Server
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] supporta l'aggiornamento separato del [!INCLUDE[ssDE](../../../includes/ssde-md.md)] e di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] dai cluster di failover di [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] e [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] in tutti i nodi del cluster di failover.  
  
 I dettagli relativi al supporto sono i seguenti:  
  
-   L'aggiornamento è supportato sia tramite l'interfaccia utente sia dal prompt dei comandi. Per altre informazioni, vedere [Eseguire l'aggiornamento di un'istanza del cluster di failover di SQL Server &#40;installazione&#41;](upgrade-a-sql-server-failover-cluster-instance-setup.md) e [Installare SQL Server 2014 dal prompt dei comandi](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md).  
  
-   L'aggiornamento da [!INCLUDE[ssKilimanjaro](../../../includes/sskilimanjaro-md.md)] -è possibile eseguire l'aggiornamento dal prompt dei comandi in ogni nodo del cluster di failover o tramite l'interfaccia utente di installazione per aggiornare ogni nodo del cluster. Se nell'istanza che si intende aggiornare non sono presenti le caratteristiche di replica e di ricerca full-text, queste verranno installate automaticamente senza che sia possibile ometterle.  
  
-   Installazione del Service Pack: è necessario applicare separatamente i patch e i service pack di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ai cluster di failover di [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)] in tutti i nodi.  
  
-   Non sono supportati gli scenari seguenti:  
  
    -   Non è possibile eseguire la migrazione da un'istanza autonoma di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a un cluster di failover.  
  
    -   Aggiungere funzionalità a un cluster di failover. Non è possibile ad esempio aggiungere il [!INCLUDE[ssDE](../../../includes/ssde-md.md)] a un cluster di failover solo di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] esistente.  
  
    -   Non è possibile effettuare il downgrade di un nodo del cluster di failover a un'istanza autonoma.  
  
-   Per altre informazioni, vedere [Istanze del cluster di failover Always On (SQL Server)](always-on-failover-cluster-instances-sql-server.md).  
  
## <a name="upgrading-a-includessnoversionincludesssnoversion-mdmd-multi-subnet-failover-cluster"></a>Aggiornamento di un cluster di failover su più subnet di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]  
 È possibile aggiornare direttamente una non-multi-subnet [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cluster di failover a un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cluster di failover su più subnet. Per altre informazioni, vedere [Eseguire l'aggiornamento di un'istanza del cluster di failover di SQL Server &#40;installazione&#41;](upgrade-a-sql-server-failover-cluster-instance-setup.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiornamenti di versione ed edizione supportati](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md)   
 [Aggiornare un'istanza Cluster di Failover SQL Server &#40;programma di installazione&#41;](upgrade-a-sql-server-failover-cluster-instance-setup.md)   
 [Installazione di SQL Server 2014 dal prompt dei comandi](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)  
  
  
