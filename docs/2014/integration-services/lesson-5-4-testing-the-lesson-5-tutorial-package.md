---
title: "Passaggio 4: Test del pacchetto dell'esercitazione della lezione 5 | Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 5215b77d-c2ec-4b25-a3de-ca49ea197d74
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 29154120646f74da7471f44a1630b3d99afefa4f
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52747483"
---
# <a name="step-4-testing-the-lesson-5-tutorial-package"></a>Passaggio 4: Test del pacchetto creato nell'esercitazione della lezione 5
  In fase di esecuzione, il pacchetto ottiene il valore della proprietà `Directory` da una variabile aggiornata in fase di esecuzione, anziché utilizzare il nome della directory originale specificato quando è stato creato il pacchetto. Il valore della variabile è popolato dal file SSISTutorial.dtsConfig file.  
  
 Per verificare che il pacchetto esegua l'aggiornamento della proprietà Directory con il nuovo valore in fase di esecuzione, eseguire semplicemente il pacchetto. Poiché solo tre file di dati di esempio sono stati copiati nella nuova directory, il flusso di dati verrà eseguito solo tre volte anziché essere reiterato nei 14 file della cartella originale.  
  
## <a name="checking-the-package-layout"></a>Verifica del layout del pacchetto  
 Prima di testare il pacchetto è consigliabile verificare che il flusso di controllo e il flusso di dati nel pacchetto della lezione 5 contengano gli oggetti visualizzati nelle figure seguenti. Il flusso di controllo deve essere identico a quello nella lezione 4. Il flusso di dati deve essere identico a quello nella lezione 4.  
  
 **Flusso di controllo**  
  
 ![Flusso di controllo nel pacchetto](../../2014/tutorials/media/task4lesson2control.gif "Flusso di controllo nel pacchetto")  
  
 **Flusso di dati**  
  
 ![Flusso di dati nel pacchetto](../../2014/tutorials/media/task9lesson1data.gif "Flusso di dati nel pacchetto")  
  
### <a name="to-test-the-lesson-5-tutorial-package"></a>Per testare il pacchetto creato nella lezione 5 dell'esercitazione  
  
1.  Scegliere **Avvia debug** dal menu **Debug**.  
  
2.  Al termine dell'esecuzione del pacchetto, scegliere **Arresta debug** dal menu **Debug**.  
  
## <a name="next-lesson"></a>Lezione successiva  
 [Lezione 6: Utilizzo di parametri con il modello di distribuzione](../integration-services/lesson-6-using-parameters-with-the-project-deployment-model-in-ssis.md)  
  
  
