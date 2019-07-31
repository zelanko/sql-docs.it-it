---
title: Eseguire l'aggiornamento di un'istanza del cluster di failover di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 10/01/2017
ms.prod: sql
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
ms.openlocfilehash: 681e944da0a49c6a1b485606e5ed1ed0bd8ffd0f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67904981"
---
# <a name="upgrade-a-sql-server-failover-cluster-instance"></a>Eseguire l'aggiornamento di un'istanza del cluster di failover di SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] supporta l'aggiornamento di un cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a una nuova versione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o a un nuovo Service Pack o aggiornamento cumulativo di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], oppure quando si esegue l'installazione in un nuovo Service Pack o aggiornamento cumulativo di Windows separatamente in tutti i nodi cluster di failover, con tempo di inattività limitato a un singolo failover manuale (o due failover manuali in caso di failback alla replica primaria originale).  
  
 L'aggiornamento del sistema operativo Windows di un cluster di failover non è supportato per i sistemi operativi precedenti a [!INCLUDE[winblue-server-2-md](../../../includes/winblue-server-2-md.md)]. Per aggiornare un nodo del cluster in esecuzione in [!INCLUDE[winblue-server-2-md](../../../includes/winblue-server-2-md.md)] o versioni successive, vedere [Eseguire un aggiornamento o un aggiornamento in sequenza](#perform-a-rolling-upgrade-or-update).  
  
 I dettagli relativi al supporto sono i seguenti:  
  
-   L'aggiornamento di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è supportato sia tramite l'interfaccia utente che al prompt dei comandi. È possibile eseguire l'aggiornamento dal prompt dei comandi in ogni nodo del cluster di failover o tramite l'interfaccia utente del programma di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per aggiornare ogni nodo del cluster.  Per altre informazioni, vedere [Aggiornare un'istanza del cluster di failover di SQL Server &#40;programma di installazione&#41;](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md) e [Installare SQL Server dal prompt dei comandi](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  
  
-   In un aggiornamento di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] non sono supportati gli scenari seguenti:  
  
    -   Non è possibile eseguire l'aggiornamento da un'istanza autonoma di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a un cluster di failover.  
  
    -   Non è possibile aggiungere funzionalità a un cluster di failover. Non è possibile ad esempio aggiungere il [!INCLUDE[ssDE](../../../includes/ssde-md.md)] a un cluster di failover solo di [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]esistente.  
  
    -   Non è possibile effettuare il downgrade di un nodo del cluster di failover a un'istanza autonoma.  
  
    -   La modifica dell'edizione del cluster di failover è limitata a determinati scenari. Per altre informazioni, vedere [Aggiornamenti di versione ed edizione supportati](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md).  
  
-   Durante l'aggiornamento del cluster di failover, il tempo di inattività è limitato alla durata del failover e al tempo necessario per l'esecuzione degli script di aggiornamento. Se si segue il processo di aggiornamento in sequenza del cluster di failover indicato sotto e sono soddisfatti tutti i prerequisiti in tutti i nodi prima di iniziare il processo di aggiornamento, il tempo di inattività è minimo. L'aggiornamento di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando le tabelle ottimizzate per la memoria sono in uso richiede un tempo maggiore. Per altre informazioni, vedere [pianificare e testare il Database Engine Upgrade Plan](../../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md).  
  
## <a name="prerequisites"></a>Prerequisites  
 Prima di iniziare, esaminare le informazioni seguenti:  
  
-   [Aggiornamenti di versione ed edizione supportati](../../../database-engine/install-windows/supported-version-and-edition-upgrades.md): verificare che sia possibile eseguire l'aggiornamento a [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] dalla versione del sistema operativo Windows e di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in uso. Non è ad esempio possibile eseguire l'aggiornamento direttamente da un'istanza di clustering di failover di SQL Server 2005 a [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] o aggiornare un cluster di failover in esecuzione in [!INCLUDE[winxpsvr-md](../../../includes/winxpsvr-md.md)].  
  
-   [Scegliere un metodo di aggiornamento del motore di database](../../../database-engine/install-windows/choose-a-database-engine-upgrade-method.md): selezionare il metodo e la procedura di aggiornamento appropriati in base alla verifica degli aggiornamenti della versione e dell'edizione supportate e anche agli altri componenti installati nell'ambiente interessato per aggiornare i componenti nell'ordine corretto.  
  
-   [Pianificare e testare il piano di aggiornamento del motore di database](../../../database-engine/install-windows/plan-and-test-the-database-engine-upgrade-plan.md): esaminare le note sulla versione, i problemi di aggiornamento noti, l'elenco di controllo pre-aggiornamento e sviluppare e testare il piano di aggiornamento.  
  
-   [Requisiti hardware e software per l'installazione di SQL Server ](../../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md):  esaminare i requisiti software per l'installazione di [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Se è necessario software aggiuntivo, installarlo in ogni nodo prima di iniziare il processo di aggiornamento per ridurre al minimo eventuali tempi di inattività.  
  
## <a name="perform-a-rolling-upgrade-or-update"></a>Eseguire un aggiornamento o un aggiornamento in sequenza  
 Per aggiornare un cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], eseguire il programma di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] per aggiornare i nodi del cluster di failover, uno alla volta, a partire dai nodi passivi. Man mano che viene aggiornato, ogni nodo viene escluso dai possibili proprietari del cluster di failover. In caso di failover imprevisto, i nodi aggiornati non partecipano al failover fino a quando la proprietà del gruppo di risorse del cluster non viene spostata in un nodo aggiornato dal programma di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
 Per impostazione predefinita, il programma di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] determina automaticamente il momento in cui eseguire il failover a un nodo aggiornato, che dipende dal numero complessivo di nodi nell'istanza del cluster di failover e dal numero di nodi già aggiornati. Quando un numero di nodi uguale o maggiore della metà è già stato aggiornato, il programma di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] esegue il failover a un nodo aggiornato nel momento in cui si esegue l'aggiornamento del nodo successivo. In seguito al failover a un nodo aggiornato, il gruppo cluster viene spostato in un nodo aggiornato. Tutti i nodi aggiornati vengono inseriti nell'elenco dei possibili proprietari e tutti i nodi non ancora aggiornati vengono rimossi da tale elenco. Man mano che ne viene eseguito l'aggiornamento, ogni nodo rimanente viene aggiunto ai possibili proprietari del cluster di failover.  
  
 Questo processo comporta un tempo di inattività limitato alla durata del failover e al tempo di esecuzione degli script di aggiornamento del database durante l'aggiornamento dell'intero cluster di failover.  
  
 Per controllare il comportamento del failover dei nodi del cluster durante il processo di aggiornamento, eseguire l'operazione di aggiornamento nel prompt dei comandi e utilizzare il parametro /FAILOVERCLUSTERROLLOWNERSHIP. Per altre informazioni, vedere [Installazione di SQL Server dal prompt dei comandi](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md).  
  
## <a name="next-steps"></a>Passaggi successivi  
 [Aggiornare SQL Server usando l'Installazione guidata &#40;programma di installazione&#41;](../../../database-engine/install-windows/upgrade-sql-server-using-the-installation-wizard-setup.md)   
 [Installare SQL Server dal prompt dei comandi](../../../database-engine/install-windows/install-sql-server-2016-from-the-command-prompt.md)   
 [Eseguire l'aggiornamento di un'istanza del cluster di failover di SQL Server &#40;installazione&#41;](../../../sql-server/failover-clusters/windows/upgrade-a-sql-server-failover-cluster-instance-setup.md)  
  
  
