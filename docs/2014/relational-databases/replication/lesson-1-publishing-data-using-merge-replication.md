---
title: 'Lezione 1: Pubblicazione dei dati tramite la replica di tipo merge | Microsoft Docs'
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- replication [SQL Server], tutorials
ms.assetid: c3c6e0b6-54cd-4b7d-8efb-2cefe14fcd7f
author: rothja
ms.author: jroth
ms.openlocfilehash: 30d7c1e04c305a74f99d5d2818b344bfd8f83bd1
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85065993"
---
# <a name="lesson-1-publishing-data-using-merge-replication"></a>Lezione 1: Pubblicazione dei dati tramite la replica di tipo merge
  In questa lezione verrà creata una pubblicazione di tipo merge con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] per pubblicare un subset delle tabelle **Employee**, **SalesOrderHeader**e **SalesOrderDetail** nel database di esempio [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] . Queste tabelle vengono filtrate usando filtri di riga con parametri in modo che ogni sottoscrizione contenga una partizione univoca dei dati. Verrà inoltre aggiunto l'account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usato dall'agente di merge all'elenco di accesso alla pubblicazione. Per eseguire questa esercitazione è necessario avere completato l'esercitazione precedente [Preparazione del server per la replica](tutorial-preparing-the-server-for-replication.md).  
  
### <a name="to-create-a-publication-and-define-articles"></a>Per creare una pubblicazione e definire articoli  
  
1.  Connettersi al server di pubblicazione in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]e quindi espandere il nodo del server.  
  
2.  Espandere la cartella **Replica** , fare clic con il pulsante destro del mouse su **Pubblicazioni locali**e quindi scegliere **Nuova pubblicazione**.  
  
     Verrà avviata la Creazione guidata nuova pubblicazione.  
  
3.  Nella pagina Database di pubblicazione selezionare [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)]e quindi fare clic su **Avanti**.  
  
4.  Nella pagina Tipo di pubblicazione selezionare **Pubblicazione di tipo merge**e quindi fare clic su **Avanti**.  
  
