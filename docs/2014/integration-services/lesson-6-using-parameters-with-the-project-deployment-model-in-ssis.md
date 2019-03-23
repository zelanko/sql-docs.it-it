---
title: 'Lezione 6: Utilizzo di parametri con il modello di distribuzione | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 9216f18c-1762-4f2d-8c22-bd0ab7107555
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d559defe1dd08f26077738cdd0aea219e8f7554b
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58384959"
---
# <a name="lesson-6-using-parameters-with-the-project-deployment-model"></a>Lezione 6: Utilizzo di parametri con il modello di distribuzione del progetto
  In SQL Server 2012 è disponibile un nuovo modello di distribuzione in cui è possibile distribuire i progetti nel server Integration Services. Il server Integration Services consente di gestire ed eseguire pacchetti e di configurare i valori di runtime per i pacchetti.  
  
 In questa lezione si modificherà il pacchetto creato nella [lezione 5: Aggiunta delle configurazioni di pacchetto per il modello di distribuzione pacchetto](lesson-5-add-ssis-package-configurations-for-the-package-deployment-model.md) per utilizzare il modello di distribuzione. Sostituire il valore di configurazione con un parametro per specificare la posizione dei dati di esempio. È inoltre possibile copiare il pacchetto della lezione 5 completato incluso nell'esercitazione.  
  
 Mediante la configurazione guidata progetti di Integration Services convertire il progetto nel modello di distribuzione del progetto e utilizzare un parametro anziché un valore di configurazione per impostare la proprietà Directory. In questa lezione vengono illustrati solo alcuni dei passaggi per convertire i pacchetti esistenti SSIS nel nuovo modello di distribuzione del progetto.  
  
 Quando il pacchetto viene di nuovo eseguito, il servizio Integration Services usa il parametro per popolare il valore della variabile e la variabile a sua volta aggiorna la proprietà Directory. Di conseguenza, tramite il pacchetto viene eseguita un'iterazione della nuova cartella dei dati specificata dal valore del parametro anziché della cartella impostata nel file di configurazione del pacchetto.  
  
> [!IMPORTANT]  
>  Per eseguire questa esercitazione, è necessario il database di esempio **AdventureWorksDW2012** . Per altre informazioni sull'installazione e sulla distribuzione di **AdventureWorksDW2012**, vedere [Considerazioni per l'installazione di esempi e di database di esempio di SQL Server](https://technet.microsoft.com/library/ms161556%28v=sql.105%29).  
  
## <a name="lesson-tasks"></a>Argomenti della lezione  
 In questa lezione sono incluse le attività seguenti:  
  
1.  [Passaggio 1: Copia del pacchetto della lezione 5](lesson-6-1-copying-the-lesson-5-package.md)  
  
2.  [Passaggio 2: Conversione del progetto nel modello di distribuzione progetto](lesson-6-2-converting-the-project-to-the-project-deployment-model.md)  
  
3.  [Passaggio 3: Test del pacchetto della lezione 6](lesson-6-3-testing-the-lesson-6-package.md)  
  
4.  [Passaggio 4: Distribuzione del pacchetto della lezione 6](lesson-6-4-deploying-the-lesson-6-package.md)  
  
## <a name="start-the-lesson"></a>Inizio della lezione  
 [Passaggio 1: Copia del pacchetto della lezione 5](lesson-6-1-copying-the-lesson-5-package.md)  
  
  
