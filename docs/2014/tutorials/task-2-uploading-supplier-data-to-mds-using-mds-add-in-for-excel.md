---
title: 'Attività 2: Caricamento dei dati dei fornitori in MDS utilizzando il componente aggiuntivo MDS per Excel. Documenti Microsoft'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 598deb57-e0cc-4e0a-aeb1-94432c094c67
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 4e3cd4cecd88bcad83c6e9f2a59ecd5f225fb02a
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487695"
---
# <a name="task-2-uploading-supplier-data-to-mds-using-mds-add-in-for-excel"></a>Attività 2: Caricamento dei dati fornitore in MDS tramite il componente aggiuntivo MDS per Excel
  In questa attività si pubblicano i dati puliti e fornitore **in MDS** utilizzando il **componente aggiuntivo MDS per Excel**. Creare un'entità denominata **Fornitore** nel modello **Fornitori** creato nella lezione precedente. All'entità sarà associato un attributo per ogni colonna nel file di Excel. Gli attributi Code e Name dell'entità Supplier corrispondono alle colonne **SupplierID** e **Supplier Name** in Excel.  
  
1.  Aprire **Cleansed e Matched Suppliers.xls** in **Excel**.  
  
2.  Per selezionare interi dati, premete **CTRL-A.** È **importante** selezionare tutti i dati nel foglio di calcolo.  
  
3.  Fare clic su **Dati master** sulla barra dei menu.  
  
4.  Fare clic sul pulsante **Crea entità** sulla barra multifunzione.  
  
     ![Excel - Scheda Dati master - Pulsante Crea entità](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-01.jpg "Excel - Scheda Dati master - Pulsante Crea entità")  
  
5.  Nella finestra di dialogo **Gestisci connessioni,** se la connessione al **server MDS locale** non viene visualizzata in Connessioni **esistenti**, eseguire le operazioni seguenti:  
  
    1.  Selezionare **Crea una nuova connessione**e fare clic sul pulsante **Nuovo.**  
  
    2.  Nella finestra di dialogo **Aggiungi nuova connessione** digitare Server **MDS locale** per **Descrizione** e **http:\//localhost/MDS** per **l'indirizzo del server MDS**, quindi fare clic **su OK** per chiudere la finestra di dialogo.  
  
6.  Nella finestra di dialogo **Gestisci connessioni** selezionare **Server MDS locale** (`http://localhost/MDS`), fare clic su **Test** per verificare la connessione. Fare clic **su OK** nella finestra di messaggio.  
  
7.  Fare clic su **Connetti** per connettersi al server MDS.  
  
8.  Nella finestra di dialogo **Crea entità** selezionare **Fornitori** per il **modello**.  
  
9. Assicurarsi che **VERSION_1** sia selezionato per **Versione**.  
  
10. Immettere **Fornitore** per **Nuovo nome entità**.  
  
11. Selezionare **IDFornitore** per la colonna che contiene un campo **identificatore univoco** (è anche possibile generare un codice automaticamente). Si esegue essenzialmente il mapping della colonna **SupplierID** in **Excel** all'attributo **Code** dell'entità **Supplier.**  
  
12. Selezionare **Nome fornitore** per il campo Nomi della colonna contenente i **nomi.** Si esegue essenzialmente il mapping della colonna **Nome fornitore** in **Excel** all'attributo **Name** dell'entità **Supplier.** Gli attributi **Code** e **Name** sono attributi obbligatori per un'entità in MDS.  
  
     ![Finestra di dialogo Crea entità](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-02.jpg "Finestra di dialogo Crea entità")  
  
13. Fare clic **su OK** per creare l'entità in MDS, pubblicare i dati master nell'entità e chiudere la finestra di dialogo **Crea entità.**  
  
14. A questo punto, si dovrebbe vedere un nuovo foglio denominato **Fornitore**, che è il nome dell'entità, aggiunto al foglio di calcolo di Excel e nella parte superiore del foglio di lavoro si dovrebbe vedere che il foglio di lavoro è connesso al server MDS. Si noti che il foglio di lavoro originale (denominato **Foglio1**) esiste ancora.  
  
     ![Excel - Schede Fornitore e Foglio1](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-03.jpg "Excel - Schede Fornitore e Foglio1")  
  
     ![Excel - Visualizzazione dettagli connessione MDS](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-04.jpg "Excel - Visualizzazione dettagli connessione MDS")  
  
15. Mantenere **Excel** aperto.  
  
## <a name="next-task"></a>Attività successiva  
 [Attività 3: Verifica dei dati in Gestione dati master](../../2014/tutorials/task-3-verifying-the-data-in-master-data-manager.md)  
  
  
