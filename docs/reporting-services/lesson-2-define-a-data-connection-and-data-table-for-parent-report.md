---
title: 'Lesson 2: Define a Data Connection and Data Table for Child Report (Lezione 2: Definire una connessione dati e una tabella dati per il report padre) | Microsoft Docs'
description: Informazioni su come creare una connessione dati e una tabella dati per il report padre dopo aver creato un nuovo progetto di sito Web usando il modello di sito Web ASP.NET per Visual C#.
ms.date: 05/18/2016
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
ms.assetid: f02dee0c-85ad-45d4-b707-10e9e8541db9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 26599029af2b4fd6a52e85dc9b7567e9a7152038
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/28/2020
ms.locfileid: "87235657"
---
# <a name="lesson-2-define-a-data-connection-and-data-table-for-parent-report"></a>Lezione 2: Definire una connessione dati e una tabella di dati per il report padre
Dopo aver creato un nuovo progetto di sito Web utilizzando il modello di sito Web ASP.NET per Visual C#, il passaggio successivo consiste nel creare una connessione dati e una tabella di dati per il report padre. In questa esercitazione la connessione dati è al database AdventureWorks2014.  
  
## <a name="to-define-a-data-connection-and-data-table-by-adding-a-dataset-for-parent-report"></a>Per definire una connessione dati e l'oggetto DataTable aggiungendo un oggetto DataSet (per il report padre)  
  
1.  Selezionare **Aggiungi nuovo elemento** dal menu **Sito Web**.  
  
2.  Nella finestra di dialogo **Aggiungi nuovo elemento** selezionare **DataSet** e scegliere **Aggiungi**. Quando richiesto, è necessario aggiungere l'elemento alla cartella **App_Code** selezionando **Sì**.  
  
    Verrà aggiunto un nuovo file XSD **DataSet1.xsd** al progetto e verrà aperto Progettazione DataSet.  
  
3.  Dalla finestra della casella degli strumenti trascinare un controllo **[TableAdapter](/visualstudio/data-tools/fill-datasets-by-using-tableadapters)** nell'area di progettazione. Viene avviata la configurazione guidata **TableAdapter** .  
  
4.  Nella pagina **Seleziona connessione dati** fare clic su **Nuova connessione**.  
  
5.  Se si tratta della prima creazione di un'origine dati in Visual Studio, viene visualizzata la pagina **Scegli origine dati**. Nella casella **Origine dati** selezionare **Microsoft SQL Server**.  
  
6.  Nella finestra di dialogo **Aggiungi connessione** effettuare i passaggi seguenti:  
  
    1.  Nella casella **Nome server** immettere il server in cui si trova il database **AdventureWorks2014** .  
  
        L'istanza predefinita di SQL Server Express è **(local)\sqlexpress**.  
  
    2.  Nella sezione **Accesso al server** selezionare l'opzione di accesso ai dati. **Usa autenticazione di Windows** è l'impostazione predefinita.  
  
    3.  Nell'elenco a discesa **Selezionare o immettere un nome di database** selezionare **AdventureWorks2014**.  
  
    4.  Selezionare **OK**, quindi **Avanti**.  
  
7.  Se è stata selezionata l'opzione **Usa autenticazione di SQL Server** nel Passaggio 6 (b), selezionare l'opzione per includere i dati sensibili nella stringa o per impostare le informazioni nel codice dell'applicazione.  
  
8.  Nella pagina **Salva stringa di connessione nel file di configurazione dell'applicazione** digitare il nome per la stringa di connessione o accettare l'impostazione predefinita **AdventureWorks2014ConnectionString**. Selezionare **Avanti**.  
  
9. Nella pagina **Seleziona un tipo di comando** selezionare **Usa istruzioni SQL**e quindi fare clic su **Avanti**.  
  
10. Nella pagina **Immettere un'istruzione SQL** immettere la seguente query Transact-SQL per recuperare i dati dal database **AdventureWorks2014** e quindi fare clic su **Avanti**.  
  
    ```  
    SELECT ProductID, Name, ProductNumber, SafetyStockLevel, ReorderPoint FROM  Production.Product Order By ProductID  
    ```  
  
    È anche possibile creare la query facendo clic su **Generatore di query**e, successivamente, verificare la query facendo clic su **Esegui query**. Se non vengono restituiti i dati previsti dalla query, è possibile che si stia utilizzando una versione precedente di AdventureWorks. Per altre informazioni su come ottenere il database di esempio **AdventureWorks2014**, vedere [Database di esempio AdventureWorks](https://github.com/Microsoft/sql-server-samples/releases).  
  
11. Nella pagina **Scegliere i metodi per generare** assicurarsi di deselezionare **Crea metodi per inviare aggiornamenti direttamente al database (GenerateDBDirectMethods)** e quindi fare clic su **Fine**.  
  
    > [!WARNING]  
    > Assicurarsi di deselezionare **Crea metodi per inviare aggiornamenti direttamente al database (GenerateDBDirectMethods)**  
  
    È stata completata la configurazione dell'oggetto DataTable di ADO.NET come origine dati del report. Nella pagina Progettazione DataSet in Visual Studio si dovrebbe visualizzare l'oggetto DataTable aggiunto, con le colonne specificate nella query. In DataSet1 sono inclusi i dati della tabella Product, basati sulla query.  
  
12. Salvare il file.  
  
13. Per visualizzare un'anteprima dei dati, scegliere **Anteprima dati** dal menu **Dati** e quindi fare clic su **Anteprima**.  
  
## <a name="next-task"></a>Attività successiva  
È stata creata correttamente una connessione dati e una tabella di dati per il report padre. Successivamente, verrà progettato il report padre utilizzando la Creazione guidata report. Vedere [Lezione 3: Progettare il report padre tramite la Creazione guidata report](../reporting-services/lesson-3-design-the-parent-report-using-the-report-wizard.md).  
  

