---
title: 'Passaggio 4: Distribuzione del pacchetto della lezione 6 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: b613cef7-7993-4d89-a429-a8251d74d435
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 0e04a36ca687c57daae2f286025add57a32632c8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/25/2020
ms.locfileid: "62767333"
---
# <a name="step-4-deploying-the-lesson-6-package"></a>Passaggio 4: Distribuzione del pacchetto della lezione 6
  La distribuzione del pacchetto implica l'aggiunta del pacchetto al catalogo SSISDB in Integration Services in un'istanza di SQL Server. In questa lezione verranno illustrate le procedure per aggiungere il pacchetto creato nella lezione 6 al catalogo SSISDB, impostare il parametro ed eseguire il pacchetto. Per questa lezione verrà usato SQL Server Management Studio per aggiungere il pacchetto della lezione 6 al catalogo SSISDB e distribuire il pacchetto. Dopo avere distribuito il pacchetto, modificare il parametro in modo da puntare a un nuovo percorso, quindi eseguire il pacchetto.  
  
 In questa lezione verranno illustrate le procedure seguenti:  
  
-   Aggiungere il pacchetto al catalogo SSISDB nel nodo SSIS in SQL Server.  
  
-   Distribuire il pacchetto.  
  
-   Impostare il valore di parametro del pacchetto.  
  
-   Eseguire il pacchetto in SSMS.  
  
### <a name="to-locate-or-add-the-ssisdb-catalog"></a>Per individuare o aggiungere il catalogo SSISDB  
  
1.  Fare clic sul pulsante Start, scegliere Tutti i programmi, Microsoft SQL Server 2012, quindi fare clic su SQL Server Management Studio.  
  
2.  Nella finestra di dialogo Connetti al server verificare le impostazioni predefinite, quindi fare clic su Connetti. Per eseguire la connessione, è necessario che nella casella Nome server sia presente il nome del computer in cui è installato SQL Server. Se il motore di database è un'istanza denominata, nella casella Nome server deve essere contenuto anche il nome dell'istanza nel formato <nome_computer>\\<nome_istanza>.  
  
3.  In Esplora oggetti espandere Cataloghi di Integration Services.  
  
4.  Se in Cataloghi di Integration Services non è elencato alcun catalogo, aggiungere il catalogo SSISDB.  
  
5.  Per aggiungere il catalogo SSISDB, fare clic con il pulsante destro del mouse su Cataloghi di Integration Services e scegliere Crea catalogo.  
  
6.  Nella finestra di dialogo Crea catalogo selezionare Abilita integrazione con CLR.  
  
7.  Nella casella Password digitare una nuova password, quindi digitarla nuovamente nella casella Conferma password. Assicurarsi di ricordare la password digitata.  
  
8.  Fare clic su OK per aggiungere il catalogo SSISDB.  
  
### <a name="to-add-the-package-to-the-ssisdb-catalog"></a>Per aggiungere il pacchetto al catalogo SSISDB  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse su SSISDB, quindi scegliere Crea cartella.  
  
2.  Nella finestra di dialogo Crea cartella digitare SSIS Tutorial nella casella Nome cartella e fare clic su OK.  
  
3.  Espandere la cartella SSIS Tutorial, fare clic con il pulsante destro del mouse su Progetti e scegliere Importa pacchetti.  
  
4.  Nella pagina introduttiva della Conversione guidata progetto di Integration Services fare clic su Avanti.  
  
5.  Nella pagina Individua pacchetti verificare che sia selezionato File system nell'elenco Origine, quindi fare clic su Sfoglia.  
  
6.  Nella finestra di dialogo Sfoglia cartella selezionare la cartella contenente il progetto SSIS Tutorial, quindi fare clic su OK.  
  
7.  Scegliere Avanti.  
  
8.  Nella pagina Seleziona pacchetti verranno visualizzati tutti e sei i pacchetti di SSIS Tutorial. Nell'elenco Pacchetti selezionare Lesson 6.dtsx, quindi fare clic su Avanti.  
  
9. Nella pagina Seleziona destinazione digitare SSIS Tutorial Deployment nella casella Nome progetto, quindi fare clic su Avanti.  
  
