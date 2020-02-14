---
title: 'Passaggio 4: Distribuire il pacchetto della lezione 6 | Microsoft Docs'
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: b613cef7-7993-4d89-a429-a8251d74d435
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 2a16cd38eef12584f8d876e610bfda5d602c3076
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "71283019"
---
# <a name="lesson-6-4-deploy-the-lesson-6-package"></a>Lezione 6-4: Distribuire il pacchetto della lezione 6

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



La distribuzione del pacchetto implica l'aggiunta del pacchetto al catalogo SSISDB in [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] in un'istanza di SQL Server. In questa lezione vengono illustrate le procedure per aggiungere il pacchetto creato nella lezione 6 al catalogo SSISDB, impostare il nuovo parametro ed eseguire il pacchetto. Per questa lezione viene usato SQL Server Management Studio per aggiungere il pacchetto della lezione 6 al catalogo SSISDB e distribuire il pacchetto. Dopo avere distribuito il pacchetto, modificare il parametro in modo da puntare a un nuovo percorso e quindi eseguire il pacchetto.   
In questa attività:  

1. Aggiungere il pacchetto al catalogo SSISDB nel nodo SSIS in SQL Server.  
  
2. Distribuire il pacchetto.  
  
3. Impostare il valore di parametro del pacchetto.  

4. Eseguire il pacchetto in SSMS.  
  
## <a name="locate-or-add-the-ssisdb-catalog"></a>Individuare o aggiungere il catalogo SSISDB  
  
1.  Selezionare **Start** > **Tutti i programmi** > **Microsoft SQL Server 2017** e quindi selezionare **SQL Management Studio**.  
  
2.  Nella finestra di dialogo **Connetti al server** verificare le impostazioni predefinite e quindi selezionare **Connetti**. Per eseguire la connessione, è necessario che il **nome** del server sia il nome del computer in cui è installato SQL Server. Se il **motore di database** è un'istanza denominata, il nome nella casella **Server** deve essere il nome dell'istanza nel formato *\<nome_computer>\\\<nome_istanza>* . 
  
3.  In **Esplora oggetti** espandere **Cataloghi di Integration Services**.  
  
4.  Se in **Cataloghi di Integration Services** non è elencato alcun catalogo, aggiungere il catalogo SSISDB.  
  
5.  Per aggiungere il catalogo SSISDB, fare clic con il pulsante destro del mouse su **Cataloghi di Integration Services** e scegliere **Crea catalogo**.  
  
6.  Nella finestra di dialogo **Crea catalogo** selezionare **Abilita integrazione con CLR**.  
  
7.  Nella casella **Password** immettere una password e quindi digitarla nuovamente nella casella **Conferma password**. 
  
8.  Selezionare **OK** per aggiungere il catalogo SSISDB.  
  
## <a name="add-the-package-to-the-ssisdb-catalog"></a>Aggiungere il pacchetto al catalogo SSISDB  
  
1.  In **Esplora oggetti** fare clic con il pulsante destro del mouse su **SSISDB** e selezionare **Crea cartella**.  
  
2.  Nella finestra di dialogo **Crea cartella** immettere SSIS Tutorial nella casella Nome cartella e selezionare **OK**.  
  
3.  Espandere la cartella **SSIS Tutorial**, fare clic con il pulsante destro del mouse su **Progetti** e selezionare **Importa pacchetti**.  
  
4.  Nella **pagina introduttiva** della **Conversione guidata progetto di Integration Services** fare clic su **Avanti**.  
  
5.  Nella pagina **Individua pacchetti** verificare che sia selezionato **File system** nell'elenco **Origine**, quindi fare clic su **Sfoglia**.  
  
6.  Nella finestra di dialogo **Sfoglia cartella** passare alla cartella contenente il progetto SSIS Tutorial, quindi selezionare **OK**.  
  
7.  Selezionare **Avanti**.  
  
8.  Nella pagina Seleziona pacchetti vengono visualizzati tutti e sei i pacchetti di SSIS Tutorial. Nell'elenco **Pacchetti** selezionare **Lesson 6.dtsx**, quindi selezionare **Avanti**.  
  
