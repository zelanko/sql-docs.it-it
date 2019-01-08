---
title: 'Passaggio 2: Aggiunta e configurazione del contenitore ciclo Foreach | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 88a973cc-0f23-4ecf-adb6-5b06279c2df6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2aa42ac9ab25c9765aac2afa10abdd50f2df4cb7
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53360114"
---
# <a name="step-2-adding-and-configuring-the-foreach-loop-container"></a>Passaggio 2: Aggiunta e configurazione del contenitore Ciclo Foreach
  In questa attività verrà aggiunta la capacità di creare un ciclo in una cartella di file flat e applicare la stessa trasformazione del flusso di dati utilizzata nella lezione 1 a ognuno di questi file flat. Ciò si ottiene tramite l'aggiunta e la configurazione di un contenitore Ciclo Foreach al flusso di controllo.  
  
 Il contenitore Ciclo Foreach che si aggiunge deve essere in grado di collegarsi a ogni file flat della cartella. Dal momento che tutti i file della cartella hanno lo stesso formato, il contenitore Ciclo Foreach può utilizzare la stessa gestione connessione file flat per la connessione a tali file. La gestione connessione file flat utilizzata dal contenitore è la stessa creata nella lezione 1.  
  
 Al momento, la gestione connessione file flat della lezione 1 si connette a un solo file flat specifico. Per ottenere la connessione in modo iterativo a ogni file flat della cartella, sarà necessario configurare il contenitore Ciclo Foreach e la gestione connessione file flat come segue:  
  
-   **Contenitore ciclo foreach:** Il valore enumerato del contenitore verrà eseguito il mapping a una variabile di pacchetto definita dall'utente. Il contenitore utilizzerà poi questa variabile definita dall'utente per modificare in modo dinamico la proprietà `ConnectionString` della gestione connessione file flat e connettersi in modo iterativo a ogni file flat della cartella.  
  
-   **Gestione connessione File flat:** Si modificherà la gestione connessione che è stata creata nella lezione 1 usando una variabile definita dall'utente per popolare la gestione connessione `ConnectionString` proprietà.  
  
 Le procedure di questa attività mostrano come creare e modificare il contenitore Ciclo Foreach per utilizzare una variabile di pacchetto definita dall'utente ed aggiungere l'attività flusso di dati al ciclo. Si imparerà a modificare la gestione connessione file flat per utilizzare una variabile definita dall'utente nella successiva attività.  
  
 Dopo aver apportato tali modifiche al pacchetto, quando questo viene eseguito, il contenitore Ciclo Foreach si ripete attraverso la raccolta di dati nella cartella Sample Data. Ogni volta che viene individuato un file che corrisponde ai criteri, il contenitore Ciclo Foreach popola la variabile definita dall'utente con il nome file, esegue il mapping della variabile definita dall'utente alla proprietà `ConnectionString` della gestione connessione file flat SampleCurrency Data e quindi esegue il flusso di dati su tale file. Di conseguenza, in ogni iterazione del Ciclo Foreach, l'attività Flusso di dati consuma un file flat diverso.  
  
> [!NOTE]  
>  Dal momento che [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] separa il flusso di controllo dal flusso dei dati, i cicli aggiunti al flusso di controllo non richiedono la modifica del flusso di dati. Di conseguenza, non è necessario modificare il flusso di dati creato nella lezione 1.  
  
### <a name="to-add-a-foreach-loop-container"></a>Per aggiungere un contenitore Ciclo Foreach  
  
1.  In **SQL Server Data Tools**fare clic sulla scheda **Flusso di controllo** .  
  
2.  Nella **Casella degli strumenti SSIS**espandere **Contenitori**, quindi trascinare **Contenitore Ciclo Foreach** sulla superficie di progettazione della scheda **Flusso di controllo** .  
  
3.  Fare clic con il pulsante destro del mouse sul **Contenitore Ciclo Foreach** appena aggiunto e scegliere **Modifica**.  
  
4.  Nel **Editor ciclo Foreach** finestra di dialogo il **generali** pagina per **Name**, immettere `Foreach File in Folder`. Fare clic su **OK**.  
  
5.  Fare doppio clic il contenitore ciclo Foreach, fare clic su **delle proprietà**e nella finestra Proprietà verificare che il `LocaleID` è impostata su **inglese (Stati Uniti)**.  
  
### <a name="to-configure-the-enumerator-for-the-foreach-loop-container"></a>Per configurare l'enumeratore per il contenitore Ciclo Foreach  
  
1.  Fare doppio clic su Foreach File in Folder per riaprire l' **Editor ciclo Foreach**.  
  
2.  Fare clic su **Raccolta**.  
  
3.  Nella pagina **Raccolta** selezionare **Enumeratore Foreach File**.  
  
4.  Nel gruppo **Configurazione enumeratore** fare clic su **Sfoglia**.  
  
5.  Nella finestra di dialogo **Sfoglia per cartelle** individuare nel computer la cartella contenente i file Currency_*.txt.  
  
     Questi dati di esempio sono inclusi nei pacchetti di lezioni di [!INCLUDE[ssIS](../includes/ssis-md.md)] . Per scaricare i dati di esempio e i pacchetti di lezioni, effettuare le operazioni seguenti.  
  
    1.  Passare alla pagina relativa agli [esempi di prodotti di Integration Services](https://go.microsoft.com/fwlink/?LinkId=275027)  
  
    2.  Fare clic sulla scheda **DOWNLOADS** .  
  
    3.  Fare clic sul collegamento ipertestuale "http://msftisprodsamples.codeplex.com/downloads/get/578097" SQL2012. File Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip.  
  
6.  Nella casella **File** digitare **Currency_\*.txt**.  
  
### <a name="to-map-the-enumerator-to-a-user-defined-variable"></a>Per eseguire il mapping dell'enumeratore a una variabile definita dall'utente  
  
1.  Fare clic su **Mapping variabili**.  
  
2.  Nella colonna **Variabile** della pagina **Mapping variabili**, fare clic sulla cella vuota e selezionare **\<Nuova variabile...>**.  
  
3.  Nel **Aggiungi variabile** della finestra di dialogo per **Name**, tipo `varFileName`.  
  
    > [!IMPORTANT]  
    >  Per i nomi delle variabili viene fatta distinzione tra maiuscole e minuscole.  
  
4.  Fare clic su **OK**.  
  
5.  Fare di nuovo clic su **OK** per chiudere la finestra di dialogo **Editor ciclo Foreach** .  
  
### <a name="to-add-the-data-flow-task-to-the-loop"></a>Per aggiungere le attività flusso di dati al ciclo  
  
-   Trascinare il **Extract Sample Currency Data** attività flusso di dati nel contenitore ciclo Foreach ora ridenominato `Foreach File in Folder`.  
  
## <a name="next-lesson-task"></a>Attività della lezione successiva  
 [Passaggio 3: Modifica della gestione connessione File Flat](lesson-2-3-modifying-the-flat-file-connection-manager.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Configurare un contenitore Ciclo Foreach](control-flow/foreach-loop-container.md)   
 [Uso di variabili nei pacchetti](use-variables-in-packages.md)  
  
  
