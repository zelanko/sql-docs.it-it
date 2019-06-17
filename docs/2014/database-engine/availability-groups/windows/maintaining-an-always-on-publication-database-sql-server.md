---
title: Gestione di un Database di pubblicazione AlwaysOn (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- Availability Groups [SQL Server], interoperability
- replication [SQL Server], AlwaysOn Availability Groups
ms.assetid: 55b345fe-2eb9-4b04-a900-63d858eec360
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a862c5c9cea1087f54a4dbff13b6c39eb5e39385
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62791989"
---
# <a name="maintaining-an-alwayson-publication-database-sql-server"></a>Gestione di un database di pubblicazione AlwaysOn (SQL Server)
  In questo argomento verranno illustrate alcune considerazioni speciali per la gestione di un database di pubblicazione quando si utilizzano gruppi di disponibilità AlwaysOn.  
  
 
  
##  <a name="MaintainPublDb"></a> Gestione di un database di pubblicazione in un gruppo di disponibilità  
 La gestione di un database di pubblicazione AlwaysOn è sostanzialmente analoga a quella di un database di pubblicazione standard, con le considerazioni seguenti:  
  
-   L'amministrazione deve avvenire nell'host della replica primaria. In [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]le pubblicazioni vengono visualizzate nella cartella **Pubblicazioni locali** per l'host della replica primaria e per le repliche secondarie leggibili. Dopo il failover potrebbe essere necessario aggiornare manualmente [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] per riflettere la modifica se la replica secondaria promossa a primaria non era leggibile.  
  
-   In Monitoraggio replica le informazioni sulla pubblicazione vengono sempre visualizzate nel server di pubblicazione originale. Queste informazioni possono tuttavia essere visualizzate in Monitoraggio replica da qualsiasi replica aggiungendo il server di pubblicazione originale come server.  
  
-   Se l'amministrazione viene effettuata nella replica primaria corrente mediante oggetti RMO (Replication Management Objects) o stored procedure, nei casi in cui si specifica il nome del server di pubblicazione è necessario specificare il nome dell'istanza in cui il database è stato abilitato per la replica, ovvero il server di pubblicazione originale. Per determinare il nome appropriato, utilizzare la funzione `PUBLISHINGSERVERNAME`. Quando un database di pubblicazione viene unito in join a un gruppo di disponibilità, i metadati di replica archiviati nelle repliche di database secondarie sono identici a quelli della replica primaria. Ne consegue che, per i database di pubblicazione abilitati per la replica nel database primario, il nome dell'istanza del server di pubblicazione archiviato in tabelle di sistema nel database secondario equivale al nome del database primario e non a quello del database secondario. Ciò influisce sulla manutenzione e sulla configurazione della replica se viene eseguito il failover del database di pubblicazione su un database secondario. Ad esempio, se si configura la replica con stored procedure in un database secondario dopo il failover e si vuole usare una sottoscrizione pull a un database di pubblicazione abilitato in una replica diversa, è necessario specificare il nome del server di pubblicazione originale anziché di server di pubblicazione corrente come il *@publisher* parametro `sp_addpullsubscription` o `sp_addmergepulllsubscription`. Se tuttavia si abilita un database di pubblicazione dopo il failover, il nome dell'istanza del server di pubblicazione archiviato nelle tabelle di sistema corrisponde al nome dell'host primario corrente. In questo caso si utilizzerà il nome host della replica primaria corrente per il parametro *@publisher* .  
  
    > [!NOTE]  
    >  Per alcune procedure, ad esempio `sp_addpublication`, il *@publisher* parametro è supportato solo per i server di pubblicazione che non sono istanze di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]; in questi casi, non è rilevante per [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] AlwaysOn.  
  
-   Per sincronizzare una sottoscrizione in [!INCLUDE[ssManStudio](../../../includes/ssmanstudio-md.md)] dopo un failover, sincronizzare le sottoscrizioni pull dal Sottoscrittore e le sottoscrizioni push dal server di pubblicazione attivo.  
  
##  <a name="RemovePublDb"></a> Rimozione di un database di pubblicazione da un gruppo di disponibilità  
 Considerare i problemi seguenti se un database pubblicato viene rimosso da un gruppo di disponibilità o se un gruppo di disponibilità che dispone di un database del membro pubblicato viene eliminato.  
  
