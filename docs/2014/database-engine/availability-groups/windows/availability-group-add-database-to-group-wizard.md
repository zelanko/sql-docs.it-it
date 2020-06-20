---
title: Utilizzare la procedura guidata Aggiungi database a gruppo di disponibilità (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.adddatabasewizard.f1
helpviewer_keywords:
- Availability Groups [SQL Server], wizards
- Availability Groups [SQL Server], databases
ms.assetid: 81e5e36d-735d-4731-8017-2654673abb88
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 02cd05baa6da57de6f90099d788d582821492d55
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84937154"
---
# <a name="use-the-add-database-to-availability-group-wizard-sql-server-management-studio"></a>Utilizzare la procedura guidata Aggiungi database a gruppo di disponibilità (SQL Server Management Studio)
  Utilizzare la procedura guidata Aggiungi database a gruppo di disponibilità per aggiungere uno o più database a un gruppo di disponibilità AlwaysOn esistente.  
  
> [!NOTE]  
>  Per informazioni sull'uso di [!INCLUDE[tsql](../../../includes/tsql-md.md)] o PowerShell per aggiungere un database, vedere [Aggiungere un database a un gruppo di disponibilità &#40;SQL Server&#41;](availability-group-add-a-database.md).  
  
 **Contenuto dell'argomento:**  
  
-   **Prima di iniziare:**  
  
     [Prerequisiti e restrizioni](#Prerequisites)  
  
     [Sicurezza](#Security)  
  
-   **Per aggiungere un database usando**  [Procedura guidata Aggiungi database a gruppo di disponibilità (SQL Server Management Studio)](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Prima di iniziare  
 Se non è mai stato aggiunto un database a un gruppo di disponibilità, vedere la sezione "database di disponibilità" in [prerequisiti, restrizioni e consigli per Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).  
  
###  <a name="prerequisites-restrictions-and-recommendations"></a><a name="Prerequisites"></a>Prerequisiti, restrizioni e raccomandazioni  
  
-   È necessario essere connessi all'istanza del server che ospita la replica primaria corrente.  
  
-   Se un database viene crittografato o contiene una chiave di crittografia del database (DEK), non è possibile usare [!INCLUDE[ssAoNewAgWiz](../../../includes/ssaonewagwiz-md.md)] o [!INCLUDE[ssAoAddDbWiz](../../../includes/ssaoadddbwiz-md.md)] per aggiungere il database a un gruppo di disponibilità. Anche se è stato decrittografato un database crittografato, i backup del log potrebbero contenere dati crittografati. In questo caso, la sincronizzazione dei dati iniziale completa potrebbe non riuscire sul database. Questo avviene perché l'operazione di ripristino del log potrebbe richiedere il certificato usato dalle chiavi di crittografia del database e tale certificato potrebbe non essere disponibile.  
  
     **Affinché un database decrittografato sia idoneo a essere aggiunto a un gruppo di disponibilità usando la procedura guidata:**  
  
    1.  Creare un backup del log del database primario.  
  
    2.  Creare un backup del log completo del database primario.  
  
    3.  Ripristinare il backup del database nell'istanza del server in cui è ospitata la replica secondaria.  
  
    4.  Creare un nuovo backup del log dal database primario.  
  
    5.  Ripristinare questo backup del log sul database secondario.  
  
-   **Prerequisiti per l'utilizzo della sincronizzazione dati iniziale completa**  
  
    -   Tutti i percorsi di file dei database devono essere identici in ogni istanza del server in cui è ospitata una replica per il gruppo di disponibilità.  
  
    -   In un'istanza del server in cui è ospitata una replica secondaria non può essere presente alcun nome di database primario. Ciò significa che non può essere ancora presente alcun nuovo database secondario.  
  
    -   Sarà necessario specificare una condivisione di rete affinché la procedura guidata sia in grado di creare e accedere ai backup. Per la replica primaria, all'account usato per avviare il [!INCLUDE[ssDE](../../../includes/ssde-md.md)] devono essere associate le autorizzazioni del file system in lettura e scrittura per una condivisione di rete. Per le repliche secondarie, all'account deve essere associata l'autorizzazione di lettura per la condivisione di rete.  
  
     Se non è possibile usare la procedura guidata per eseguire la sincronizzazione dei dati iniziale completa, sarà necessario preparare i database secondari manualmente. Tale operazione può essere eseguita prima o dopo l'esecuzione della procedura guidata. Per altre informazioni, vedere [Preparare manualmente un database secondario per un gruppo di disponibilità &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md).  
  
###  <a name="security"></a><a name="Security"></a> Sicurezza  
  
####  <a name="permissions"></a><a name="Permissions"></a> Autorizzazioni  
 È necessaria l'autorizzazione ALTER AVAILABILITY GROUP nel gruppo di disponibilità, l'autorizzazione CONTROL AVAILABILITY GROUP, l'autorizzazione ALTER ANY AVAILABILITY GROUP o l'autorizzazione CONTROL SERVER.  
  
##  <a name="using-the-add-database-to-availability-group-wizard-sql-server-management-studio"></a><a name="SSMSProcedure"></a>Utilizzo della procedura guidata Aggiungi database a gruppo di disponibilità (SQL Server Management Studio)  
 **Per utilizzare la procedura guidata Aggiungi database a gruppo di disponibilità**  
  
1.  In Esplora oggetti connettersi all'istanza del server che ospita la replica primaria del gruppo di disponibilità ed espandere l'albero del server.  
  
2.  Espandere il nodo **Disponibilità elevata AlwaysOn** e il nodo **Gruppi di disponibilità** .  
  
3.  Fare clic con il pulsante destro del mouse sul gruppo di disponibilità a cui si aggiunge un database e selezionare il comando **Aggiungi database** . Verrà avviata la procedura guidata Aggiungi database a gruppo di disponibilità.  
  
4.  Nella pagina **Seleziona database** selezionare uno o più database. Per ulteriori informazioni, vedere [pagina Selezione database &#40;creazione guidata gruppo di disponibilità-aggiunta guidata Database&#41;](select-databases-page-new-availability-group-wizard-and-add-database-wizard.md).  
  
5.  Nella pagina **Seleziona sincronizzazione dei dati iniziale** specificare come creare e aggiungere i nuovi database secondari al gruppo di disponibilità. Scegliere una delle seguenti opzioni:  
  
    -   **Completo**  
  
         Selezionare questa opzione se l'ambiente soddisfa i requisiti per l'avvio automatico della sincronizzazione dei dati iniziale. Per altre informazioni, vedere [Prerequisiti, restrizioni e raccomandazioni](#Prerequisites), più indietro in questo argomento.  
  
         Se si seleziona **Completo**, dopo avere creato il gruppo di disponibilità verrà tentato il backup di ogni database primario e del relativo log delle transazioni su una condivisione di rete e verranno ripristinati i backup su ogni istanza del server in cui è ospitata una replica secondaria. Ogni database secondario verrà quindi aggiunto al gruppo di disponibilità.  
  
         Nel campo **Specificare un percorso di rete condiviso accessibile da tutte le repliche:** specificare una condivisione di backup a cui possano accedere in lettura e scrittura tutte le istanze del server che ospitano repliche. I backup del log faranno parte della catena di backup del log. Archiviare i file di backup del log in modo appropriato.  
  
        > [!IMPORTANT]  
        >  Per informazioni sulle autorizzazioni del file system necessarie, vedere [Prerequisiti](#Prerequisites)più indietro in questo argomento.  
  
    -   **Solo join**  
  
         Se sono stati preparati manualmente database secondari sulle istanze del server che ospiteranno le repliche secondarie, è possibile selezionare questa opzione. I database secondari esistenti verranno uniti al gruppo di disponibilità tramite la procedura guidata.  
  
    -   **Ignora sincronizzazione dei dati iniziale**  
  
         Selezionare questa opzione se si desidera usare i backup dei database e del log dei database primari. Per altre informazioni, vedere [Avviare lo spostamento dati su un database secondario AlwaysOn &#40;SQL Server&#41;](start-data-movement-on-an-always-on-secondary-database-sql-server.md).  
  
     Per ulteriori informazioni, vedere [pagina Seleziona sincronizzazione dati iniziale &#40;procedure guidate gruppi di disponibilità AlwaysOn&#41;](select-initial-data-synchronization-page-always-on-availability-group-wizards.md).  
  
6.  Nella pagina **Connetti a repliche secondarie esistenti** , se le istanze di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] che ospitano le repliche di disponibilità per questo gruppo di disponibilità vengono tutte eseguite come un servizio nello stesso account utente, scegliere **Connetti tutto**. Se alcune delle istanze del server vengono eseguite come un servizio con account diversi, fare clic sul pulsante **Connetti** singolo a destra di ogni nome di istanza del server.  
  
     Per ulteriori informazioni, vedere la [pagina connessione a repliche secondarie esistenti &#40;aggiunta guidata replica e aggiunta guidata database&#41;](connect-to-existing-secondary-replicas-page.md).  
  
7.  Nella pagina **Convalida** viene verificato se i valori specificati in questa procedura guidata soddisfano i requisiti della Creazione guidata Gruppo di disponibilità. Per apportare una modifica, è possibile fare clic su **Precedente** per tornare a una pagina precedente della procedura guidata per modificare uno o più valori. Scegliere **Avanti** per tornare alla pagina **Convalida** , quindi fare clic su **Ripeti convalida**.  
  
     Per ulteriori informazioni, vedere la [pagina convalida &#40;procedure guidate gruppi di disponibilità AlwaysOn&#41;](validation-page-always-on-availability-group-wizards.md).  
  
8.  Nella pagina **Riepilogo** rivedere le scelte effettuate per il nuovo gruppo di disponibilità. Per apportare una modifica, fare clic su **Indietro** per tornare alla pagina pertinente. Dopo avere apportato la modifica, fare clic su **Avanti** per tornare alla pagina **Riepilogo** .  
  
     Per ulteriori informazioni, vedere la [pagina riepilogo &#40;procedure guidate gruppi di disponibilità AlwaysOn&#41;](summary-page-always-on-availability-group-wizards.md).  
  
     Se si è soddisfatti delle selezioni, è possibile fare clic su Script per creare uno script dei passaggi eseguiti dalla procedura guidata. Per creare e configurare il nuovo gruppo di disponibilità, fare quindi clic su **Fine**.  
  
9. Nella pagina **Stato** viene visualizzato lo stato di avanzamento dei passaggi per la creazione del gruppo di disponibilità, ovvero configurazione di endpoint, creazione del gruppo di disponibilità e creazione di un join della replica secondaria al gruppo.  
  
     Per ulteriori informazioni, vedere [pagina stato &#40;procedure guidate gruppi di disponibilità AlwaysOn&#41;](progress-page-always-on-availability-group-wizards.md).  
  
10. Al termine di questi passaggi, nella pagina **Risultati** vengono visualizzati i relativi risultati. Se tutti questi passaggi sono stati eseguiti correttamente, il nuovo gruppo di disponibilità è completamente configurato. Se si verifica un errore durante uno dei passaggi, potrebbe essere necessario completare manualmente la configurazione. Per informazioni sulla causa di un determinato errore, fare clic sul collegamento "Errore" nella colonna **Risultato** .  
  
     Al termine della procedura guidata, fare clic su **Chiudi** per uscire.  
  
     Per altre informazioni, vedere [Pagina Risultati &#40;procedure guidate gruppi di disponibilità AlwaysOn&#41;](results-page-always-on-availability-group-wizards.md).  
  
11. Se la sincronizzazione dati iniziale non è stata avviata automaticamente su tutti i database secondari, è necessario configurare eventuali database secondari non ancora aggiunti. Per altre informazioni, vedere [Avviare lo spostamento dati su un database secondario AlwaysOn &#40;SQL Server&#41;](start-data-movement-on-an-always-on-secondary-database-sql-server.md).  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> Attività correlate  
  
-   [Preparare manualmente un database secondario per un gruppo di disponibilità &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)  
  
-   [Creare un join di un database secondario a un gruppo di disponibilità &#40;SQL Server&#41;](join-a-secondary-database-to-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Prerequisiti, restrizioni e consigli per Gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [Aggiungere un database a un gruppo di disponibilità &#40;SQL Server&#41;](availability-group-add-a-database.md)   
 [Avviare lo spostamento dati su un database secondario AlwaysOn &#40;SQL Server&#41;](start-data-movement-on-an-always-on-secondary-database-sql-server.md)   
 [Aggiungere un database a un gruppo di disponibilità &#40;SQL Server&#41;](availability-group-add-a-database.md)  
  
  