9. Nella pagina **Seleziona destinazione** immettere **SSIS Tutorial Deployment** nella casella **Nome progetto** e quindi selezionare **Avanti**.

10. Selezionare **Avanti** in tutte le pagine rimanenti della procedura guidata finché non si giunge alla pagina **Verifica**.  
  
11. Nella pagina **Verifica** selezionare **Converti**.  
  
12. Al termine della conversione selezionare **Chiudi**.  
  
Quando si chiude la Conversione guidata progetto di Integration Services, SSIS visualizza la Distribuzione guidata Integration Services. Usare questa procedura guidata per distribuire il pacchetto della lezione 6.  
  
1.  Nella **pagina introduttiva** della **Distribuzione guidata Integration Services** verificare i passaggi per la distribuzione del progetto e quindi selezionare **Avanti**.  
  
2.  Nella pagina **Seleziona destinazione** verificare che il nome del server sia l'istanza di SQL Server che contiene il catalogo SSISDB e che il percorso indichi **SSIS Tutorial Deployment**, quindi selezionare **Avanti**.  
  
3.  Nella pagina **Verifica** rivedere il **riepilogo**, quindi selezionare **Distribuisci**.  
  
4.  Al termine della distribuzione selezionare **Chiudi**.  
  
5.  In **Esplora oggetti** fare clic con il pulsante destro del mouse su **Cataloghi di Integration Services** e selezionare **Aggiorna**.  
  
6.  Espandere **Cataloghi di Integration Services**, quindi **SSISDB**. Continuare a espandere l'albero in **SSIS Tutorial** finché non si espande tutto il progetto. Nel nodo **Pacchetti** del nodo **SSIS Tutorial Deployment** viene visualizzato **Lesson 6.dtsx**.  
  
7.  Per verificare che il pacchetto sia completo, fare clic con il pulsante destro del mouse su **Lesson 6.dtsx** e selezionare **Configura**. Nella finestra di dialogo **Configura** selezionare **Parametri** e verificare che siano indicati una voce con **Lesson 6.dtsx** come **Contenitore**, **VarFolderName** come **Nome** e il percorso di **New Sample Data** come valore, quindi selezionare **Chiudi**.  
  
## <a name="create-and-populate-a-new-sample-data-folder"></a>Creare e popolare una nuova cartella di dati di esempio  
  
1.  In **Esplora risorse** al livello di radice dell'unità, ad esempio **C:\\** , creare una cartella denominata **Sample Data Two**.  
  
2.  Aprire la cartella **Sample Data** riportata nei [prerequisiti della lezione 1](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites) e quindi copiare uno dei tre file di esempio.  
  
3.  Passare alla cartella **Sample Data Two** e incollare i file copiati.  
  
## <a name="change-the-package-parameter-to-point-to-the-new-sample-data"></a>Modificare il parametro del pacchetto in modo da fare riferimento ai nuovi dati di esempio  
  
1.  In **Esplora oggetti** fare clic con il pulsante destro del mouse su **Lesson 6.dtsx** e selezionare **Configura**.  
  
2.  Nella finestra di dialogo **Configura** modificare il valore del parametro in modo da puntare al percorso di **Sample Data Two**, ad esempio **C:\\Sample Data Two**.  
  
3.  Selezionare **OK** per chiudere la finestra di dialogo **Configura**.  
  
## <a name="test-the-lesson-6-package-deployment"></a>Testare la distribuzione del pacchetto della lezione 6  
  
1.  In **Esplora oggetti** fare clic con il pulsante destro del mouse su **Lesson 6.dtsx** e selezionare **Esegui**.  
  
2.  Nella finestra di dialogo **Esegui pacchetto** selezionare **OK**.  
  
3.  Nella finestra di dialogo del messaggio selezionare **Sì** per aprire il **report della panoramica**.  
  
Nel **report della panoramica** per il pacchetto sono visualizzati il nome del pacchetto e un riepilogo dello stato. La sezione **Panoramica sulle esecuzioni** illustra il risultato di ogni attività del pacchetto. La sezione **Parametri usati** contiene i nomi e i valori di tutti i parametri usati nell'esecuzione del pacchetto, compreso **VarFolderName**.  
  
