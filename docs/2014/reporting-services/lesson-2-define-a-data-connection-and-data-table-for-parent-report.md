---
title: 'Lesson 2: Define a Data Connection and Data Table for Child Report (Lezione 2: Definire una connessione dati e una tabella dati per il report padre) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
ms.assetid: f02dee0c-85ad-45d4-b707-10e9e8541db9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 987e6924fe3fbffb416e4266861ae7cfede16596
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66108500"
---
# <a name="lesson-2-define-a-data-connection-and-data-table-for-parent-report"></a>Lezione 2: Definire una connessione dati e una tabella di dati per il report padre
  Dopo aver creato un nuovo progetto di sito Web utilizzando il modello di sito Web ASP.NET per Visual C#, il passaggio successivo consiste nel creare una connessione dati e una tabella di dati per il report padre. In questa esercitazione la connessione dati è al database AdventureWorks2008. È anche possibile scegliere di connettersi al database AdventureWorks2012.  
  
### <a name="to-define-a-data-connection-and-data-table-by-adding-a-dataset-for-parent-report"></a>Per definire una connessione dati e l'oggetto DataTable aggiungendo un oggetto DataSet (per il report padre)  
  
1.  Selezionare **Aggiungi nuovo elemento** dal menu **Sito Web**.  
  
2.  Nella finestra di dialogo **Aggiungi nuovo elemento** selezionare **DataSet** , quindi fare clic su **Aggiungi**. Quando richiesto, è necessario aggiungere l'elemento alla cartella **App_Code** facendo clic su **Sì**.  
  
     Verrà aggiunto un nuovo file XSD **DataSet1.xsd** al progetto e verrà aperto Progettazione DataSet.  
  
3.  Dalla finestra della casella degli strumenti trascinare un controllo **[TableAdapter](https://msdn.microsoft.com/library/bz9tthwx\(v=vs.100\).aspx)** nell'area di progettazione. Viene avviata la configurazione guidata **TableAdapter** .  
  
4.  Nella pagina **scegliere la connessione dati** fare clic su **nuova connessione**.  
  
5.  Se è la prima volta che si crea un'origine dati in Visual Studio, verrà visualizzata la pagina **Scegli origine dati** . Nella casella **Origine dati** selezionare **Microsoft SQL Server**.  
  
6.  Nella finestra di dialogo **Aggiungi connessione** effettuare i passaggi seguenti:  
  
    1.  Nella casella **nome server** immettere il server in cui si trova il database **AdventureWorks2008** .  
  
         L'istanza predefinita di SQL Server Express è **(local)\sqlexpress**.  
  
    2.  Nella sezione **Accesso al server** selezionare l'opzione di accesso ai dati. **Usa autenticazione di Windows** è l'impostazione predefinita.  
  
    3.  Nell'elenco **a discesa selezionare o immettere un nome di database** fare clic su **AdventureWorks2008**.  
  
    4.  Fare clic su **OK** e quindi su **Avanti**.  
  
7.  Se è stata selezionata l'opzione **Usa autenticazione di SQL Server** nel Passaggio 6 (b), selezionare l'opzione per includere i dati sensibili nella stringa o per impostare le informazioni nel codice dell'applicazione.  
  
8.  Nella pagina **Salva stringa di connessione nel file di configurazione dell'applicazione** Digitare il nome per la stringa di connessione o accettare l'impostazione predefinita **AdventureWorks2008ConnectionString**. Fare clic su **Avanti**.  
  
9. Nella pagina **scegliere un tipo di comando** selezionare **Usa istruzioni SQL**e quindi fare clic su **Avanti**.  
  
10. Nella pagina **immettere un'istruzione SQL** immettere la query Transact-SQL seguente per recuperare i dati dal database **AdventureWorks2008** e quindi fare clic su **Avanti**.  
  
    ```  
    SELECT ProductID, Name, ProductNumber, SafetyStockLevel, ReorderPoint FROM  Production.Product Order By ProductID  
    ```  
  
     È anche possibile creare la query facendo clic su **Generatore di query**, quindi verificare la query facendo clic su **Esegui query**. Se non vengono restituiti i dati previsti dalla query, è possibile che si stia utilizzando una versione precedente di AdventureWorks. Per ulteriori informazioni sull'installazione della versione **AdventureWorks2008** di AdventureWorks, vedere [procedura dettagliata: installazione del database AdventureWorks](https://msdn.microsoft.com/library/aa992075\(v=vs.100\).aspx).  
  
11. Nella pagina **scegliere i metodi per generare** assicurarsi di deselezionare **Crea metodi per inviare aggiornamenti direttamente al database (GenerateDBDirectMethods)**, quindi fare clic su **fine**.  
  
    > [!WARNING]  
    >  Assicurarsi di deselezionare l'opzione di creazione.  
  
     È stata completata la configurazione dell'oggetto DataTable di ADO.NET come origine dati del report. Nella pagina Progettazione DataSet in Visual Studio si dovrebbe visualizzare l'oggetto DataTable aggiunto, con le colonne specificate nella query. In DataSet1 sono inclusi i dati della tabella Product, basati sulla query.  
  
12. Salvare il file.  
  
13. Per visualizzare l'anteprima dei dati, fare clic su **Anteprima dati** dal menu **dati** e quindi fare clic su **Anteprima**.  
  
## <a name="next-task"></a>Attività successiva  
 È stata creata correttamente una connessione dati e una tabella di dati per il report padre. Successivamente, verrà progettato il report padre utilizzando la Creazione guidata report.  
  
  