-   Se il database di pubblicazione nel server di pubblicazione originale viene rimosso da una replica primaria del gruppo di disponibilità, è necessario eseguire `sp_redirect_publisher` senza specificare un valore per il *@redirected_publisher* parametro allo scopo di rimuovere il reindirizzamento per la coppia server di pubblicazione/database.  
  
    ```  
    EXEC sys.sp_redirect_publisher   
        @original_publisher = 'MyPublisher',  
        @published_database = 'MyPublishedDB';  
    ```  
  
     Il database rimarrà nello stato di recupero nella replica primaria e dovrà essere ripristinato. Una volta effettuata questa operazione, la replica dovrebbe funzionare invariata rispetto al server di pubblicazione originale.  
  
-   Nel caso di failover del database di pubblicazione dal server di pubblicazione originale su una replica e se il database viene rimosso dalla replica primaria del gruppo di disponibilità, utilizzare la stored procedure `sp_redirect_publisher` per reindirizzare in modo esplicito il server di pubblicazione originale al nuovo server di pubblicazione. Il database rimarrà nello stato di recupero e dovrà essere ripristinato. Una volta effettuata questa operazione, la replica dovrebbe continuare a funzionare come nel gruppo di disponibilità.  
  
    ```  
    EXEC sys.sp_redirect_publisher   
        @original_publisher = 'MyPublisher',  
        @published_database = 'MyPublishedDB',  
        @redirected_publisher = 'MyNewPublisher';  
    ```  
  
     Non rimuovere il server remoto per il server di pubblicazione originale dal distributore, anche se non è più possibile accedere al server. I metadati del server per il server di pubblicazione originale sono necessari nel distributore per rispondere alle query sui metadati di pubblicazione.  
  
-   Se viene rimosso un gruppo di disponibilità completo, il comportamento di un database replicato membro è lo stesso di un database pubblicato rimosso da un gruppo di disponibilità. È possibile riprendere la replica dall'ultima replica primaria non appena viene ripristinato il database e modificato il reindirizzamento. Se il database viene ripristinato nel server di pubblicazione originale, il reindirizzamento deve essere rimosso. Se il database viene ripristinato in un host diverso, il reindirizzamento deve essere effettuato in modo esplicito al nuovo host.  
  
    > [!NOTE]  
    >  Quando viene rimosso un gruppo di disponibilità contenente database membro pubblicati o viene rimosso un database pubblicato da un gruppo di disponibilità, tutte le copie dei database pubblicati rimarranno nello stato di recupero. Se ripristinati, saranno tutti visualizzati come database pubblicato. Sarà necessario mantenere una sola copia con i metadati di pubblicazione. Per disabilitare la replica per una copia del database pubblicato, è necessario prima rimuovere tutte le sottoscrizioni e le pubblicazioni dal database.  
  
     Eseguire `sp_dropsubscription` per rimuovere le sottoscrizioni della pubblicazione. Accertarsi di impostare il parametro *@ignore_distributributor* su 1 per mantenere i metadati per il database di pubblicazione attivo nel server di distribuzione.  
  
    ```  
    USE MyDBName;  
    GO  
  
    EXEC sys.sp_dropsubscription   
        @subscriber = 'MySubscriber',  
        @publication = 'MyPublication',  
        @article = 'all',  
        @ignore_distributor = 1;  
    ```  
  
     Eseguire `sp_droppublication` per rimuovere tutte le pubblicazioni. Impostare di nuovo il parametro *@ignore_distributor* su 1 per mantenere i metadati per il database di pubblicazione attivo nel server di distribuzione.  
  
    ```  
    EXEC sys.sp_droppublication   
        @publication = 'MyPublication',  
        @ignore_distributor = 1;  
    ```  
  
     Eseguire `sp_replicationdboption` per disabilitare replica per il database.  
  
    ```  
    EXEC sys.sp_replicationdboption  
        @dbname = 'MyDBName',  
        @optname = 'publish',  
        @value = 'false';  
    ```  
  
     A questo punto la copia del database pubblicato può essere mantenuta o eliminata.  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
-   [Configurare la replica per i gruppi di disponibilità AlwaysOn (SQL Server)](always-on-availability-groups-sql-server.md)  
  
-   [La replica, rilevamento delle modifiche, Change Data Capture e gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](replicate-track-change-data-capture-always-on-availability.md)  
  
-   [Domande frequenti sull'amministrazione della replica](../../../relational-databases/replication/administration/frequently-asked-questions-for-replication-administrators.md)  
  
-   [Sottoscrittori della replica e gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](replication-subscribers-and-always-on-availability-groups-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Prerequisiti, restrizioni e consigli per gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Gruppi di disponibilità AlwaysOn: Interoperabilità (SQL Server)](always-on-availability-groups-interoperability-sql-server.md)   
 [Replica di SQL Server](../../../relational-databases/replication/sql-server-replication.md)  
  
  
