---
title: Finestra di dialogo Proprietà server di distribuzione di replica di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 11/20/2018
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.configdistwizard.distdbproperties.f1
- sql13.rep.configdistwizard.distproperties.general.f1
- sql13.rep.configdistwizard.distproperties.publishers.f1
ms.assetid: f643c7c3-f238-4835-b81e-2c2b3b53b23f
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3e542e49811ed7f57a9b60dbf1f0428f69706bdb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68128305"
---
# <a name="sql-server-replication-distributor-properties-dialog-box"></a>Finestra di dialogo Proprietà server di distribuzione di replica di SQL Server 
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Questa pagina descrive le pagine disponibili nella finestra di dialogo Proprietà server di distribuzione. 

## <a name="general"></a>Generale
La pagina **Generale** della finestra di dialogo **Proprietà server di distribuzione** consente di aggiungere ed eliminare i database di distribuzione e di impostarne le relative proprietà.  
  
 Nel database di distribuzione vengono archiviati i metadati e i dati di cronologia relativi a tutti i tipi di replica, nonché le transazioni per la replica transazionale. In molti casi, è sufficiente un singolo database di distribuzione. Se tuttavia un singolo server di distribuzione viene utilizzato da più server di pubblicazione, è opportuno creare un database di distribuzione per ogni server di pubblicazione, in modo da garantire che il flusso di dati di ogni database di distribuzione risulti distinto.  

 **Database**  
 Nella griglia delle proprietà **Database** vengono visualizzati il nome e le proprietà di memorizzazione dei database di distribuzione nel server di distribuzione. **Periodo memorizzazione transazioni** rappresenta il periodo di tempo per cui le transazioni rimangono archiviate per la replica transazionale. Il periodo di memorizzazione della transazione è inoltre noto come periodo di memorizzazione per la distribuzione. **Periodo memorizzazione cronologia** equivale invece al periodo di tempo per cui rimangono archiviati i metadati della cronologia per ogni tipo di replica. Per altre informazioni sul periodo di memorizzazione, vedere [Scadenza e disattivazione delle sottoscrizioni](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
 Fare clic sul pulsante delle proprietà **...** nella griglia delle proprietà **Database** per aprire la finestra di dialogo **Proprietà database di distribuzione** .  
  
 **Nuova**  
 Fare clic su questo pulsante per creare un nuovo database di distribuzione.  
  
 **Elimina**  
 Selezionare un database di distribuzione esistente nella griglia delle proprietà **Database** e scegliere **Elimina** per eliminarlo. Non è possibile eliminare il database di distribuzione se ne esiste uno solo, poiché ogni server di distribuzione deve disporre di almeno un database di distribuzione. Per eliminare tutti i database di distribuzione, è necessario disabilitare la distribuzione nel computer. Per altre informazioni, vedere [Disabilitare la pubblicazione e la distribuzione](../../relational-databases/replication/disable-publishing-and-distribution.md).  
  
 **Impostazioni predefinite profili**  
 Fare clic su questo pulsante per accedere ai profili dell'agente di replica nella finestra di dialogo **Profili agenti** . Per ulteriori informazioni sui profili, vedere [Replication Agent Profiles](../../relational-databases/replication/agents/replication-agent-profiles.md).  

## <a name="publishers"></a>Server di pubblicazione
La pagina **Server di pubblicazione** della finestra di dialogo **Proprietà server di distribuzione** consente di abilitare l'utilizzo del server di distribuzione corrente da parte dei server di pubblicazione. È inoltre possibile impostare le proprietà associate a tali server di pubblicazione. Tenere presente che, se si abilita un server di pubblicazione per l'utilizzo di questo server come server di distribuzione remoto, il server non diventerà un server di pubblicazione. È infatti necessario connettersi al server di pubblicazione, configurarlo per la pubblicazione e selezionare questo server come server di distribuzione. Utilizzando la Creazione guidata nuova pubblicazione è possibile configurare il server di pubblicazione e selezionare un server di distribuzione.  
  
 **Server di pubblicazione**  
 Consente di selezionare i server autorizzati all'utilizzo del server di distribuzione corrente. Per visualizzare e impostare proprietà aggiuntive fare clic sul pulsante delle proprietà ( **...** ) accanto a un server di pubblicazione.  
  
 **Aggiungi**  
 Se il server desiderato non è incluso nell'elenco, fare clic su **Aggiungi** per aggiungere un server di pubblicazione [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o Oracle all'elenco dei server di pubblicazione disponibili. Se il server aggiunto è il primo server a utilizzare il server di distribuzione corrente come server di distribuzione remoto, viene richiesto di digitare una password per il collegamento amministrativo.  
  
 **Password per collegamento amministrativo**  
 Utilizzare questa opzione per specificare o aggiornare la password per la connessione che la replica stabilisce tra il server di pubblicazione e il server di distribuzione remoto utilizzando l'account di accesso **distributor_admin** :  
  
-   Se il server di distribuzione viene utilizzato solo come server di distribuzione locale, tale password viene generata in modo casuale e viene configurata automaticamente.   
-   Se il server di distribuzione viene utilizzato già da un server di pubblicazione remoto, una password è stata specificata inizialmente in questa pagina o nella pagina **Password server di distribuzione** della Configurazione guidata distribuzione.    
-   Se si tratta del primo server di pubblicazione abilitato per il server di distribuzione corrente viene richiesto di digitare una password.  Per altre informazioni sulla sicurezza dei database di distribuzione, vedere [Proteggere il database di distribuzione](../../relational-databases/replication/security/secure-the-distributor.md).  

## <a name="distribution-database"></a>Database di distribuzione 
 La finestra di dialogo **Proprietà database di distribuzione** consente di visualizzare varie proprietà e di impostare il periodo di memorizzazione della transazione e della cronologia per il database.  
  
 **Nome**  
 Il nome del database di distribuzione, il cui valore predefinito è "distribution" (sola lettura).  
  
 **Percorsi dei file**  
 Il percorso del file di database e del file di log (sola lettura).  
  
 **Periodo di memorizzazione della transazione**  
 Questa proprietà è nota anche come periodo di memorizzazione della distribuzione. Si tratta della quantità di tempo di memorizzazione delle transazioni ai fini della replica transazionale. Per altre informazioni, vedere [Subscription Expiration and Deactivation](../../relational-databases/replication/subscription-expiration-and-deactivation.md).  
  
 **Periodo di memorizzazione cronologia**  
 Quantità di tempo di memorizzazione dei metadati della cronologia ai fini di tutti i tipi di replica.  
  
 **Sicurezza agente di lettura coda**  
 L'agente di lettura coda viene utilizzato dalla replica transazionale con sottoscrizioni ad aggiornamento in coda. L'agente di lettura coda viene creato automaticamente se si seleziona **Creazione di una pubblicazione transazionale con aggiornamento delle sottoscrizioni** nella pagina **Tipo di pubblicazione** della Creazione guidata nuova pubblicazione. Fare clic su **Impostazioni di sicurezza** per modificare l'account nell'ambito del quale l'agente viene eseguito e si connette al server di distribuzione.  
  
 In questa pagina è inoltre possibile creare un agente di lettura coda selezionando **Crea agente di lettura coda** . L'opzione è disabilitata se l'agente è già stato creato.  
  
 Ulteriori informazioni sulla connessione relative all'agente di lettura coda vengono specificate in due posizioni:    
-   L'agente si connette al server di pubblicazione mediante le credenziali specificate nella finestra di dialogo **Proprietà server di pubblicazione** che è disponibile nella pagina **Server di pubblicazione** della finestra di dialogo **Proprietà server di distribuzione** .    
-   L'agente si connette al Sottoscrittore mediante le credenziali specificate per l'agente di distribuzione in Creazione guidata nuova sottoscrizione.  Per altre informazioni, vedere  [Replication Agent Security Model](../../relational-databases/replication/security/replication-agent-security-model.md). 
  
## <a name="see-also"></a>Vedere anche  
 [Configura distribuzione](../../relational-databases/replication/configure-distribution.md)   
 [Visualizzare e modificare le proprietà del server di pubblicazione e del database di distribuzione](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
  
  
