---
description: "Passaggio 5: Testare il pacchetto creato nella lezione 4 dell'esercitazione"
title: "Passaggio 5: Testare il pacchetto creato nella lezione 4 dell'esercitazione | Microsoft Docs"
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 5f18df92-0248-4858-836b-c8b02f0e0439
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ccd458d09c43a97693c620b9498ad1d593751905
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88457136"
---
# <a name="lesson-4-5-test-the-lesson-4-package"></a>Lezione 4-5: Testare il pacchetto della lezione 4

[!INCLUDE[sqlserver-ssis](../includes/applies-to-version/sqlserver-ssis.md)]



In fase di esecuzione, il file danneggiato **Currency_BAD.txt** non è in grado di generare una corrispondenza all'interno della trasformazione Lookup Currency Key. Dato che l'output degli errori di Lookup Currency Key è stato configurato per il reindirizzamento delle righe con esito negativo alla nuova destinazione Failed Rows, il componente non presenta errori e il pacchetto viene eseguito correttamente. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] riporta tutte le righe di errore nel file **ErrorOutput.txt**.  
  
In questa attività viene eseguito il test della configurazione dell'output degli errori modificata tramite l'esecuzione del pacchetto. Al termine dell'esecuzione corretta del pacchetto è possibile visualizzare il contenuto del file **ErrorOutput.txt**.  
  
> [!NOTE]  
> Per evitare l'accumulo di righe di errore nel file **ErrorOutput.txt**, eliminare manualmente il contenuto del file dopo l'esecuzione di ogni pacchetto.  
  
## <a name="check-the-package-layout"></a>Verificare il layout del pacchetto  
Prima di testare il pacchetto, verificare che il flusso di controllo e il flusso di dati nel pacchetto della lezione 4 siano simili alle figure seguenti: 
  
**Flusso di controllo**  
  
![Flusso di controllo nel pacchetto](../integration-services/media/task4lesson2control.gif "Flusso di controllo nel pacchetto")  
  
**Flusso di dati**  
  
![Flusso di dati nel pacchetto](../integration-services/media/task5lesson5data.gif "Flusso di dati nel pacchetto")  
  
## <a name="run-the-lesson-4-tutorial-package"></a>Eseguire il pacchetto creato nella lezione 4 dell'esercitazione  
  
1.  Scegliere **Avvia debug** dal menu **Debug**.  
  
2.  Al termine dell'esecuzione del pacchetto, selezionare **Arresta debug** dal menu **Debug**.  
  
## <a name="view-the-contents-of-the-erroroutputtxt-file"></a>Verificare il contenuto del file ErrorOutput.txt  
  
Aprire il file **ErrorOutput.txt** in Blocco note o qualsiasi altro editor di testo. L'ordine predefinito delle colonne è: AverageRate, CurrencyID, CurrencyDate, EndOfDateRate, ErrorCode, ErrorColumn, ErrorDescription.  
 
Tutte le righe nel file contengono il valore "BAD" per il CurrencyID privo di corrispondenza, il valore -1071607778 per ErrorCode, il valore 0 per ErrorColumn e il valore "Nessuna corrispondenza per la riga durante le ricerca" per ErrorDescription. Il valore di ErrorColumn è 0 perché l'errore non è specifico per la colonna, mentre l'operazione di ricerca non è riuscita.
  
  
## <a name="next-lesson"></a>Lezione successiva
[Lezione 5: Aggiungere configurazioni del pacchetto SSIS per il modello di distribuzione del pacchetto](../integration-services/lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md)  
