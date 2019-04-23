---
title: 'Lezione 2: Definire una connessione dati e un tabella di dati per il Report padre | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: f02dee0c-85ad-45d4-b707-10e9e8541db9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: c6b7e6e38ca10cf23179872ddc3ff4476bc3657d
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/22/2019
ms.locfileid: "59939857"
---
# <a name="lesson-2-define-a-data-connection-and-data-table-for-parent-report"></a>Lezione 2: Definire una connessione dati e un tabella di dati per il Report padre
  Dopo aver creato un nuovo progetto di sito Web utilizzando il modello di sito Web ASP.NET per Visual C#, il passaggio successivo consiste nel creare una connessione dati e una tabella di dati per il report padre. In questa esercitazione la connessione dati è al database AdventureWorks2008. È anche possibile scegliere di connettersi al database AdventureWorks2012.  
  
### <a name="to-define-a-data-connection-and-data-table-by-adding-a-dataset-for-parent-report"></a>Per definire una connessione dati e l'oggetto DataTable aggiungendo un oggetto DataSet (per il report padre)  
  
1.  Selezionare **Aggiungi nuovo elemento** dal menu **Sito Web**.  
  
2.  Nel **Aggiungi nuovo elemento** finestra di dialogo **DataSet** e fare clic su **Add**. Quando richiesto è necessario aggiungere l'elemento per il **App_Code** cartella facendo **Sì**.  
  
     Verrà aggiunto un nuovo file XSD **DataSet1.xsd** al progetto e verrà aperto Progettazione DataSet.  
  
3.  Dalla finestra della casella degli strumenti trascinare un controllo **[TableAdapter](https://msdn.microsoft.com/library/bz9tthwx\(v=vs.100\).aspx)** nell'area di progettazione. Viene avviata la configurazione guidata **TableAdapter** .  
  
4.  Nel **Seleziona connessione dati** pagina, fare clic su **nuova connessione**.  
  
5.  Se si tratta della prima creazione di un'origine dati in Visual Studio, viene visualizzata la pagina **Scegli origine dati**. Nella casella **Origine dati** selezionare **Microsoft SQL Server**.  
  
6.  Nella finestra di dialogo **Aggiungi connessione** effettuare i passaggi seguenti:  
  
    1.  Nel **nome Server** casella, immettere il server in cui le **AdventureWorks2008** trova il database.  
  
         L'istanza predefinita di SQL Server Express è **(local)\sqlexpress**.  
  
    2.  Nella sezione **Accesso al server** selezionare l'opzione di accesso ai dati. **Usa autenticazione di Windows** è l'impostazione predefinita.  
  
    3.  Dal **selezionare o immettere un nome di database** elenco a discesa, fare clic su **AdventureWorks2008**.  
  
    4.  Fare clic su **OK**e quindi su **Avanti**.  
  
7.  Se è stata selezionata l'opzione **Usa autenticazione di SQL Server** nel Passaggio 6 (b), selezionare l'opzione per includere i dati sensibili nella stringa o per impostare le informazioni nel codice dell'applicazione.  
  
8.  Nel **Salva stringa di connessione nel file di configurazione dell'applicazione** pagina, digitare il nome della stringa di connessione o accettare il valore predefinito **AdventureWorks2008ConnectionString**. Scegliere **Avanti**.  
  
9. Nel **scegliere un tipo di comando** pagina, selezionare **Usa istruzioni SQL**e quindi fare clic su **Next**.  
  
10. Nel **immettere un'istruzione SQL** pagina, immettere la query Transact-SQL seguente per recuperare i dati dalle **AdventureWorks2008** del database e quindi fare clic su **Avanti**.  
  
    ```  
    SELECT ProductID, Name, ProductNumber, SafetyStockLevel, ReorderPoint FROM  Production.Product Order By ProductID  
    ```  
  
     È anche possibile creare la query facendo clic **generatore di Query**, quindi verificare la query facendo clic **Esegui Query**. Se non vengono restituiti i dati previsti dalla query, è possibile che si stia utilizzando una versione precedente di AdventureWorks. Per altre informazioni sull'installazione di **AdventureWorks2008** versione di AdventureWorks, vedere [procedura dettagliata: Installazione del Database AdventureWorks](https://msdn.microsoft.com/library/aa992075\(v=vs.100\).aspx).  
  
11. Nel **scegliere i metodi per generare** pagina, assicurarsi di deselezionare **Crea metodi per inviare aggiornamenti direttamente al database (GenerateDBDirectMethods)**, quindi fare clic su **fine**.  
  
    > [!WARNING]  
    >  Assicurarsi di deselezionare l'opzione di creazione.  
  
     È stata completata la configurazione dell'oggetto DataTable di ADO.NET come origine dati del report. Nella pagina Progettazione DataSet in Visual Studio si dovrebbe visualizzare l'oggetto DataTable aggiunto, con le colonne specificate nella query. In DataSet1 sono inclusi i dati della tabella Product, basati sulla query.  
  
12. Salvare il file.  
  
13. Per visualizzare in anteprima i dati, fare clic su **i dati di anteprima** nel **Data** menu e quindi fare clic su **anteprima**.  
  
## <a name="next-task"></a>Attività successiva  
 È stata creata correttamente una connessione dati e una tabella di dati per il report padre. Successivamente, verrà progettato il report padre utilizzando la Creazione guidata report.  
  
  
