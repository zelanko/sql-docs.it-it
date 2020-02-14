---
title: "Passaggio 3: Testare il pacchetto creato nella lezione 3 dell'esercitazione | Microsoft Docs"
ms.custom: ''
ms.date: 01/04/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 1096a476-93cf-4474-86f5-27d6357eb380
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9cdb19c6df46e3c24625bfb740c82771f0adcc1d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "71283173"
---
# <a name="lesson-3-3-test-the-lesson-3-tutorial-package"></a>Lezione 3-3: Testare il pacchetto creato nella lezione 3 dell'esercitazione

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



In questa attività viene eseguito il pacchetto **Lesson 3.dtsx**. Mentre il pacchetto viene eseguito, nella finestra **Eventi del log** sono elencate le voci di log che SSIS scrive nel file di log del provider di log. Al termine dell'esecuzione del pacchetto è possibile visualizzare il contenuto del file di log.  
  
## <a name="check-the-package-layout"></a>Verificare il layout del pacchetto  
Prima di testare il pacchetto, verificare che il flusso di controllo e il flusso di dati nel pacchetto della lezione 3 contengano gli oggetti visualizzati nelle figure seguenti. Il flusso di controllo deve essere identico alla lezione 2 e il flusso di dati deve essere identico alle lezioni 1 e 2.  
  
**Flusso di controllo**  
  
![Flusso di controllo nel pacchetto](../integration-services/media/task4lesson2control.gif "Flusso di controllo nel pacchetto")  
  
**Flusso di dati**  
  
![Flusso di dati nel pacchetto](../integration-services/media/task9lesson1data.gif "Flusso di dati nel pacchetto")  
  
## <a name="run-the-lesson-3-tutorial-package"></a>Eseguire il pacchetto creato nella lezione 3 dell'esercitazione  
  
1.  Selezionare **Eventi del log** dal menu SSIS.  
  
2.  Selezionare **Avvia debug** dal menu **Debug**.  
  
3.  Al termine dell'esecuzione del pacchetto, selezionare **Arresta debug** dal menu **Debug**.  
  
## <a name="examine-the-generated-log-file"></a>Esaminare il file di log generato  
  
-   Aprire il file TutorialLog.log in Blocco note o in un altro editor di testo.  
  
-   Una descrizione completa delle informazioni generate per gli eventi **PipelineExecutionPlan** e **PipelineExecutionTrees** esula dall'ambito di questa esercitazione.  Nel file di log si può osservare che nella prima riga sono elencati i campi di informazione specificati nella scheda **Dettagli** della finestra di dialogo **Configura log SSIS**. È anche possibile verificare che [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] ha inserito nel log i due eventi selezionati, **PipelineExecutionPlan** e **PipelineExecutionTrees**, per ogni iterazione del ciclo Foreach.  
  
## <a name="next-lesson"></a>Lezione successiva  
[Lezione 4: Aggiungere il reindirizzamento del flusso degli errori con SSIS](../integration-services/lesson-4-add-error-flow-redirection-with-ssis.md)  
  
  
  
