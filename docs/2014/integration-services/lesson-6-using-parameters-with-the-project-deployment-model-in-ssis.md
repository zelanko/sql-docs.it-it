---
title: 'Lezione 6: utilizzo di parametri con il modello di distribuzione del progetto | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9216f18c-1762-4f2d-8c22-bd0ab7107555
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 71f86fdc1169a3c9a60d18d832bc90476f193baf
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84951311"
---
# <a name="lesson-6-using-parameters-with-the-project-deployment-model"></a>Lezione 6: Uso di parametri con il modello di distribuzione del progetto
  In SQL Server 2012 è disponibile un nuovo modello di distribuzione in cui è possibile distribuire i progetti nel server Integration Services. Il server Integration Services consente di gestire ed eseguire pacchetti e di configurare i valori di runtime per i pacchetti.  
  
 In questa lezione verrà modificato il pacchetto creato nella [lezione 5: aggiunta di configurazioni del pacchetto per il modello di distribuzione del pacchetto per l'](lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md) utilizzo del modello di distribuzione del progetto. Sostituire il valore di configurazione con un parametro per specificare la posizione dei dati di esempio. È inoltre possibile copiare il pacchetto della lezione 5 completato incluso nell'esercitazione.  
  
 Mediante la configurazione guidata progetti di Integration Services convertire il progetto nel modello di distribuzione del progetto e utilizzare un parametro anziché un valore di configurazione per impostare la proprietà Directory. In questa lezione vengono illustrati solo alcuni dei passaggi per convertire i pacchetti esistenti SSIS nel nuovo modello di distribuzione del progetto.  
  
 Quando il pacchetto viene di nuovo eseguito, il servizio Integration Services usa il parametro per popolare il valore della variabile e la variabile a sua volta aggiorna la proprietà Directory. Di conseguenza, tramite il pacchetto viene eseguita un'iterazione della nuova cartella dei dati specificata dal valore del parametro anziché della cartella impostata nel file di configurazione del pacchetto.  
  
> [!IMPORTANT]  
>  Per eseguire questa esercitazione, è necessario il database di esempio **AdventureWorksDW2012** . Per altre informazioni sull'installazione e sulla distribuzione di **AdventureWorksDW2012**, vedere [Considerazioni per l'installazione di esempi e di database di esempio di SQL Server](https://technet.microsoft.com/library/ms161556%28v=sql.105%29).  
  
## <a name="lesson-tasks"></a>Argomenti della lezione  
 In questa lezione sono incluse le attività seguenti:  
  
1.  [Passaggio 1: Copia del pacchetto della lezione 5](lesson-6-1-copying-the-lesson-5-package.md)  
  
2.  [Passaggio 2: Conversione del progetto nel modello di distribuzione del progetto](lesson-6-2-converting-the-project-to-the-project-deployment-model.md)  
  
3.  [Passaggio 3: Test del pacchetto della lezione 6](lesson-6-3-testing-the-lesson-6-package.md)  
  
4.  [Passaggio 4: Distribuzione del pacchetto della lezione 6](lesson-6-4-deploying-the-lesson-6-package.md)  
  
## <a name="start-the-lesson"></a>Inizio della lezione  
 [Passaggio 1: Copia del pacchetto della lezione 5](lesson-6-1-copying-the-lesson-5-package.md)  
  
  
