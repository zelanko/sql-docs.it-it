---
title: 'Lezione 2: Creazione di una sottoscrizione per una pubblicazione transazionale | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 5995b7d2-7c06-46f5-b96c-2bee879bcda2
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: d3e8b5f0be58d9153fbe4d0ffd0287ea753fcc5e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "62721081"
---
# <a name="lesson-2-creating-a-subscription-to-the-transactional-publication"></a>Lezione 2: Creazione di una sottoscrizione per una pubblicazione transazionale
  In questa lezione verranno descritte le procedure per creare una sottoscrizione in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Per eseguire questa lezione è necessario aver completato la lezione precedente, [Lezione 1: Pubblicazione dei dati tramite la replica transazionale](lesson-1-publishing-data-using-transactional-replication.md).  
  
### <a name="to-create-the-subscription"></a>Per creare la sottoscrizione  
  
1.  Connettersi al server di pubblicazione [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]in, espandere il nodo del server, quindi espandere la cartella **replica** .  
  
2.  Nella cartella **Pubblicazioni locali** fare clic con il pulsante destro del mouse sulla pubblicazione **AdvWorksProductTrans** e quindi scegliere **Nuove sottoscrizioni**.  
  
     Verrà avviata la Creazione guidata nuova sottoscrizione.  
  
3.  Nella pagina Pubblicazione selezionare **AdvWorksProductTrans**e quindi fare clic su **Avanti**.  
  
4.  Nella pagina Posizione in cui eseguire l'agente di distribuzione selezionare **Esegui tutti gli agenti nel database di distribuzione**e quindi fare clic su **Avanti**.  
  
5.  Nella pagina Sottoscrittori, se il nome dell'istanza del Sottoscrittore non è visualizzato, fare clic su **Aggiungi Sottoscrittore**, quindi su **Aggiungi Sottoscrittore SQL Server**, immettere il nome dell'istanza del Sottoscrittore nella finestra di dialogo **Connetti al server** e quindi fare clic su **Connetti**.  
  
6.  Nella pagina Sottoscrittori selezionare il nome dell'istanza del server Sottoscrittore e selezionare ** \<nuovo database>** nel **database di sottoscrizione**.  
  
7.  Nella finestra di dialogo **Nuovo database** digitare **ProductReplica** nella casella **Nome database** , fare clic su **OK**e scegliere **Avanti**.  
  
8.  Nella finestra di dialogo **sicurezza agente di distribuzione** fare clic sul pulsante con i puntini di sospensione (**..**.), immettere \< _Machine_Name>_ **\ repl_distribution** nella casella **account processo** , immettere la password per l'account, fare clic su **OK**e quindi su **Avanti**.  
  
9. Fare clic su **Fine** per accettare i valori predefiniti nelle pagine seguenti e completare la procedura guidata.  
  
### <a name="setting-database-permissions-at-the-subscriber"></a>Impostazione delle autorizzazioni per il database nel Sottoscrittore  
  
1.  Connettersi al Sottoscrittore in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], espandere **Database**, **ProductReplica**e **Sicurezza**, fare clic con il pulsante destro del mouse su **Utenti**e quindi scegliere **Nuovo utente**.  
  
2.  Nella pagina **Generale** , nell'elenco della pagina **Tipo utente** selezionare **Utente di Windows**.  
  
3.  Selezionare la casella **nome utente** e fare clic sul pulsante con i puntini di sospensione (...) nella casella **immettere il nome dell'oggetto da selezionare** <Machine_Name>**\ Repl_distribution**, fare clic su **Controlla nomi**e quindi su **OK**.  
  
4.  Nella pagina **Appartenenze** , in **Appartenenza a ruoli del database** selezionare **db_owner**, quindi scegliere **OK** per creare l'utente.  
  
### <a name="to-view-the-synchronization-status-of-the-subscription"></a>Per visualizzare lo stato di sincronizzazione della sottoscrizione  
  
1.  Connettersi al server di pubblicazione [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]in, espandere il nodo del server, quindi espandere la cartella **replica** .  
  
2.  Nella cartella **Pubblicazioni locali** espandere la pubblicazione **AdvWorksProductTrans** , fare clic con il pulsante destro del mouse sulla sottoscrizione nel database **ProductReplica** e quindi scegliere **Visualizza stato sincronizzazione**.  
  
     Verrà visualizzato lo stato corrente della sincronizzazione della sottoscrizione.  
  
3.  Se la sottoscrizione non è visualizzata in **AdvWorksProductTrans**, premere F5 per aggiornare l'elenco.  
  
## <a name="next-steps"></a>Passaggi successivi  
 In questo modo è stata creata una sottoscrizione per la pubblicazione transazionale. Poiché l'agente di distribuzione per questa sottoscrizione è in esecuzione continua, la sottoscrizione viene inizializzata al momento della creazione. Il passaggio successivo consiste nell'utilizzo di token di traccia per verificare che le modifiche sono state replicate nel Sottoscrittore e per determinare la latenza. Vedere [Lezione 3: Convalida della sottoscrizione e misurazione della latenza](lesson-3-validating-the-subscription-and-measuring-latency.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Inizializzare una sottoscrizione con uno snapshot](initialize-a-subscription-with-a-snapshot.md)   
 [Create a Push Subscription](create-a-push-subscription.md)   
 [Sottoscrizione delle pubblicazioni](subscribe-to-publications.md)  
  
  