5.  Nella pagina Tipo di Sottoscrittore verificare che sia selezionato solo [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o versione successiva, quindi fare clic su **Avanti**.  
  
6.  Nella pagina Articoli espandere il nodo **Tabelle** , selezionare **SalesOrderHeader** e **SalesOrderDetail**, espandere **Employee**, selezionare **EmployeeID** o **LoginID**e quindi fare clic su **Avanti**.  
  
    > [!TIP]  
    >  Le colonne necessarie aggiuntive sono selezionate automaticamente. Selezionare tutte le colonne selezionate automaticamente e visualizzare la nota sotto l'elenco **Oggetti da pubblicare** per una spiegazione sul motivo per cui la colonna è necessaria.  
  
7.  Nella pagina Filtro righe tabella fare clic su **Aggiungi** e quindi su **Aggiungi filtro**.  
  
8.  Nella finestra di dialogo **Aggiungi filtro** selezionare **Employee (HumanResources)** in **Selezionare la tabella da filtrare**, fare clic sulla colonna **LoginID** , fare clic sulla freccia destra per aggiungere la colonna alla clausola WHERE della query di filtro, quindi modificare la clausola WHERE come segue:  
  
    ```  
    WHERE [LoginID] = HOST_NAME()  
    ```  
  
9. Selezionare **Una riga di questa tabella verrà inviata a una sola sottoscrizione**e quindi fare clic su **OK**.  
  
10. Nella pagina **Filtro righe tabella** fare clic su **Employee (Human Resources)**, selezionare **Aggiungi** , quindi scegliere **Aggiungi join per estendere il filtro selezionato**.  
  
11. Nella finestra di dialogo **Aggiungi join** selezionare **Sales.SalesOrderHeader** in **Tabella unita in join**, selezionare **L'istruzione per il join verrà scritta manualmente**e quindi completare l'istruzione per il join come segue:  
  
    ```  
    ON Employee.EmployeeID = SalesOrderHeader.SalesPersonID  
    ```  
  
12. In **Specificare le opzioni del join**selezionare **Chiave univoca**e quindi fare clic su **OK**.  
  
13. Nella pagina Filtro righe tabella fare clic su **SalesOrderHeader**, su **Aggiungi**e quindi su **Aggiungi join per estendere il filtro selezionato**.  
  
14. Nella finestra di dialogo **Aggiungi join** selezionare **Sales.SalesOrderDetail** in **Tabella unita in join**.  
  
15. Fare clic su **L'istruzione per il join verrà scritta manualmente**.  
  
16. In **Colonne tabella filtrata**selezionare **BusinessEntityID**, quindi fare clic sul pulsante freccia per copiare il nome della colonna nell'istruzione per il join.  
  
17. Nella casella **Istruzione per il join** completare l'istruzione per il join come indicato di seguito:  
  
    ```  
    ON Employee.BusinessEntityID = SalesOrderHeader.SalesPersonID  
    ```  
  
18. In **Specificare le opzioni del join**selezionare **Chiave univoca**e quindi fare clic su **OK**.  
  
19. Nella pagina **Filtro righe tabella** fare clic su **SalesOrderHeader (Sales)**, selezionare **Aggiungi**, quindi scegliere **Aggiungi join per estendere il filtro selezionato**.  
  
20. Nella finestra di dialogo **Aggiungi join** selezionare **Sales.SalesOrderDetail** in **Tabella unita in join**, fare clic su **OK**e quindi su **Avanti**.  
  
21. Selezionare **Crea snapshot immediatamente**, deselezionare **Usa la pianificazione seguente per l'esecuzione dell'agente snapshot**e quindi fare clic su **Avanti**.  
  
22. Nella pagina sicurezza agente fare clic su **impostazioni di sicurezza**, digitare \<_Machine_Name> _**\ Repl_snapshot** nella casella **account processo** , specificare la password per l'account, quindi fare clic su **OK**. Fare clic su **Fine**.  
  
23. Nella pagina Completamento procedura guidata immettere **AdvWorksSalesOrdersMerge** nella casella **Nome pubblicazione** , quindi fare clic su **Fine**.  
  
24. Dopo aver creato la pubblicazione, fare clic su **Chiudi**.  
  
### <a name="to-view-the-status-of-snapshot-generation"></a>Per visualizzare lo stato della generazione dello snapshot  
  
1.  Connettersi al server di pubblicazione in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], espandere il nodo del server e quindi la cartella **Replica** .  
  
2.  Nella cartella Pubblicazioni locali fare clic con il pulsante destro del mouse su **AdvWorksSalesOrdersMerge**e quindi scegliere **Visualizza stato agente snapshot**.  
  
3.  Verrà visualizzato lo stato corrente del processo dell'agente snapshot per la pubblicazione. Verificare che il processo snapshot abbia avuto esito positivo prima di passare alla lezione successiva.  
  
### <a name="to-add-the-merge-agent-login-to-the-pal"></a>Per aggiungere l'account di accesso dell'agente di merge all'elenco di accesso alla pubblicazione  
  
1.  Connettersi al server di pubblicazione in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], espandere il nodo del server e quindi la cartella **Replica** .  
  
2.  Nella cartella Pubblicazioni locali fare clic con il pulsante destro del mouse su **AdvWorksSalesOrdersMerge**e quindi scegliere **Proprietà**.  
  
     Verrà visualizzata la finestra di dialogo **Proprietà pubblicazione** .  
  
3.  Selezionare la pagina **Elenco di accesso alla pubblicazione** e fare clic su **Aggiungi**.  
  
4.  Nella finestra di dialogo Aggiungi accesso alla pubblicazione selezionare _<Nome_computer>_**\repl_merge** e quindi fare clic su **OK**. Fare clic su **OK**.  
  
## <a name="next-steps"></a>Passaggi successivi  
 In questo modo è stata creata la pubblicazione di tipo merge. Il passaggio successivo consiste nel sottoscrivere la pubblicazione. Vedere [Lezione 2: Creazione di una sottoscrizione per una pubblicazione di tipo merge](lesson-2-creating-a-subscription-to-the-merge-publication.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Filtrare i dati pubblicati](publish/filter-published-data.md)   
 [Filtri di riga con parametri](merge/parameterized-filters-parameterized-row-filters.md)   
 [Definire un articolo](publish/define-an-article.md)  
  
  
