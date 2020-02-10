---
title: 'Attività 2: caricamento dei dati fornitore in MDS tramite Componente aggiuntivo MDS per Excel | Microsoft Docs'
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
ms.openlocfilehash: 57a5044ccee040ef1eba95925c689f48739c259f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "65484667"
---
# <a name="task-2-uploading-supplier-data-to-mds-using-mds-add-in-for-excel"></a>Attività 2: Caricamento dei dati fornitore in MDS utilizzando il componente aggiuntivo MDS per excel
  In questa attività verranno pubblicati i dati puliti e fornitore in **MDS** utilizzando il **componente aggiuntivo MDS per Excel**. Si crea un'entità denominata **Supplier** nel modello **Suppliers** creato nella lezione precedente. All'entità sarà associato un attributo per ogni colonna nel file di Excel. Gli attributi di codice e nome dell'entità Supplier corrispondono alle colonne **SupplierID** e **Supplier Name** in Excel.  
  
1.  Aprire **cleand and Matched Suppliers. xls** in **Excel**.  
  
2.  Premere **CTRL + a** per selezionare tutti i dati. È **importante** selezionare tutti i dati nel foglio di calcolo.  
  
3.  Fare clic su **dati master** sulla barra dei menu.  
  
4.  Fare clic sul pulsante **Crea entità** sulla barra multifunzione.  
  
     ![Excel - Scheda Dati master - Pulsante Crea entità](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-01.jpg "Excel - Scheda Dati master - Pulsante Crea entità")  
  
5.  Nella finestra di dialogo **Gestisci connessioni** , se non si visualizza la connessione al **Server MDS locale** in **connessioni esistenti**, effettuare le seguenti operazioni:  
  
    1.  Selezionare **Crea una nuova connessione**e fare clic sul pulsante **nuovo** .  
  
    2.  Nella finestra di dialogo **Aggiungi nuova connessione** digitare **Server MDS locale** per **Descrizione** e **http://localhost/MDS** per **Indirizzo server MDS**, quindi fare clic su **OK** per chiudere la finestra di dialogo.  
  
6.  Nella finestra di dialogo **Gestisci connessioni** selezionare **Server MDS locale** (http://localhost/MDS), fare clic su **test** per testare la connessione. Fare clic su **OK** nella finestra di messaggio.  
  
7.  Fare clic su **Connetti** per connettersi al server MDS.  
  
8.  Nella finestra di dialogo **Crea entità** selezionare **Suppliers** per il **modello**.  
  
9. Verificare che sia selezionato **VERSION_1** per la **versione**.  
  
10. Immettere **Supplier** per **nome nuova entità**.  
  
11. Selezionare **SupplierID** per **la colonna contenente un campo identificatore univoco** . è anche possibile generare automaticamente un codice. Si sta essenzialmente eseguendo il mapping della colonna **SupplierID** in **Excel** all'attributo **Code** dell'entità **Supplier** .  
  
12. Selezionare **Supplier Name** per **la colonna che contiene il campo names** . Si sta essenzialmente eseguendo il mapping della colonna **Supplier Name** in **Excel** all'attributo **Name** dell'entità **Supplier** . Gli attributi del **nome** e del **codice** sono attributi obbligatori per un'entità in MDS.  
  
     ![Finestra di dialogo Crea entità](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-02.jpg "Finestra di dialogo Crea entità")  
  
13. Fare clic su **OK** per creare l'entità in MDS, pubblicare i dati master nell'entità e chiudere la finestra di dialogo **Crea entità** .  
  
14. A questo punto, verrà visualizzato un nuovo foglio denominato **Supplier**, che è il nome dell'entità, aggiunto al foglio di calcolo di Excel e nella parte superiore del foglio di lavoro si noterà che il foglio di lavoro è connesso al server MDS. Si noti che il foglio di foglio originale (denominato **Sheet1**) esiste ancora.  
  
     ![Excel - Schede Fornitore e Foglio1](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-03.jpg "Excel - Schede Fornitore e Foglio1")  
  
     ![Excel - Visualizzazione dettagli connessione MDS](../../2014/tutorials/media/et-ulingsdtomdsusingmdsaddinforexcel-04.jpg "Excel - Visualizzazione dettagli connessione MDS")  
  
15. Mantieni aperto **Excel** .  
  
## <a name="next-task"></a>Attività successiva  
 [Attività 3: Verifica dei dati in Gestione dati master](../../2014/tutorials/task-3-verifying-the-data-in-master-data-manager.md)  
  
  
