---
title: 'Passaggio 2: Aggiunta e configurazione del contenitore Ciclo Foreach | Microsoft Docs'
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 88a973cc-0f23-4ecf-adb6-5b06279c2df6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 492691c3fd6c8cd9206b591aa2302bc62a658daa
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52527135"
---
# <a name="lesson-2-2---adding-and-configuring-the-foreach-loop-container"></a>Lezione 2-2 - Aggiunta e configurazione del contenitore Ciclo Foreach
In questa attività verrà aggiunta la capacità di creare un ciclo in una cartella di file flat e applicare la stessa trasformazione del flusso di dati utilizzata nella lezione 1 a ognuno di questi file flat. Ciò si ottiene tramite l'aggiunta e la configurazione di un contenitore Ciclo Foreach al flusso di controllo.  
  
Il contenitore Ciclo Foreach che si aggiunge deve essere in grado di collegarsi a ogni file flat della cartella. Dal momento che tutti i file della cartella hanno lo stesso formato, il contenitore Ciclo Foreach può utilizzare la stessa gestione connessione file flat per la connessione a tali file. La gestione connessione file flat utilizzata dal contenitore è la stessa creata nella lezione 1.  
  
Al momento, la gestione connessione file flat della lezione 1 si connette a un solo file flat specifico. Per ottenere la connessione in modo iterativo a ogni file flat della cartella, sarà necessario configurare il contenitore Ciclo Foreach e la gestione connessione file flat come segue:  
  
-   **Contenitore Ciclo Foreach:** sul valore enumerato del contenitore verrà eseguito il mapping a una variabile di pacchetto definita dall'utente. Il contenitore userà poi questa variabile definita dall'utente per modificare in modo dinamico la proprietà **ConnectionString** della gestione connessione file flat e connettersi in modo iterativo a ogni file flat della cartella.  
  
-   **Gestione connessione file flat:** la gestione connessione creata nella lezione 1 verrà modificata usando una variabile definita dall'utente per popolare la proprietà **ConnectionString** di gestione connessione.  
  
Le procedure di questa attività mostrano come creare e modificare il contenitore Ciclo Foreach per utilizzare una variabile di pacchetto definita dall'utente ed aggiungere l'attività flusso di dati al ciclo. Si imparerà a modificare la gestione connessione file flat per utilizzare una variabile definita dall'utente nella successiva attività.  
  
Dopo aver apportato tali modifiche al pacchetto, quando questo viene eseguito, il contenitore Ciclo Foreach si ripete attraverso la raccolta di dati nella cartella Sample Data. Ogni volta che viene individuato un file che corrisponde ai criteri, il contenitore Ciclo Foreach popola la variabile definita dall'utente con il nome file, esegue il mapping della variabile definita dall'utente alla proprietà **ConnectionString** della gestione connessione file flat per i dati della valuta di esempio e quindi esegue il flusso di dati su tale file. Di conseguenza, in ogni iterazione del Ciclo Foreach, l'attività Flusso di dati consuma un file flat diverso.  
  
> [!NOTE]  
> Dal momento che [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] separa il flusso di controllo dal flusso dei dati, i cicli aggiunti al flusso di controllo non richiedono la modifica del flusso di dati. Di conseguenza, non è necessario modificare il flusso di dati creato nella lezione 1.  
  
### <a name="to-add-a-foreach-loop-container"></a>Per aggiungere un contenitore Ciclo Foreach  
  
1.  In **SQL Server Data Tools**fare clic sulla scheda **Flusso di controllo** .  
  
2.  Nella **Casella degli strumenti SSIS**espandere **Contenitori**, quindi trascinare **Contenitore Ciclo Foreach** sulla superficie di progettazione della scheda **Flusso di controllo** .  
  
3.  Fare clic con il pulsante destro del mouse sul **Contenitore Ciclo Foreach** appena aggiunto e scegliere **Modifica**.  
  
4.  Nella pagina **Generale** della finestra di dialogo **Editor ciclo Foreach** digitare **Foreach File in Folder**per **Nome**. Fare clic su **OK**.  
  
5.  Fare clic con il pulsante destro del mouse sul contenitore Ciclo Foreach, scegliere **Proprietà**e verificare che la proprietà **LocaleID** sia impostata su **Inglese (Stati Uniti)** nella finestra Proprietà.  
  
### <a name="to-configure-the-enumerator-for-the-foreach-loop-container"></a>Per configurare l'enumeratore per il contenitore Ciclo Foreach  
  
1.  Fare doppio clic su Foreach File in Folder per riaprire l' **Editor ciclo Foreach**.  
  
2.  Fare clic su **Raccolta**.  
  
3.  Nella pagina **Raccolta** selezionare **Enumeratore Foreach File**.  
  
4.  Nel gruppo **Configurazione enumeratore** fare clic su **Sfoglia**.  
  
5.  Nella finestra di dialogo **Sfoglia per cartelle** individuare nel computer la cartella contenente i file Currency_*.txt.  
  
    Questi dati di esempio sono inclusi nei pacchetti di lezioni di [!INCLUDE[ssIS](../includes/ssis-md.md)] . Per scaricare i dati di esempio e i pacchetti di lezioni, effettuare le operazioni seguenti.  
  
    1.  Passare alla pagina relativa agli [esempi di prodotti di Integration Services](https://go.microsoft.com/fwlink/?LinkId=275027). 
  
    2.  Fare clic sulla scheda **DOWNLOADS** .  
  
    3.  Fare clic sul collegamento per il file [SQL2012.Integration_Services.Create_Simple_ETL_Tutorial.Sample.zip](https://msftisprodsamples.codeplex.com/downloads/get/596031).  
  
6.  Nella casella **File** digitare **Currency_\*.txt**.  
  
### <a name="to-map-the-enumerator-to-a-user-defined-variable"></a>Per eseguire il mapping dell'enumeratore a una variabile definita dall'utente  
  
1.  Fare clic su **Mapping variabili**.  
  
2.  Nella colonna **Variabile** della pagina **Mapping variabili**, fare clic sulla cella vuota e selezionare **\<Nuova variabile...>**.  
  
3.  Nella finestra di dialogo **Aggiungi variabile** digitare **varFileName**per **Nome**.  
  
    > [!IMPORTANT]  
    > Per i nomi delle variabili viene fatta distinzione tra maiuscole e minuscole.  
  
4.  Fare clic su **OK**.  
  
5.  Fare di nuovo clic su **OK** per chiudere la finestra di dialogo **Editor ciclo Foreach** .  
  
### <a name="to-add-the-data-flow-task-to-the-loop"></a>Per aggiungere le attività flusso di dati al ciclo  
  
-   Trascinare l'attività flusso di dati **Extract Sample Currency Data** nel contenitore Ciclo Foreach ora ridenominato **Foreach File in Folder**.  
  
## <a name="next-lesson-task"></a>Attività della lezione successiva  
[Passaggio 3: Modifica della gestione connessione file flat](../integration-services/lesson-2-3-modifying-the-flat-file-connection-manager.md)  
  
## <a name="see-also"></a>Vedere anche  
[Configurazione di un contenitore Ciclo Foreach](https://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25)  
[Utilizzo di variabili nei pacchetti](https://msdn.microsoft.com/library/7742e92d-46c5-4cc4-b9a3-45b688ddb787)  
  
  
  
