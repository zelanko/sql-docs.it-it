---
title: Usare la procedura guidata Aggiungi replica a gruppo di disponibilità (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.addreplicawizard.f1
helpviewer_keywords:
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], wizards
ms.assetid: 60d962b6-2af4-4394-9190-61939a102bc0
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7a9074c49b3e8c9d80666d3bb586ffeba225e88b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62813378"
---
# <a name="use-the-add-replica-to-availability-group-wizard-sql-server-management-studio"></a>Utilizzare la procedura guidata Aggiungi replica a gruppo di disponibilità (SQL Server Management Studio)
  Utilizzare la procedura guidata Aggiungi replica a gruppo di disponibilità per aggiungere una nuova replica secondaria a un gruppo di disponibilità AlwaysOn esistente.  
  
> [!NOTE]  
>  Per altre informazioni sull'uso di [!INCLUDE[tsql](../../../includes/tsql-md.md)] o di PowerShell per aggiungere una replica secondaria a un gruppo di disponibilità, vedere [Aggiungere una replica secondaria a un gruppo di disponibilità &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md).  
  

  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
 Se non è mai stata aggiunta una replica di disponibilità a un gruppo di disponibilità, vedere le sezioni "istanze del server" e "repliche e gruppi di disponibilità" in [prerequisiti, restrizioni e consigli per Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).  
  
###  <a name="Prerequisites"></a> Prerequisiti  
  
-   È necessario essere connessi all'istanza del server che ospita la replica primaria corrente.  
  
-   Prima di aggiungere una replica secondaria, verificare che l'istanza ospite di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] si trovi nello stesso cluster Windows Server Failover Clustering (WSFC) delle repliche esistenti, ma risieda in un nodo del cluster diverso. Inoltre, verificare che questa istanza del server soddisfi tutti gli altri prerequisiti di [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] . Per ulteriori informazioni, vedere [prerequisiti, restrizioni e consigli per Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).  
  
