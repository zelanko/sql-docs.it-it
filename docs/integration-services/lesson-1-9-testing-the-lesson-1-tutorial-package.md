---
title: "Passaggio 9: Testare il pacchetto creato nella lezione 1 dell'esercitazione | Microsoft Docs"
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 9aee7acf-797b-46f2-830d-80ab64a9f0b6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: dde0ffe53ab5763230cafa752d687ab42d3a60c5
ms.sourcegitcommit: dd794633466b1da8ead9889f5e633bdf4b3389cd
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54143221"
---
# <a name="lesson-1-9-test-the-lesson-1-package"></a>Lezione 1-9: Testare il pacchetto della lezione 1

In questa esercitazione verranno effettuate le attività seguenti:  
  
-   Creazione di un nuovo progetto [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
-   Configurazione delle gestioni connessioni necessarie al pacchetto per connettersi ai dati di origine e di destinazione.  
  
-   Aggiunta di un flusso di dati che preleva i dati da un'origine file flat, esegue le necessarie trasformazioni Ricerca sui dati e configura i dati per la destinazione.  
  
Il pacchetto è ora completo e pronto per essere testato.
  
## <a name="check-the-package-components"></a>Controllare i componenti del pacchetto
  
Prima di testare il pacchetto, verificare che il flusso di controllo e il flusso di dati nel pacchetto della lezione 1 contengano gli oggetti visualizzati nelle figure seguenti.  
  
**Flusso di controllo** 
  
![Flusso di controllo nel pacchetto](../integration-services/media/task9lesson1control.gif "Flusso di controllo nel pacchetto")  
  
**Flusso di dati**  
  
![Flusso di dati nel pacchetto](../integration-services/media/task9lesson1data.gif "Flusso di dati nel pacchetto")  
  
## <a name="run-the-lesson-1-package"></a>Eseguire il pacchetto della lezione 1  
  
1.  Selezionare **Avvia debug** dal menu **Debug**.  
  
    Il pacchetto viene eseguito e vengono aggiunte 1.097 righe alla tabella dei fatti **NewFactCurrencyRate** in **AdventureWorksDW2012**. Per verificare questo risultato, selezionare la scheda **Flusso di dati**.
  
2.  Al termine dell'esecuzione del pacchetto, selezionare **Arresta debug** dal menu **Debug**.  
  
## <a name="go-to-next-lesson"></a>Passare alla lezione successiva
[Lezione 2: Aggiungere cicli con SSIS](../integration-services/lesson-2-adding-looping-with-ssis.md)  
  
## <a name="see-also"></a>Vedere anche  
[Esecuzione di progetti e pacchetti](packages/run-integration-services-ssis-packages.md) 
  
  
  