10. Fare clic su Avanti in tutte le pagine rimanenti della procedura guidata finché non si giunge alla pagina Verifica.  
  
11. Nella pagina Verifica fare clic su Converti.  
  
12. Al termine della conversione fare clic su Chiudi.  
  
 Quando si chiude la Conversione guidata progetto di Integration Services, SSIS visualizza la Distribuzione guidata Integration Services. Usare questa procedura guidata per distribuire il pacchetto della lezione 6.  
  
1.  Nella pagina introduttiva della Distribuzione guidata Integration Services verificare i passaggi per la distribuzione del progetto, quindi fare clic su Avanti.  
  
2.  Nella pagina Seleziona destinazione verificare che il nome del server sia l'istanza di SQL Server che contiene il catalogo SSISDB e che il percorso mostri SSIS Tutorial Deployment, quindi fare clic su Avanti.  
  
3.  Nella pagina Verifica rivedere il riepilogo, quindi fare clic su Distribuisci.  
  
4.  Al termine della distribuzione fare clic su Chiudi.  
  
5.  In Esplora oggetti fare clic con il pulsante destro del mouse su Cataloghi di Integration Services e scegliere Aggiorna.  
  
6.  Espandere Cataloghi di Integration Services, quindi SSISDB. Continuare a espandere l'albero in SSIS Tutorial finché non si espande tutto il progetto. Nel nodo Pacchetti del nodo SSIS Tutorial Deployment verrà visualizzato Lesson 6.dtsx.  
  
 Per verificare che il pacchetto sia completo, fare clic con il pulsante destro del mouse su Lesson 6.dtsx e scegliere Configura. Nella finestra di dialogo Configura selezionare Parametri e verificare che sia presente una voce con Lesson 6.dtsx come Contenitore, VarFolderName come Nome e il percorso di New Sample Data come valore, quindi fare clic su Chiudi.  
  
 Prima di continuare, creare una nuova cartella di dati di esempio, denominarla Sample Data Two e copiarvi i tre file di esempio originali.  
  
### <a name="to-create-and-populate-a-new-sample-data-folder"></a>Per creare e popolare una nuova cartella di dati di esempio  
  
1.  In Esplora risorse al livello di radice dell'unità, ad esempio, C:\\, creare una nuova cartella denominata Sample Data Two.  
  
2.  Aprire la cartella c:\Programmi\Microsoft SQL Server\110\Samples\Integration Services\Tutorial\Creating a Simple ETL Package\Sample Data, quindi copiare i tre file di esempio dalla cartella.  
  
3.  Incollare i file copiati nella cartella New Sample Data.  
  
### <a name="to-change-the-package-parameter-to-point-to-the-new-sample-data"></a>Per modificare il parametro del pacchetto in modo da puntare ai nuovi dati di esempio  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse su Lesson 6.dtsx e scegliere Configura.  
  
2.  Nella finestra di dialogo Configura modificare il valore del parametro in modo da puntare al percorso di Sample Data Two. Ad esempio C:\Sample Data Two se la nuova cartella è stata posizionata nella cartella radice dell'unità C.  
  
3.  Fare clic su OK per chiudere la finestra di dialogo Configura.  
  
### <a name="to-test-the-lesson-6-package-deployment"></a>Per testare la distribuzione del pacchetto creato nella lezione 6  
  
1.  In Esplora oggetti fare clic con il pulsante destro del mouse su Lesson 6.dtsx e scegliere Esegui.  
  
2.  Nella finestra di dialogo Esegui pacchetto fare clic su OK.  
  
3.  Nella finestra di dialogo del messaggio fare clic su Sì per aprire il report della panoramica.  
  
 Verrà visualizzato il report della panoramica per il pacchetto in cui è presente il nome del pacchetto e un riepilogo dello stato. La sezione Panoramica sulle esecuzioni illustra il risultato di ogni attività nel pacchetto e la sezione Parametri usati mostra i nomi e i valori di tutti i parametri usati nell'esecuzione del pacchetto, compreso VarFolderName.  
  
  
