---
title: Visualizzare i conflitti di dati per le pubblicazioni transazionali (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- conflict resolution [SQL Server replication], queued updating subscriptions
- queued updating subscriptions [SQL Server replication]
- viewing conflict information
ms.assetid: 9977dd75-b0de-4376-9c13-86d80567d8aa
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e046351ca3dc7977691fc98e24453ccbf8e6af53
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63144412"
---
# <a name="view-data-conflicts-for-transactional-publications-sql-server-management-studio"></a>Visualizzazione di conflitti di dati per le pubblicazioni transazionali (SQL Server Management Studio)
  Il Visualizzatore conflitti di replica [!INCLUDE[msCoName](../../includes/msconame-md.md)] consente di visualizzare i conflitti per la replica transazionale peer-to-peer e per la replica transazionale con sottoscrizioni ad aggiornamento in coda. Per informazioni sul rilevamento e la risoluzione dei conflitti, vedere [Rilevamento dei conflitti nella replica peer-to-peer](transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md) e [Impostare le opzioni di risoluzione dei conflitti per l'aggiornamento in coda &#40;SQL Server Management Studio&#41;](publish/create-an-updatable-subscription-to-a-transactional-publication.md).  
  
 La disponibilità di dati dei conflitti dipende dal tipo di replica e dal periodo di memorizzazione dei conflitti:  
  
-   Per la replica peer-to-peer, per impostazione predefinita quando viene rilevato un conflitto si verifica un errore dell'agente di distribuzione. Nel log degli errori viene registrato un errore di conflitto, ma nella tabella dei conflitti non vengono registrati dati, che non sono quindi disponibili per la visualizzazione. Se l'esecuzione dell'agente di distribuzione può continuare, viene registrato localmente un conflitto in ogni nodo in cui è stato rilevato. Per ulteriori informazioni, vedere la sezione relativa alla gestione dei conflitti in [Conflict Detection in Peer-to-Peer Replication](transactional/peer-to-peer-conflict-detection-in-peer-to-peer-replication.md).  
  
-   Per le sottoscrizioni ad aggiornamento in coda, sono disponibili dati per ogni conflitto. I dati dei conflitti sono disponibili nel Visualizzatore conflitti di replica per l'intervallo di tempo specificato per il periodo di memorizzazione dei conflitti, che per impostazione predefinita è di 14 giorni. Per impostare il periodo di memorizzazione dei conflitti, eseguire una delle operazioni seguenti:  
  
    -   Specificare un valore del periodo di memorizzazione per il parametro @conflict_retention di [sp_addpublication](/sql/relational-databases/system-stored-procedures/sp-addpublication-transact-sql).  
  
    -   Specificare il valore `'conflict_retention'` per il @property parametro e un periodo di conservazione valore per il @value parametro [sp_changepublication](/sql/relational-databases/system-stored-procedures/sp-changepublication-transact-sql).  
  
### <a name="to-view-conflicts"></a>Per visualizzare i conflitti  
  
1.  Connettersi al server appropriato in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], quindi espandere il nodo del server:  
  
    -   Per la replica peer-to-peer, si tratta del nodo in cui si è verificato il conflitto.  
  
    -   Per le sottoscrizioni ad aggiornamento in coda, si tratta di server di pubblicazione.  
  
2.  Espandere la cartella **Replica** e quindi la cartella **Pubblicazioni locali** .  
  
3.  Fare clic con il pulsante destro del mouse sulla pubblicazione per la quale si desidera visualizzare i conflitti e quindi scegliere **Visualizza conflitti**.  
  
4.  Nella finestra di dialogo **Seleziona tabella con conflitti** selezionare un database, una pubblicazione e una tabella per cui visualizzare i conflitti.  
  
5.  Nel Visualizzatore conflitti di replica è possibile:  
  
    -   Filtrare le righe con i pulsanti a destra della griglia superiore.  
  
    -   Selezionare una riga nella griglia superiore per visualizzare le informazioni su tale riga nella griglia inferiore.  
  
    -   Selezionare una o più righe nella griglia superiore e quindi fare clic su **Rimuovi**per rimuovere la riga dalla tabella di metadati dei conflitti.  
  
    -   Fare clic sul pulsante delle proprietà (**...**) per visualizzare altre informazioni su una colonna coinvolta in un conflitto.  
  
    -   Selezionare **Registra informazioni dettagliate sul conflitto** per registrare i dati del conflitto in un file. Per specificare un percorso per il file, scegliere **Opzioni** dal menu **Visualizza**. Immettere un valore o fare clic sul pulsante Sfoglia (**...**) e quindi passare al file appropriato. Fare clic su **OK** per chiudere la finestra di dialogo **Opzioni** .  
  
6.  Chiudere il Visualizzatore conflitti di replica.  
  
## <a name="see-also"></a>Vedere anche  
 [Replica transazionale peer-to-peer](transactional/peer-to-peer-transactional-replication.md)   
 [Queued Updating Conflict Detection and Resolution](transactional/updatable-subscriptions-queued-updating-conflict-resolution.md)  
  
  
