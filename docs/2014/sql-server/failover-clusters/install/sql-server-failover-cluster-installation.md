---
title: Installazione del cluster di failover di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: c0e75a7c-85c5-423c-a218-77247bf071aa
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 49fce70b4fc01f77fe7ca54e3951f0372ba18489
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63067647"
---
# <a name="sql-server-failover-cluster-installation"></a>Installazione del cluster di failover di SQL Server
  Per installare un cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , è necessario creare e configurare un'istanza del cluster di failover eseguendo il programma di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="installing-a-failover-cluster"></a>Installazione di un cluster di failover  
 Per installare un cluster di failover, è necessario utilizzare un account di dominio con diritti di amministratore locale, nonché disporre dell'autorizzazione per accedere come servizio e per operare come parte del sistema operativo in tutti i nodi del cluster di failover. Per installare un cluster di failover tramite il programma di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , attenersi alla procedura seguente:  
  
1.  Per installare, configurare e gestire un cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , utilizzare il programma di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
    -   Identificare le informazioni necessarie per creare l'istanza del cluster di failover (ad esempio la risorsa disco del cluster, gli indirizzi IP e il nome di rete) e i nodi disponibili per il failover. Per altre informazioni:  
  
        -   [Operazioni preliminari all'installazione del clustering di failover](before-installing-failover-clustering.md)  
  
        -   [Considerazioni sulla sicurezza per un'installazione di SQL Server](../../install/security-considerations-for-a-sql-server-installation.md)  
  
    -   La procedura di configurazione deve essere eseguita prima di eseguire [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] il programma di installazione. utilizzare Amministrazione cluster di Windows per eseguirli. È necessario disporre di un gruppo WSFC per ogni istanza del cluster di failover che si desidera configurare.  
  
    -   È necessario assicurarsi che il sistema soddisfi i requisiti minimi. Per altre informazioni sui requisiti specifici per un cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , vedere [Operazioni preliminari all'installazione del clustering di failover](before-installing-failover-clustering.md).  
  
2.  Aggiungere o rimuovere nodi da una configurazione del cluster di failover senza influire sugli altri nodi del cluster. Per altre informazioni, vedere [Aggiungere o rimuovere nodi in un cluster di failover di SQL Server &#40;programma di installazione&#41;](add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
    -   In tutti i nodi di un cluster di failover deve essere utilizzata la stessa piattaforma, a 32 o a 64 bit, e l'edizione e la versione del sistema operativo eseguite devono essere uguali. È inoltre necessario installare le versioni a 64 bit di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in computer a 64 bit che eseguono versioni a 64 bit dei sistemi operativi Windows. Non è disponibile alcun supporto WOW64 per il clustering di failover in questa versione.  
  
3.  Specificare più indirizzi IP per ogni istanza del cluster di failover. È possibile specificare più indirizzi IP per ogni subnet. Se i diversi indirizzi IP si trovano nella stessa subnet, il programma di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] consente di impostare la dipendenza su AND. Se si sta eseguendo il clustering di nodi in più subnet, il programma di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] consente di impostare la dipendenza su OR.  
  
## <a name="includessnoversionincludesssnoversion-mdmd-failover-cluster-installation-options"></a>
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Opzioni di installazione del cluster di failover  
  
##### <a name="option-1-integrated-installation-with-add-node"></a>Opzione 1: installazione integrata con la funzionalità per l'aggiunta del nodo  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] è costituita da due passaggi:  
  
1.  Creazione e configurazione di un'istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a nodo singolo. Dopo il completamento di una configurazione del nodo, è disponibile un'istanza del cluster di failover in grado di funzionare correttamente, ma senza disponibilità elevata poiché nel cluster di failover è presente solo un nodo.  
  
2.  In ogni nodo da aggiungere al cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , eseguire il programma di installazione per aggiungere il nodo specifico con la funzionalità relativa.  
  
##### <a name="option-2-advancedenterprise-installation"></a>Opzione 2: installazione avanzata o aziendale  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] L'installazione avanzata o aziendale del cluster di failover prevede due passaggi:  
  
1.  In ogni nodo che apparterrà al cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] eseguire il programma di installazione con la funzionalità per la preparazione del cluster di failover. Questo passaggio prepara i nodi per l'inserimento nel cluster, ma al termine del passaggio non è ancora presente alcuna istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] operativa.  
  
2.  Dopo che i nodi sono stati preparati per il clustering, eseguire il programma di installazione nel nodo proprietario del disco condiviso con la funzionalità per il completamento del cluster di failover. In questo passaggio l'istanza del cluster di failover viene creata e configurata e al termine del passaggio sarà disponibile un'istanza del cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] operativa.  
  
    > [!NOTE]  
    >  Entrambe le opzioni consentono l'installazione di un cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] a nodi multipli. La funzionalità per l'aggiunta del nodo può essere utilizzata per aggiungere altri nodi per entrambe le opzioni dopo la creazione di un cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
    > [!IMPORTANT]  
    >  La lettera di unità del sistema operativo per i percorsi di installazione di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve corrispondere per tutti i nodi aggiunti al cluster di failover di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
#### <a name="ip-address-configuration-during-setup"></a>Configurazione dell'indirizzo IP durante l'installazione  
 
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] consente di impostare o modificare le impostazioni della dipendenza delle risorse IP durante le azioni seguenti:  
  
-   Installazione integrata: [Creare un nuovo cluster di failover di SQL Server &#40;programma di installazione&#41;](create-a-new-sql-server-failover-cluster-setup.md)  
  
-   CompleteFailoverCluster (installazione avanzata): [Creare un nuovo cluster di failover di SQL Server &#40;programma di installazione&#41;](create-a-new-sql-server-failover-cluster-setup.md)  
  
-   Aggiunta di un nodo: [Aggiungere o rimuovere nodi in un cluster di failover di SQL Server &#40;programma di installazione&#41;](add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)  
  
-   Rimozione di un nodo: [Aggiungere o rimuovere nodi in un cluster di failover di SQL Server &#40;programma di installazione&#41;](add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md)  
  
 **Nota** Gli indirizzi IP IPV6 sono supportati.  Se configurati entrambi, gli indirizzi IPv4 e IPv6 vengono trattati come subnet diverse e IPv6 viene portato online per primo.  
  
##### <a name="includessnoversionincludesssnoversion-mdmd-multi-subnet-failover-cluster"></a>
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Cluster di failover su più subnet  
 È possibile impostare le dipendenze OR quando i nodi del cluster si trovano in subnet diverse. Tuttavia, ogni nodo del cluster di failover su più subnet di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] deve essere un possibile proprietario di almeno uno degli indirizzi IP specificati.  
  
## <a name="see-also"></a>Vedere anche  
 [Prima di installare il clustering di failover](before-installing-failover-clustering.md)   
 [Creare un nuovo cluster di failover di SQL Server &#40;installazione&#41;](create-a-new-sql-server-failover-cluster-setup.md)   
 [Installare SQL Server 2014 dal prompt dei comandi](../../../database-engine/install-windows/install-sql-server-from-the-command-prompt.md)   
 [Aggiornare un cluster di failover di SQL Server](../windows/upgrade-a-sql-server-failover-cluster-instance.md)  
  
  
