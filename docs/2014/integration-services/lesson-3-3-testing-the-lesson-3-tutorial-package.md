---
title: "Passaggio 3: Test del pacchetto dell'esercitazione della lezione 3 | Microsoft Docs"
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 1096a476-93cf-4474-86f5-27d6357eb380
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ac1aa0c45e8201d50ead862dd1631bbb3324c8e3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62891589"
---
# <a name="step-3-testing-the-lesson-3-tutorial-package"></a>Passaggio 3: Test del pacchetto creato nella lezione 3 dell'esercitazione
  In questa attività verrà eseguito il pacchetto Lesson 3.dtsx. Durante l'esecuzione del pacchetto, nella finestra Registra eventi verranno elencate le voci di log scritte nel file di log. Al termine dell'esecuzione del pacchetto sarà possibile verificare il contenuto del file di log generato dal provider di log.  
  
## <a name="checking-the-package-layout"></a>Verifica del layout del pacchetto  
 Prima di testare il pacchetto è consigliabile verificare che il flusso di controllo e il flusso di dati nel pacchetto della lezione 3 contengano gli oggetti visualizzati nelle figure seguenti. Il flusso di controllo deve essere identico a quello nella lezione 2. Il flusso di dati deve essere identico a quello nelle lezioni 1 e 2.  
  
 **Flusso di controllo**  
  
 ![Flusso di controllo nel pacchetto](../../2014/tutorials/media/task4lesson2control.gif "Flusso di controllo nel pacchetto")  
  
 **Flusso di dati**  
  
 ![Flusso di dati nel pacchetto](../../2014/tutorials/media/task9lesson1data.gif "Flusso di dati nel pacchetto")  
  
### <a name="to-run-the-lesson-4-tutorial-package"></a>Per eseguire il pacchetto creato nella lezione 4 dell'esercitazione  
  
1.  Scegliere Registra eventi dal menu SSIS.  
  
2.  Scegliere **Avvia debug** dal menu **Debug**.  
  
3.  Al termine dell'esecuzione del pacchetto, scegliere **Arresta debug** dal menu **Debug**.  
  
### <a name="to-examine-the-generated-log-file"></a>Per esaminare il file di log generato  
  
-   Aprire il file TutorialLog.log in Blocco note o in un altro editor di testo.  
  
-   Sebbene la semantica delle informazioni generate per il `PipelineExecutionPlan` e `PipelineExecutionTrees` eventi esulano dall'ambito di questa esercitazione, si può notare che la prima riga sono elencati i campi di informazione specificati nella **dettagli** scheda della finestra il **Configura log SSIS** nella finestra di dialogo. È inoltre possibile verificare che i due eventi selezionati, PipelineExecutionPlan e PipelineExecutionTrees, sono stati inseriti nel log per ogni iterazione del ciclo Foreach.  
  
## <a name="next-lesson"></a>Lezione successiva  
 [Lezione 4: Aggiunta del reindirizzamento del flusso di errore](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md)  
  
  
