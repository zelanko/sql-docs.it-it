---
title: 'Lesson 4: Define a Data Connection and Data Table for Child Report (Lezione 4: Definire una connessione dati e una tabella dati per il report figlio) | Microsoft Docs'
description: Informazioni su come usare Reporting Services per creare una connessione dati e una tabella di dati per il report figlio.
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: a6aa2c56-227c-43c5-a28e-c7104131ac5e
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 80df8e86ed3d23c5ab097cdab3f26d83838c4544
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87245120"
---
# <a name="lesson-4-define-a-data-connection-and-data-table-for-child-report"></a>Lezione 4: Definire una connessione dati e una tabella di dati per il report figlio
Dopo aver progettato il report padre, il passaggio successivo consiste nel creare una connessione dati e una tabella di dati per il report figlio. In questa esercitazione la connessione dati è al database AdventureWorks2014.  
  
### <a name="to-define-a-data-connection-and-datatable-by-adding-a-dataset-for-child-report"></a>Per definire una connessione dati e l'oggetto DataTable aggiungendo un oggetto DataSet (per il report figlio)  
  
1.  Selezionare **Aggiungi nuovo elemento** dal menu **Sito Web**.  
  
2.  Nella finestra di dialogo **Aggiungi nuovo elemento** selezionare **DataSet** e scegliere **Aggiungi**. Quando richiesto, è necessario aggiungere l'elemento alla cartella **App_Code** selezionando **Sì**.  
  
    Verrà aggiunto un nuovo file XSD **DataSet2.xsd** al progetto e verrà aperto Progettazione DataSet.  
  
3.  Dalla finestra della casella degli strumenti trascinare un controllo **TableAdapter** nell'area di progettazione. Viene avviata la configurazione guidata **TableAdapter** .  
  
4.  Nella pagina **Seleziona connessione dati** è possibile selezionare la connessione creata nella lezione 2. Se è già selezionata, selezionate **Avanti** e andare al passaggio 8. In caso contrario, selezionare **Nuova connessione**.  
  
5.  Nella finestra di dialogo **Aggiungi connessione** effettuare i passaggi seguenti:  
  
    1.  Nella casella **Nome server** immettere il server in cui si trova il database **AdventureWorks2014** .  
  
        L'istanza predefinita di SQL Server Express è **(local)\sqlexpress**.  
  
    2.  Nella sezione **Accesso al server** selezionare l'opzione di accesso ai dati. **Usa autenticazione di Windows** è l'impostazione predefinita.  
  
    3.  Nell'elenco a discesa **Selezionare o immettere un nome di database** selezionare **AdventureWorks2014**.  
  
    4.  Selezionare **OK**, quindi **Avanti**.  
  
6.  Se è stato selezionato **Usa autenticazione di SQL Server** nel passaggio 5 (b), selezionare l'opzione per includere i dati sensibili nella stringa o per impostare le informazioni nel codice dell'applicazione.  
  
7.  Nella pagina **Salva stringa di connessione nel file di configurazione dell'applicazione** digitare il nome per la stringa di connessione o accettare l'impostazione predefinita **AdventureWorks2014ConnectionString**. Selezionare **Avanti**.  
  
8.  Nella pagina **Seleziona un tipo di comando** selezionare **Usa istruzioni SQL**e quindi fare clic su **Avanti**.  
  
9. Nella pagina **Immettere un'istruzione SQL** immettere la seguente query Transact-SQL per recuperare i dati dal database **AdventureWorks2014** e quindi fare clic su **Avanti**.  
  
    ```  
    SELECT PurchaseOrderID, PurchaseOrderDetailID, OrderQty, ProductID, ReceivedQty, RejectedQty, StockedQty FROM Purchasing.PurchaseOrderDetail  
    ```  
  
    È anche possibile creare la query facendo clic su **Generatore di query**e, successivamente, verificare la query facendo clic su **Esegui query** . Se non vengono restituiti i dati previsti dalla query, è possibile che si stia utilizzando una versione precedente di AdventureWorks. Per altre informazioni su come ottenere il database di esempio **AdventureWorks2014**, vedere [Database di esempio AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases).  
  
10. Nella pagina **Scegliere i metodi per generare** deselezionare **Crea metodi per inviare aggiornamenti direttamente al database (GenerateDBDirectMethods)** , quindi fare clic su **Fine**.  
  
    > [!WARNING]  
    > Assicurarsi di deselezionare **Crea metodi per inviare aggiornamenti direttamente al database (GenerateDBDirectMethods)**  
  
    È stata completata la configurazione dell'oggetto [DataTable](https://msdn.microsoft.com/library/system.data.datatable.aspx) di ADO.NET come origine dati del report. Nella pagina Progettazione DataSet in Visual Studio si dovrebbe visualizzare l'oggetto **DataTable** aggiunto, con le colonne specificate nella query. In DataSet2 sono inclusi i dati della tabella PurhcaseOrderDetail, basati sulla query.  
  
11. Salvare il file.  
  
12. Per visualizzare un'anteprima dei dati, scegliere **Anteprima dati** dal menu **Dati** e quindi fare clic su **Anteprima**.  
  
## <a name="next-task"></a>Attività successiva  
È stata creata correttamente una connessione dati e una tabella di dati per il report figlio. Successivamente, verrà progettato il report figlio utilizzando la Creazione guidata report. Vedere [Lezione 5: Progettare il report figlio tramite la Creazione guidata report](../reporting-services/lesson-5-design-the-child-report-using-the-report-wizard.md).  
  

