---
title: 'Lesson 4: Define a Data Connection and Data Table for Child Report (Lezione 4: Definire una connessione dati e una tabella dati per il report figlio) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: a6aa2c56-227c-43c5-a28e-c7104131ac5e
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c1008202519f1d9bcbf48dfdc4cd4ef3a3cbbe20
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66108470"
---
# <a name="lesson-4-define-a-data-connection-and-data-table-for-child-report"></a>Lezione 4: Definire una connessione dati e una tabella di dati per il report figlio
  Dopo aver progettato il report padre, il passaggio successivo consiste nel creare una connessione dati e una tabella di dati per il report figlio. In questa esercitazione la connessione dati è al database AdventureWorks2008. È anche possibile scegliere di connettersi al database AdventureWorks2012.  
  
### <a name="to-define-a-data-connection-and-datatable-by-adding-a-dataset-for-child-report"></a>Per definire una connessione dati e l'oggetto DataTable aggiungendo un oggetto DataSet (per il report figlio)  
  
1.  Scegliere **Aggiungi nuovo elemento**dal menu **sito Web** .  
  
2.  Nella finestra di dialogo **Aggiungi nuovo elemento** fare clic su **set di dati** e quindi su **Aggiungi**. Quando richiesto, è necessario aggiungere l'elemento alla cartella **App_Code** facendo clic su **Sì**.  
  
     Verrà aggiunto un nuovo file XSD **DataSet2.xsd** al progetto e verrà aperto Progettazione DataSet.  
  
3.  Dalla finestra della casella degli strumenti trascinare un controllo **TableAdapter** nell'area di progettazione. Viene avviata la configurazione guidata **TableAdapter** .  
  
4.  Nella pagina **scegliere la connessione dati** fare clic su **nuova connessione**.  
  
5.  Nella finestra di dialogo **Aggiungi connessione** effettuare i passaggi seguenti:  
  
    1.  Nella casella **nome server** immettere il server in cui si trova il database **AdventureWorks2008** .  
  
         L'istanza predefinita di SQL Server Express è **(local)\sqlexpress**.  
  
    2.  Nella sezione **Accesso al server** selezionare l'opzione di accesso ai dati. **Usa autenticazione di Windows** è l'impostazione predefinita.  
  
    3.  Nell'elenco **a discesa selezionare o immettere un nome di database** fare clic su **AdventureWorks2008**.  
  
    4.  Fare clic su **OK** e quindi su **Avanti**.  
  
6.  Se è stato selezionato **Usa autenticazione di SQL Server** nel passaggio 5 (b), selezionare l'opzione per includere i dati sensibili nella stringa o per impostare le informazioni nel codice dell'applicazione.  
  
7.  Nella pagina **Salva stringa di connessione nel file di configurazione dell'applicazione** Digitare il nome per la stringa di connessione o accettare l'impostazione predefinita **AdventureWorks2008ConnectionString**. Fare clic su **Avanti**.  
  
8.  Nella pagina **scegliere un tipo di comando** selezionare **Usa istruzioni SQL**e quindi fare clic su **Avanti**.  
  
9. Nella pagina **immettere un'istruzione SQL** immettere la query Transact-SQL seguente per recuperare i dati dal database **AdventureWorks2008** e quindi fare clic su **Avanti**.  
  
    ```  
    SELECT PurchaseOrderID, PurchaseOrderDetailID, OrderQty, ProductID, ReceivedQty, RejectedQty, StockedQty FROM Purchasing.PurchaseOrderDetail  
    ```  
  
     È anche possibile creare la query facendo clic su **Generatore di query**, quindi verificare la query facendo clic sul pulsante **Esegui query** . Se non vengono restituiti i dati previsti dalla query, è possibile che si stia utilizzando una versione precedente di AdventureWorks. Per ulteriori informazioni sull'installazione della versione **AdventureWorks2008** di AdventureWorks, vedere [procedura dettagliata: installazione del database AdventureWorks](https://msdn.microsoft.com/library/aa992075\(v=vs.100\).aspx).  
  
10. Nella pagina **scegliere i metodi per la generazione** deselezionare **Crea metodi per inviare aggiornamenti direttamente al database (GenerateDBDirectMethods)** e quindi fare clic su **fine**.  
  
     A questo punto è stata completata la configurazione di ADO.NET [DataTable](https://msdn.microsoft.com/library/system.data.datatable\(v=vs.100\).aspx) come origine dati per il report. Nella pagina Progettazione DataSet in Visual Studio si dovrebbe visualizzare l'oggetto **DataTable** aggiunto, con le colonne specificate nella query. In DataSet2 sono inclusi i dati della tabella PurhcaseOrderDetail, basati sulla query.  
  
11. Salvare il file.  
  
12. Per visualizzare l'anteprima dei dati, fare clic su **Anteprima dati** dal menu **dati** e quindi fare clic su **Anteprima**.  
  
## <a name="next-task"></a>Attività successiva  
 È stata creata correttamente una connessione dati e una tabella di dati per il report figlio. Successivamente, verrà progettato il report figlio utilizzando la Creazione guidata report.  
  
  
