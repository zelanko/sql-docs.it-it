---
title: 'Lezione 4: Definire una connessione dati e un tabella di dati per il Report figlio | Microsoft Docs'
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
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/23/2019
ms.locfileid: "66108470"
---
# <a name="lesson-4-define-a-data-connection-and-data-table-for-child-report"></a>Lezione 4: Definire una connessione dati e una tabella di dati per il report figlio
  Dopo aver progettato il report padre, il passaggio successivo consiste nel creare una connessione dati e una tabella di dati per il report figlio. In questa esercitazione la connessione dati è al database AdventureWorks2008. È anche possibile scegliere di connettersi al database AdventureWorks2012.  
  
### <a name="to-define-a-data-connection-and-datatable-by-adding-a-dataset-for-child-report"></a>Per definire una connessione dati e l'oggetto DataTable aggiungendo un oggetto DataSet (per il report figlio)  
  
1.  Nel **sito Web** menu, fare clic su **Aggiungi nuovo elemento**.  
  
2.  Nel **Aggiungi nuovo elemento** finestra di dialogo, fare clic su **set di dati** e quindi fare clic su **Add**. Quando richiesto, è necessario aggiungere l'elemento per il **App_Code** cartella facendo **Sì**.  
  
     Verrà aggiunto un nuovo file XSD **DataSet2.xsd** al progetto e verrà aperto Progettazione DataSet.  
  
3.  Dalla finestra della casella degli strumenti trascinare un controllo **TableAdapter** nell'area di progettazione. Viene avviata la configurazione guidata **TableAdapter** .  
  
4.  Nel **Seleziona connessione dati** pagina, fare clic su **nuova connessione**.  
  
5.  Nella finestra di dialogo **Aggiungi connessione** effettuare i passaggi seguenti:  
  
    1.  Nel **nome Server** casella, immettere il server in cui le **AdventureWorks2008** trova il database.  
  
         L'istanza predefinita di SQL Server Express è **(local)\sqlexpress**.  
  
    2.  Nella sezione **Accesso al server** selezionare l'opzione di accesso ai dati. **Usa autenticazione di Windows** è l'impostazione predefinita.  
  
    3.  Dal **selezionare o immettere un nome di database** elenco a discesa, fare clic su **AdventureWorks2008**.  
  
    4.  Fare clic su **OK**e quindi su **Avanti**.  
  
6.  Se è stato selezionato **Usa autenticazione di SQL Server** nel passaggio 5 (b), selezionare l'opzione per includere i dati sensibili nella stringa o per impostare le informazioni nel codice dell'applicazione.  
  
7.  Nel **Salva stringa di connessione nel file di configurazione dell'applicazione** pagina, digitare il nome della stringa di connessione o accettare il valore predefinito **AdventureWorks2008ConnectionString**. Scegliere **Avanti**.  
  
8.  Nel **scegliere un tipo di comando** pagina, selezionare **Usa istruzioni SQL**e quindi fare clic su **Next**.  
  
9. Nel **immettere un'istruzione SQL** pagina, immettere la query Transact-SQL seguente per recuperare i dati dalle **AdventureWorks2008** del database e quindi fare clic su **Avanti**.  
  
    ```  
    SELECT PurchaseOrderID, PurchaseOrderDetailID, OrderQty, ProductID, ReceivedQty, RejectedQty, StockedQty FROM Purchasing.PurchaseOrderDetail  
    ```  
  
     È anche possibile creare la query facendo clic **generatore di Query**, quindi verificare la query facendo clic **Esegui Query** pulsante. Se non vengono restituiti i dati previsti dalla query, è possibile che si stia utilizzando una versione precedente di AdventureWorks. Per altre informazioni sull'installazione di **AdventureWorks2008** versione di AdventureWorks, vedere [procedura dettagliata: Installazione del Database AdventureWorks](https://msdn.microsoft.com/library/aa992075\(v=vs.100\).aspx).  
  
10. Nel **scegliere i metodi per generare** pagina, deselezionare **Crea metodi per inviare aggiornamenti direttamente al database (GenerateDBDirectMethods)**, quindi fare clic su **fine**.  
  
     È stata completata la configurazione ADO.NET [DataTable](https://msdn.microsoft.com/library/system.data.datatable\(v=vs.100\).aspx) come origine dati del report. Nella pagina Progettazione DataSet in Visual Studio si dovrebbe visualizzare l'oggetto **DataTable** aggiunto, con le colonne specificate nella query. In DataSet2 sono inclusi i dati della tabella PurhcaseOrderDetail, basati sulla query.  
  
11. Salvare il file.  
  
12. Per visualizzare in anteprima i dati, fare clic su **i dati di anteprima** nel **Data** menu e quindi fare clic su **anteprima**.  
  
## <a name="next-task"></a>Attività successiva  
 È stata creata correttamente una connessione dati e una tabella di dati per il report figlio. Successivamente, verrà progettato il report figlio utilizzando la Creazione guidata report.  
  
  
