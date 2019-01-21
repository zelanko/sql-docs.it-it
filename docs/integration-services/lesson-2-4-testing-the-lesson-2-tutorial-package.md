---
title: "Passaggio 4: Testare il pacchetto creato nella lezione 2 dell'esercitazione | Microsoft Docs"
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 0e8c0a25-8f79-41df-8ed2-f82a74b129cd
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2c17b7679a10d9273578c74dfa452b120ae2d87b
ms.sourcegitcommit: dd794633466b1da8ead9889f5e633bdf4b3389cd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54143201"
---
# <a name="lesson-2-4-test-the-lesson-2-tutorial-package"></a>Lezione 2-4: Testare il pacchetto creato nella lezione 2 dell'esercitazione

Dopo aver configurato il contenitore Ciclo Foreach e la gestione connessione file flat, il pacchetto creato nella lezione 2 consente di eseguire un'iterazione dei 14 file flat contenuti nella cartella Dati di esempio. Ogni volta che un nome di file corrisponde ai criteri specificati, il contenitore Ciclo Foreach popola la variabile definita dall'utente con il nome del file. Tale variabile aggiorna di conseguenza la proprietà ConnectionString della gestione connessione file flat, che stabilisce una connessione al nuovo file flat. Il contenitore Ciclo Foreach esegue quindi l'attività del flusso di dati non modificati sui dati del nuovo file flat.  
  
> [!NOTE]  
> Se si esegue il pacchetto della lezione 1, è necessario eliminare i record dalla tabella dbo.NewFactCurrencyRate nel database AdventureWorksDW2012 prima di eseguire il pacchetto da questa lezione. La lezione 2 tenta di inserire record già inseriti nella lezione 1, provocando un errore.  
  
## <a name="check-the-package-layout"></a>Verificare il layout del pacchetto  
Prima di testare il pacchetto, verificare che il flusso di controllo e il flusso di dati nel pacchetto della lezione 2 contengano gli oggetti visualizzati nelle figure seguenti. Il flusso di dati della lezione 2 è lo stesso della lezione 1.  
  
**Flusso di controllo**  
  
![Flusso di controllo nel pacchetto](../integration-services/media/task4lesson2control.gif "Flusso di controllo nel pacchetto")  
  
**Flusso di dati**  
  
![Flusso di dati nel pacchetto](../integration-services/media/task9lesson1data.gif "Flusso di dati nel pacchetto")  
  
## <a name="test-the-lesson-2-tutorial-package"></a>Testare il pacchetto creato nella lezione 2 dell'esercitazione  
  
1.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Lesson 2.dtsx** e selezionare **Esegui pacchetto**.  
  
    Il pacchetto viene eseguito. È possibile verificare lo stato di ogni ciclo nella finestra **Output** o facendo clic sulla scheda **Stato**. Ad esempio, viene evidenziato che sono state aggiunte 1097 righe alla tabella di destinazione dal file Currency_VEB.txt.  
  
2.  Al termine dell'esecuzione del pacchetto, selezionare **Arresta debug** dal menu **Debug**.  
  
## <a name="go-to-next-lesson"></a>Esecuzione del passaggio successivo  
[Lezione 3: Aggiungere la registrazione con SSIS](../integration-services/lesson-3-add-logging-with-ssis.md)  
  
## <a name="see-also"></a>Vedere anche  
[Esecuzione di progetti e pacchetti](../integration-services/packages/deploy-integration-services-ssis-projects-and-packages.md)  
  
  
  

