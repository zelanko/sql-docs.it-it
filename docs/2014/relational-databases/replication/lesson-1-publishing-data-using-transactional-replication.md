---
title: 'Lezione 1: Pubblicazione dei dati tramite la replica transazionale | Microsoft Docs'
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: 9c55aa3c-4664-41fc-943f-e817c31aad5e
author: rothja
ms.author: jroth
ms.openlocfilehash: ff715b51a7fa84a462d1439e78627d648e20472d
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065961"
---
# <a name="lesson-1-publishing-data-using-transactional-replication"></a>Lezione 1: Pubblicazione dei dati tramite la replica transazionale
  In questa lezione verrà creata una pubblicazione transazionale con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per pubblicare un subset filtrato della tabella **Product** nel database di esempio [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Verrà inoltre aggiunto l'account di accesso di SQL Server utilizzato dall'agente di distribuzione all'elenco di accesso alla pubblicazione. Per eseguire questa esercitazione è necessario avere completato l'esercitazione precedente [Preparazione del server per la replica](tutorial-preparing-the-server-for-replication.md).  
  
### <a name="to-create-a-publication-and-define-articles"></a>Per creare una pubblicazione e definire articoli  
  
1.  Connettersi al server di pubblicazione in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e quindi espandere il nodo del server.  
  
2.  Espandere la cartella **Replica** , fare clic con il pulsante destro del mouse sulla cartella **Pubblicazioni locali** e quindi scegliere **Nuova pubblicazione**.  
  
     Verrà avviata la Creazione guidata nuova pubblicazione.  
  
3.  Nella pagina Database di pubblicazione selezionare [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]e quindi fare clic su **Avanti**.  
  
4.  Nella pagina Tipo di pubblicazione selezionare **Pubblicazione transazionale**e quindi fare clic su **Avanti**.  
  
5.  Nella pagina Articoli espandere il nodo **Tabelle** , selezionare la casella di controllo **Product** , quindi espandere **Product** e deselezionare le caselle di controllo **ListPrice** e **StandardCost** . Fare clic su **Avanti**.  
  
6.  Nella pagina Filtro righe tabella fare clic su **Aggiungi**.  
  
7.  Nella finestra di dialogo **Aggiungi filtro** fare clic sulla colonna **SafetyStockLevel** , fare clic sulla freccia destra per aggiungere la colonna alla clausola WHERE dell'istruzione per il filtro e modificare la clausola WHERE come segue:  
  
    ```  
    WHERE [SafetyStockLevel] < 500  
    ```  
  
8.  Fare clic su **OK** e quindi su **Avanti**.  
  
9. Selezionare la casella di controllo **Crea uno snapshot immediatamente e mantieni lo snapshot disponibile per l'inizializzazione delle sottoscrizioni** e fare clic su **Avanti**.  
  
10. Nella pagina Sicurezza agente deselezionare la casella di controllo **Usa le impostazioni di sicurezza dell'agente snapshot** .  
  
11. Fare clic su **impostazioni di sicurezza** per il agente di snapshot, immettere \<_Machine_Name> _**\ Repl_snapshot** nella casella **account processo** , specificare la password per l'account, quindi fare clic su **OK**.  
  
12. Ripetere il passaggio precedente per impostare repl_logreader come account di processo per l'agente di lettura log e quindi fare clic su **Fine**.  
  
13. Nella pagina Completamento procedura guidata digitare **AdvWorksProductTrans** nella casella **Nome pubblicazione** , quindi fare clic su **Fine**.  
  
14. Dopo aver creato la pubblicazione, fare clic su **Chiudi** per completare la procedura guidata.  
  
### <a name="to-view-the-status-of-snapshot-generation"></a>Per visualizzare lo stato della generazione dello snapshot  
  
1.  Connettersi al server di pubblicazione in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], espandere il nodo del server e quindi la cartella **Replica** .  
  
2.  Nella cartella **Pubblicazioni locali** fare clic con il pulsante destro del mouse su **AdvWorksProductTrans**e quindi scegliere **Visualizza stato agente snapshot**.  
  
3.  Verrà visualizzato lo stato corrente del processo dell'agente snapshot per la pubblicazione. Verificare che il processo snapshot abbia avuto esito positivo prima di passare alla lezione successiva.  
  
### <a name="to-add-the-distribution-agent-login-to-the-pal"></a>Per aggiungere l'account di accesso dell'agente di distribuzione all'elenco di accesso alla pubblicazione  
  
1.  Connettersi al server di pubblicazione in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], espandere il nodo del server e quindi la cartella **Replica** .  
  
2.  Nella cartella **Pubblicazioni locali** fare clic con il pulsante destro del mouse su **AdvWorksProductTrans**e quindi scegliere **Proprietà**.  
  
     Verrà visualizzata la finestra di dialogo **Proprietà pubblicazione** .  
  
3.  Selezionare la pagina **Elenco di accesso alla pubblicazione** e fare clic su **Aggiungi**.  
  
4.  Nella finestra di dialogo **Aggiungi accesso alla pubblicazione** selezionare _<Machine_Name>_**\repl_distribution** e quindi fare clic su **OK**. Fare clic su **OK**.  
  
## <a name="next-steps"></a>Passaggi successivi  
 In questo modo è stata creata la pubblicazione transazionale. Il passaggio successivo consiste nel sottoscrivere la pubblicazione. Vedere [Lezione 2: Creazione di una sottoscrizione per una pubblicazione transazionale](lesson-2-creating-a-subscription-to-the-transactional-publication.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Filtrare i dati pubblicati](publish/filter-published-data.md)   
 [Definire un articolo](publish/define-an-article.md)   
 [Creare e applicare lo snapshot](create-and-apply-the-snapshot.md)  
  
  