-   Se un'istanza del server selezionata come host per una replica di disponibilità è in esecuzione in un account utente di dominio e non dispone ancora di un endpoint del mirroring del database, tramite la procedura guidata è possibile creare l'endpoint e concedere l'autorizzazione CONNECT all'account del servizio dell'istanza del server. Se, tuttavia, il servizio [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] viene eseguito come account predefinito, ad esempio Sistema locale, Servizio locale o Servizio di rete, oppure come account non di dominio, è necessario usare certificati per l'autenticazione dell'endpoint e non sarà possibile creare un endpoint del mirroring del database nell'istanza del server tramite la procedura guidata. In tal caso, è consigliabile creare manualmente gli endpoint del mirroring del database prima di avviare la Procedura guidata Aggiungi replica a gruppo di disponibilità.  
  
     `To use certificates for a database mirroring endpoint:`  
  
     [CREATE ENDPOINT &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-endpoint-transact-sql)  
  
     [Utilizzare certificati per un endpoint del mirroring del database &#40;Transact-SQL&#41;](../../database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)  
  
-   **Prerequisiti per l'utilizzo della sincronizzazione dati iniziale completa**  
  
    -   Tutti i percorsi di file dei database devono essere identici in ogni istanza del server in cui è ospitata una replica per il gruppo di disponibilità.  
  
    -   In un'istanza del server in cui è ospitata una replica secondaria non può essere presente alcun nome di database primario. Ciò significa che non può essere ancora presente alcun nuovo database secondario.  
  
    -   Sarà necessario specificare una condivisione di rete affinché la procedura guidata sia in grado di creare e accedere ai backup. Per la replica primaria, all'account usato per avviare il [!INCLUDE[ssDE](../../../includes/ssde-md.md)] devono essere associate le autorizzazioni del file system in lettura e scrittura per una condivisione di rete. Per le repliche secondarie, all'account deve essere associata l'autorizzazione di lettura per la condivisione di rete.  
  
     Se non è possibile usare la procedura guidata per eseguire la sincronizzazione dei dati iniziale completa, sarà necessario preparare i database secondari manualmente. Tale operazione può essere eseguita prima o dopo l'esecuzione della procedura guidata. Per altre informazioni, vedere [Preparare manualmente un database secondario per un gruppo di disponibilità &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md).  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 È necessaria l'autorizzazione ALTER AVAILABILITY GROUP nel gruppo di disponibilità, l'autorizzazione CONTROL AVAILABILITY GROUP, l'autorizzazione ALTER ANY AVAILABILITY GROUP o l'autorizzazione CONTROL SERVER.  
  
 È inoltre necessaria l'autorizzazione CONTROL ON ENDPOINT se si desidera gestire l'endpoint del mirroring del database tramite la Procedura guidata Aggiungi replica a gruppo di disponibilità.  
  

  
##  <a name="SSMSProcedure"></a> Utilizzo della procedura guidata Aggiungi replica a gruppo di disponibilità (SQL Server Management Studio)  
 **Per utilizzare la procedura guidata Aggiungi replica a gruppo di disponibilità**  
  
1.  In Esplora oggetti connettersi all'istanza del server che ospita la replica primaria del gruppo di disponibilità ed espandere l'albero del server.  
  
2.  Espandere il nodo **Disponibilità elevata AlwaysOn** e il nodo **Gruppi di disponibilità** .  
  
3.  Fare clic con il pulsante destro del mouse sul gruppo di disponibilità a cui si aggiunge una replica secondaria e scegliere il comando **Aggiungi replica** . Verrà avviata la procedura guidata Aggiungi replica a gruppo di disponibilità.  
  
4.  Nella pagina **Connetti a repliche secondarie esistenti** , connettersi a ogni replica secondaria del gruppo di disponibilità. Per ulteriori informazioni, vedere la [pagina connessione a repliche secondarie esistenti &#40;aggiunta guidata replica e aggiunta guidata database&#41;](connect-to-existing-secondary-replicas-page.md).  
  
5.  Nella pagina **Specifica repliche** specificare e configurare una o più nuove repliche secondarie per il nuovo gruppo di disponibilità. In questa pagina sono incluse tre schede. Queste schede vengono presentate nella tabella seguente. Per altre informazioni, vedere [ &#40;Creazione guidata Gruppo di disponibilità: Aggiungi replica&#41;](specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md).  
  
    |Scheda|Breve descrizione|  
    |---------|-----------------------|  
    |**Repliche**|Utilizzare questa scheda per specificare ogni istanza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] che ospiterà una nuova replica secondaria.|  
    |**Endpoints**|Utilizzare questa scheda per verificare l'endpoint del mirroring di database esistente, se presente, per ogni nuova replica secondaria. Se tale endpoint risulta mancante in un'istanza del server i cui account del servizio utilizzano l'autenticazione di Windows, si tenterà di creare l'endpoint automaticamente. **Nota:**  Se un'istanza del server è in esecuzione con un account utente non di dominio, è necessario apportare una modifica manuale all'istanza del server prima di poter continuare con la procedura guidata. Per altre informazioni, vedere la sessione [Prerequisiti](#Prerequisites)più indietro in questo argomento.|  
    |**Preferenze di backup**|Utilizzare questa scheda per specificare le preferenze di backup per il gruppo di disponibilità nel suo complesso, se si desidera modificare l'impostazione corrente e per specificare le priorità di backup per le singole repliche di disponibilità.|  
  
6.  Nella pagina **Seleziona sincronizzazione dei dati iniziale** specificare come creare e aggiungere i nuovi database secondari al gruppo di disponibilità. Scegliere una delle opzioni seguenti:  
  
    -   **Completo**  
  
         Selezionare questa opzione se l'ambiente soddisfa i requisiti per l'avvio automatico della sincronizzazione dei dati iniziale. Per altre informazioni, vedere [Prerequisiti, restrizioni e raccomandazioni](#Prerequisites), più indietro in questo argomento.  
  
         Se si seleziona **Completo**, dopo avere creato il gruppo di disponibilità verrà eseguito il backup di ogni database primario e del relativo log delle transazioni su una condivisione di rete e verranno ripristinati i backup su ogni istanza del server in cui è ospitata una nuova replica secondaria. Per ogni nuovo database secondario verrà quindi creato un join al gruppo di disponibilità.  
  
         Nel campo **Specificare un percorso di rete condiviso accessibile da tutte le repliche:** specificare una condivisione di backup a cui possano accedere in lettura e scrittura tutte le istanze del server che ospitano repliche. I backup del log faranno parte della catena di backup del log. Archiviare i file di backup del log in modo appropriato.  
  
        > [!IMPORTANT]  
        >  Per informazioni sulle autorizzazioni del file system necessarie, vedere [Prerequisiti](#Prerequisites)più indietro in questo argomento.  
  
    -   **Solo join**  
  
         Se sono stati preparati manualmente database secondari sulle istanze del server che ospiteranno le nuove repliche secondarie, è possibile selezionare questa opzione. Per i nuovi database secondari esistenti verranno creati join al gruppo di disponibilità tramite la procedura guidata.  
  
    -   **Ignora sincronizzazione dati iniziale**  
  
         Selezionare questa opzione se si desidera usare i backup dei database e del log dei database primari. Per altre informazioni, vedere [Avviare lo spostamento dati su un database secondario AlwaysOn &#40;SQL Server&#41;](start-data-movement-on-an-always-on-secondary-database-sql-server.md).  
  
7.  Nella pagina **Convalida** viene verificato se i valori specificati in questa procedura guidata soddisfano i requisiti della procedura guidata Aggiungi replica a Gruppo di disponibilità. Per apportare una modifica, fare clic su **Precedente** per tornare a una pagina precedente della procedura guidata per modificare uno o più valori. Scegliere **Avanti** per tornare alla pagina **Convalida**, quindi fare clic su **Ripeti convalida**.  
  
8.  Nella pagina **Riepilogo** rivedere le scelte effettuate per il nuovo gruppo di disponibilità. Per apportare una modifica, fare clic su **Indietro** per tornare alla pagina pertinente. Dopo avere apportato la modifica, fare clic su **Avanti** per tornare alla pagina **Riepilogo** .  
  
     Se si è soddisfatti delle selezioni, è possibile fare clic su Script per creare uno script dei passaggi eseguiti dalla procedura guidata. Per creare e configurare il nuovo gruppo di disponibilità, fare quindi clic su **Fine**.  
  
9. La pagina **Stato** visualizza lo stato di avanzamento dei passaggi per la creazione del gruppo di disponibilità, ovvero configurazione di endpoint, creazione del gruppo di disponibilità e creazione di un join della replica secondaria al gruppo.  
  
10. Al termine di questi passaggi, nella pagina **Risultati** vengono visualizzati i relativi risultati. Se tutti questi passaggi sono stati eseguiti correttamente, il nuovo gruppo di disponibilità è completamente configurato. Se si verifica un errore durante uno dei passaggi, potrebbe essere necessario completare manualmente la configurazione. Per informazioni sulla causa di un determinato errore, fare clic sul collegamento "Errore" nella colonna **Risultato** .  
  
     Al termine della procedura guidata, fare clic su **Chiudi** per uscire.  
  
> [!IMPORTANT]  
>  Dopo avere aggiunto una replica, vedere la sezione "Completamento: Dopo l'aggiunta di una replica secondaria" in [Aggiungere una replica secondaria a un gruppo di disponibilità &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md).  
  

  
##  <a name="RelatedTasks"></a> Attività correlate  
  
-   [Aggiungere una replica secondaria a un gruppo di disponibilità &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  

  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Prerequisiti, restrizioni e consigli per Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [Aggiungere una replica secondaria a un gruppo di disponibilità &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
  
