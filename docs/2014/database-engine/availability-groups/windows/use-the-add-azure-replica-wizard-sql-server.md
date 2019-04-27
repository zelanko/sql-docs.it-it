---
title: Usare la procedura guidata Aggiungi replica Azure (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql12.swb.addreplicawizard.azurereplica.f1
ms.assetid: b89cc41b-07b4-49f3-82cc-bc42b2e793ae
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: f2b925540844a45d94fb2ee823a8ac5e9bc7ef2a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62788129"
---
# <a name="use-the-add-azure-replica-wizard-sql-server"></a>Utilizzare la procedura guidata Aggiungi replica Azure (SQL Server)
  La procedura guidata Aggiungi replica Azure consente di creare una nuova macchina virtuale di Windows Azure in un ambiente IT ibrido e di configurarla come replica secondaria per un gruppo di disponibilità AlwaysOn nuovo o esistente.  
  
-   **Prima di iniziare:**  
  
     [Prerequisiti](#Prerequisites)  
  
     [Sicurezza](#Security)  
  
-   **Per aggiungere una replica mediante:**  [Aggiungi Replica Azure (SQL Server Management Studio)](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Prima di iniziare  
 Se mai stata aggiunta una replica di disponibilità per un gruppo di disponibilità, vedere la "Istanze del Server" e "repliche e gruppi di disponibilità" sezioni in [prerequisiti, restrizioni e consigli per gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md).  
  
###  <a name="Prerequisites"></a> Prerequisiti  
  
-   È necessario essere connessi all'istanza del server che ospita la replica primaria corrente.  
  
-   È necessario utilizzare un ambiente IT ibrido in cui nella subnet locale sia presente una VPN da sito a sito con Windows Azure. Per altre informazioni, vedere [Creare una rete virtuale con una connessione VPN da sito a sito usando il portale di Azure classico](https://azure.microsoft.com/documentation/articles/vpn-gateway-site-to-site-create).  
  
-   Il gruppo di disponibilità deve contenere le repliche di disponibilità locali.  
  
-   I client nel listener del gruppo di disponibilità devono avere la connettività a Internet se desiderano mantenere la connettività con il listener quando viene eseguito il failover del gruppo di disponibilità in una replica di Windows Azure.  
  
-   **Prerequisiti per l'utilizzo della sincronizzazione dei dati iniziale completa** È necessario specificare una condivisione di rete affinché la procedura guidata possa creare e accedere ai backup. Per la replica primaria, all'account usato per avviare il [!INCLUDE[ssDE](../../../includes/ssde-md.md)] devono essere associate le autorizzazioni del file system in lettura e scrittura per una condivisione di rete. Per le repliche secondarie, all'account deve essere associata l'autorizzazione di lettura per la condivisione di rete.  
  
     Se non è possibile usare la procedura guidata per eseguire la sincronizzazione dei dati iniziale completa, sarà necessario preparare i database secondari manualmente. Tale operazione può essere eseguita prima o dopo l'esecuzione della procedura guidata. Per altre informazioni, vedere [Preparare manualmente un database secondario per un gruppo di disponibilità &#40;SQL Server&#41;](manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md).  
  
###  <a name="Security"></a> Sicurezza  
  
####  <a name="Permissions"></a> Autorizzazioni  
 Vedere [Security](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md#Security)  
  
##  <a name="SSMSProcedure"></a> Utilizzo della procedura guidata Aggiungi replica Azure (SQL Server Management Studio)  
 La procedura guidata Aggiungi replica Azure può essere avviata dalla [Pagina Specifica repliche](specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md). Questa pagina può essere visualizzata in due modi:  
  
-   [Usare la Creazione guidata gruppo di disponibilità &#40;SQL Server Management Studio&#41;](use-the-availability-group-wizard-sql-server-management-studio.md)  
  
-   [Usare la procedura guidata Aggiungi replica a gruppo di disponibilità &#40;SQL Server Management Studio&#41;](use-the-add-replica-to-availability-group-wizard-sql-server-management-studio.md)  
  
 Dopo aver avviato la procedura guidata Aggiungi replica Azure effettuare i passaggi seguenti:  
  
1.  Scaricare innanzitutto un certificato di gestione per la sottoscrizione di Windows Azure. Fare clic su **Download** per aprire la pagina di accesso.  
  
2.  Nella pagina di accesso accedere alla sottoscrizione di Windows Azure. Una volta eseguito l'accesso la procedura guidata installa un certificato di gestione nel computer locale. Il certificato di gestione viene caricato automaticamente quando si utilizza di nuovo questa procedura guidata. Se sono stati scaricati più certificati di gestione, è possibile fare clic sul pulsante **...** per selezionare il certificato che si desidera utilizzare.  
  
3.  Connettersi quindi alla sottoscrizione facendo clic su **Connetti**. Una volta connessi, gli elenchi a discesa vengono popolati con i parametri di Microsoft Azure, ad esempio **Rete virtuale** e **Subnet rete virtuale**.  
  
4.  Specificare le impostazioni per la macchina virtuale Windows Azure che ospiterà la nuova replica secondaria:  
  
     Image  
     Nome dell'immagine di SQL Server da utilizzare per la macchina virtuale Windows Azure  
  
     Dimensioni VM  
     Dimensioni della macchina virtuale Windows Azure  
  
     Nome VM  
     Nome DNS della macchina virtuale Windows Azure  
  
     Nome utente VM  
     Nome utente dell'amministratore predefinito della macchina virtuale Windows Azure  
  
     Password amministratore VM (e Conferma password)  
     Password dell'amministratore predefinito della macchina virtuale Windows Azure  
  
     Rete virtuale  
     Rete virtuale in cui posizionare la macchina virtuale Windows Azure  
  
     Subnet rete virtuale  
     Subnet della rete virtuale in cui posizionare la macchina virtuale Windows Azure  
  
     Dominio  
     Dominio Active Directory (AD) a cui aggiungere la macchina virtuale Windows Azure  
  
     Nome utente di dominio  
     Nome utente di Active Directory utilizzato per aggiungere la macchina virtuale Windows Azure al dominio  
  
     Password  
     Password utilizzata per aggiungere la macchina virtuale Windows Azure al dominio  
  
5.  Fare clic su **OK** per eseguire il commit delle impostazioni e chiudere la procedura guidata Aggiungi replica Azure.  
  
6.  Continuare con il resto dei passaggi di configurazione della [Pagina Specifica repliche](specify-replicas-page-new-availability-group-wizard-add-replica-wizard.md) come per qualsiasi nuova replica.  
  
     Dopo avere completato la Creazione guidata Gruppo di disponibilità o la Procedura guidata Aggiungi replica a gruppo di disponibilità, il processo di configurazione esegue tutte le operazioni in Windows Azure per creare la nuova macchina virtuale, aggiungerla al dominio Active Directory, aggiungerla al cluster di Windows, abilitare la Disponibilità elevata AlwaysOn e aggiungere la nuova replica al gruppo di disponibilità.  
  
##  <a name="RelatedTasks"></a> Attività correlate  
  
-   [Aggiungere una replica secondaria a un gruppo di disponibilità &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Panoramica di gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](overview-of-always-on-availability-groups-sql-server.md)   
 [Prerequisiti, restrizioni e consigli per gruppi di disponibilità AlwaysOn &#40;SQL Server&#41;](prereqs-restrictions-recommendations-always-on-availability.md)   
 [Aggiungere una replica secondaria a un gruppo di disponibilità &#40;SQL Server&#41;](add-a-secondary-replica-to-an-availability-group-sql-server.md)  
  
  
