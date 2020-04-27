---
title: Aggiornare database replicati | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- merge replication database upgrades [SQL Server replication]
- replication [SQL Server], upgrading
- transactional replication, upgrading databases
- snapshot replication [SQL Server], upgrading databases
- upgrading replicated databases
ms.assetid: 9926a4f7-bcd8-4b9b-9dcf-5426a5857116
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a356a6bad7b0756f148b43ed0cbf35e8d2ce9cc9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62775321"
---
# <a name="upgrade-replicated-databases"></a>Aggiornare database replicati
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] supporta l'aggiornamento di database replicati da versioni precedenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] senza che sia necessario, durante l'aggiornamento di un nodo, arrestare le attività negli altri nodi. Verificare che vengano osservate le regole relative alle versioni supportate in una topologia:  
  
-   La versione del server di distribuzione è indifferente, purché superiore o uguale alla versione del server di pubblicazione (in molti casi l'istanza del server di distribuzione è la stessa del server di pubblicazione).  
  
-   La versione del server di pubblicazione è indifferente, purché inferiore o uguale alla versione del server di distribuzione.  
  
-   La versione del Sottoscrittore dipende dal tipo di pubblicazione:  
  
    -   La versione di un Sottoscrittore per una pubblicazione transazionale può essere una versione qualsiasi all'interno di un intervallo di due versioni, in base alla versione del server di pubblicazione. Un server di pubblicazione [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], ad esempio, può disporre di Sottoscrittori [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], mentre un server di pubblicazione [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] può disporre di Sottoscrittori [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
    -   Un Sottoscrittore a una pubblicazione di tipo merge può essere qualsiasi versione inferiore o uguale alla versione del server di pubblicazione.  
  
> [!NOTE]  
>  Questo argomento è disponibile nella Guida del programma di installazione e nella documentazione online di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . I collegamenti visualizzati in grassetto nella Guida del programma di installazione si riferiscono ad argomenti disponibili solo nella documentazione online.  
  
## <a name="run-the-log-reader-agent-for-transactional-replication-before-upgrade"></a>Esecuzione dell'agente di lettura log per la replica transazionale prima dell'aggiornamento  
 Prima di eseguire l'aggiornamento a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], è necessario assicurarsi che tutte le transazioni completate dalle tabelle pubblicate siano state elaborate dall'agente di lettura log. Per assicurarsi che tutte le transazioni siano state elaborate, eseguire i passaggi seguenti per ogni database che contiene pubblicazioni transazionali:  
  
1.  Verificare che l'agente di lettura log sia in esecuzione per il database. Per impostazione predefinita, l'agente viene eseguito in modo continuativo.  
  
2.  Arrestare l'attività dell'utente nelle tabelle pubblicate.  
  
3.  Concedere tempo all'agente di lettura log per copiare transazioni nel database di distribuzione, quindi arrestare l'agente.  
  
4.  Eseguire [sp_replcmds](/sql/relational-databases/system-stored-procedures/sp-replcmds-transact-sql) per verificare che siano state elaborate tutte le transazioni. Il set di risultati restituito da questa procedura deve essere vuoto.  
  
5.  Eseguire [sp_replflush](/sql/relational-databases/system-stored-procedures/sp-replflush-transact-sql) per chiudere la connessione da sp_replcmds.  
  
6.  Eseguire l'aggiornamento del server a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
7.  Riavviare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent e l'agente di lettura log se non vengono avviati automaticamente dopo l'aggiornamento.  
  
## <a name="run-agents-for-merge-replication-after-upgrade"></a>Esecuzione degli agenti per una replica di tipo merge dopo l'aggiornamento  
 Al termine dell'aggiornamento, eseguire l'agente snapshot per ogni pubblicazione di tipo merge e l'agente di merge per ogni sottoscrizione in modo da aggiornare i metadati della replica. Non occorre applicare il nuovo snapshot in quanto non è necessario reinizializzare le sottoscrizioni. I metadati delle sottoscrizioni vengono aggiornati alla prima esecuzione dell'agente di merge successiva all'aggiornamento. Ciò significa che il database di sottoscrizione può rimanere online e attivo durante l'aggiornamento del server di pubblicazione.  
  
 La replica di tipo merge archivia i metadati delle pubblicazioni e delle sottoscrizioni in alcune tabelle di sistema nei database di pubblicazione e sottoscrizione. L'esecuzione dell'agente snapshot aggiorna i metadati delle pubblicazioni e l'esecuzione dell'agente di merge aggiorna i metadati delle sottoscrizioni. È semplicemente richiesta la generazione di uno snapshot di pubblicazione. Se una pubblicazione di tipo merge utilizza filtri con parametri, ogni partizione includerà uno snapshot. Non è necessario aggiornare gli snapshot partizionati.  
  
 Eseguire gli agenti da [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], da Monitoraggio replica o dalla riga di comando. Per ulteriori informazioni sull'esecuzione dell'agente snapshot, vedere gli argomenti seguenti:  
  
-   [Creazione e applicazione dello snapshot iniziale](../../../2014/relational-databases/replication/create-and-apply-the-initial-snapshot.md)  
  
-   [Avviare e arrestare un agente di replica &#40;SQL Server Management Studio&#41;](../../relational-databases/replication/agents/start-and-stop-a-replication-agent-sql-server-management-studio.md)  
  
-   [Creazione e applicazione dello snapshot iniziale](../../../2014/relational-databases/replication/create-and-apply-the-initial-snapshot.md)  
  
-   [Replication Agent Executables Concepts](../../../2014/relational-databases/replication/concepts/replication-agent-executables-concepts.md)  
  
 Per ulteriori informazioni sull'esecuzione dell'agente di merge, vedere gli argomenti seguenti:  
  
-   [Sincronizzare una sottoscrizione pull](../../../2014/relational-databases/replication/synchronize-a-pull-subscription.md)  
  
-   [Sincronizzazione di una sottoscrizione push](../../../2014/relational-databases/replication/synchronize-a-push-subscription.md)  
  
 Al termine dell'aggiornamento di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in una topologia in cui viene utilizzata una replica di tipo merge, modificare il livello di compatibilità di tutte le pubblicazioni se si desidera utilizzare le nuove funzionalità.  
  
## <a name="upgrading-to-standard-workgroup-or-express-editions"></a>Aggiornamento alle versioni Standard, Workgroup o Express  
 Prima di eseguire l'aggiornamento da un'edizione all'altra di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , verificare che le funzionalità utilizzate siano supportate nell'edizione a cui si esegue l'aggiornamento. Per ulteriori informazioni, vedere la sezione sulla replica in [funzionalità supportate dalle edizioni di SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
## <a name="web-synchronization-for-merge-replication"></a>Sincronizzazione Web per la replica di tipo merge  
 L'opzione di sincronizzazione Web per la replica di tipo merge richiede che il listener per la replica di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (replisapi.dll) venga copiato nella directory virtuale nel server Internet Information Services (IIS) utilizzato per la sincronizzazione. Quando si configura la sincronizzazione Web, il file viene copiato nella directory virtuale dalla procedura di configurazione guidata della sincronizzazione Web. Se si aggiornano i componenti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] installati nel server IIS, è necessario copiare manualmente replisapi.dll dalla directory COM alla directory virtuale nel server IIS. Per altre informazioni sulla configurazione della sincronizzazione Web, vedere [Configurazione della sincronizzazione Web](../../../2014/relational-databases/replication/configure-web-synchronization.md).  
  
## <a name="restoring-a-replicated-database-from-an-earlier-version"></a>Ripristino di un database replicato da una versione precedente  
 Per verificare che in seguito al ripristino del backup di un database replicato vengano mantenute le impostazioni di replica di una versione precedente, eseguire il ripristino in un server e un database con gli stessi nomi del server e del database utilizzati per la creazione della copia di backup.  
  
## <a name="see-also"></a>Vedi anche  
 [Domande frequenti sull'amministrazione della replica](../../relational-databases/replication/administration/frequently-asked-questions-for-replication-administrators.md)   
 [Compatibilità con le versioni precedenti della replica](../../../2014/relational-databases/replication/replication-backward-compatibility.md)   
 [Aggiornamenti di versione ed edizione supportati](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)   
 [Aggiornamento a SQL Server 2014](upgrade-sql-server.md)  
  
  
