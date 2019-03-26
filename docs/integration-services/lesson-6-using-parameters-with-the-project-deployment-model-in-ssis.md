---
title: 'Lezione 6: Usare parametri con il modello di distribuzione del progetto in SSIS | Microsoft Docs'
ms.custom: ''
ms.date: 01/11/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 9216f18c-1762-4f2d-8c22-bd0ab7107555
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b9ebfb17a69abbaf8482999d3435bbdea11e0822
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/20/2019
ms.locfileid: "58289897"
---
# <a name="lesson-6-use-parameters-with-the-project-deployment-model-in-ssis"></a>Lezione 6: Usare parametri con il modello di distribuzione del progetto in SSIS

SQL Server 2012 ha introdotto un nuovo modello di distribuzione in cui è possibile distribuire i progetti nel server Integration Services. Il server Integration Services consente di gestire ed eseguire pacchetti e di configurare i valori di runtime per i pacchetti.  
  
In questa lezione si modifica il pacchetto creato nella [Lezione 5: Aggiungere configurazioni del pacchetto SSIS per il modello di distribuzione del pacchetto](../integration-services/lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md) per usare il modello di distribuzione del progetto. Sostituire il valore di configurazione con un parametro per specificare la posizione dei dati di esempio. È inoltre possibile copiare il pacchetto della lezione 5 completato incluso nell'esercitazione.  
  
La Conversione guidata progetto di Integration Services consente di convertire il progetto nel modello di distribuzione del progetto. Questo modello usa un parametro anziché un valore di configurazione per impostare la proprietà Directory. In questa lezione vengono illustrati solo alcuni dei passaggi per convertire i pacchetti esistenti SSIS nel nuovo modello di distribuzione del progetto.  
  
Quando si esegue di nuovo il pacchetto, il server [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] usa il parametro per popolare il valore della variabile. La variabile a sua volta aggiorna la proprietà Directory. Il pacchetto esegue l'iterazione nei file della cartella di dati specificata dal nuovo parametro.  
  
> [!NOTE]
> Se non è ancora stato fatto, vedere [Lezione 1: Prerequisiti](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites).
    
## <a name="lesson-tasks"></a>Argomenti della lezione  
In questa lezione sono incluse le attività seguenti:  
  
1.  [Passaggio 1: Copiare il pacchetto della lezione 5](../integration-services/lesson-6-1-copying-the-lesson-5-package.md)  
  
2.  [Passaggio 2: Convertire il progetto nel modello di distribuzione del progetto](../integration-services/lesson-6-2-converting-the-project-to-the-project-deployment-model.md)  
  
3.  [Passaggio 3: Testare il pacchetto della lezione 6](../integration-services/lesson-6-3-testing-the-lesson-6-package.md)  
  
4.  [Passaggio 4: Distribuire il pacchetto della lezione 6](../integration-services/lesson-6-4-deploying-the-lesson-6-package.md)  
  
## <a name="start-the-lesson"></a>Inizio della lezione  
[Passaggio 1: Copiare il pacchetto della lezione 5](../integration-services/lesson-6-1-copying-the-lesson-5-package.md)  
  
