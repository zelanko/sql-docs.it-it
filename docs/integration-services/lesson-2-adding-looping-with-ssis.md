---
title: 'Lezione 2: Aggiungere cicli con SSIS | Microsoft Docs'
ms.custom: ''
ms.date: 01/03/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 01f2ed61-1e5a-4ec6-b6a6-2bd070c64077
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ccd3be3203aae382cda239ed6d7bdc2fa224923b
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "71296058"
---
# <a name="lesson-2-add-looping-with-ssis"></a>Lezione 2: Aggiungere cicli con SSIS

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Nella [Lezione 1: Creare un progetto e un pacchetto di base con SSIS](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md) è stato creato un pacchetto che estrae dati da un'unica origine file flat. I dati vengono quindi trasformati usando le trasformazioni Ricerca. Il pacchetto carica infine i dati in una copia della tabella dei fatti **FactCurrencyRate** nel database di esempio **AdventureWorksDW2012**.  
  
Un processo di estrazione, trasformazione e caricamento (ETL) in genere estrae i dati da più origini file flat. L'estrazione dei dati da più origini richiede un flusso di controllo iterativo. [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] può aggiungere facilmente iterazioni o cicli ai pacchetti.  
  
[!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] offre due tipi di contenitori per eseguire i cicli di pacchetti: il contenitore Ciclo Foreach e il contenitore Ciclo For. Nel contenitore Ciclo Foreach viene usato un enumeratore per il ciclo mentre nel contenitore Ciclo For viene usata in genere un'espressione di variabili. Questa lezione prevede l'uso del contenitore Ciclo Foreach.  
  
Il contenitore Ciclo Foreach consente a un pacchetto di ripetere il flusso di controllo per ogni membro di un enumeratore specificato. Il contenitore Ciclo Foreach consente di enumerare:  
  
-   Righe di un recordset ADO  
  
-   Informazioni sullo schema ADO .NET  
  
-   Strutture di file e directory  
  
-   Variabili utente, di sistema e del pacchetto  
  
-   Oggetti enumerabili in una variabile  
  
-   Elementi di una raccolta  
  
-   Nodi in un'espressione XPATH  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Oggetti SMO (Management Objects)  
  
In questa lezione viene modificato il pacchetto ETL di esempio della lezione 1 per usare un contenitore ciclo Foreach e impostare una variabile di pacchetto definita dall'utente per il pacchetto. Tale variabile viene quindi usata per eseguire l'iterazione dei file corrispondenti nella cartella di esempio.   
  
In questa lezione verrà modificato solo il flusso di controllo, non il flusso di dati.  
  
> [!NOTE]  
> Se non è ancora stato fatto, vedere [Lezione 1: Prerequisiti](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites).

## <a name="lesson-tasks"></a>Argomenti della lezione  
In questa lezione sono incluse le attività seguenti:  
  
-   [Passaggio 1: Copiare il pacchetto della lezione 1](../integration-services/lesson-2-1-copying-the-lesson-1-package.md)  
  
-   [Passaggio 2: Aggiungere e configurare il contenitore Ciclo Foreach](../integration-services/lesson-2-2-adding-and-configuring-the-foreach-loop-container.md)  
  
-   [Passaggio 3: Modificare la gestione connessione file flat](../integration-services/lesson-2-3-modifying-the-flat-file-connection-manager.md)  
  
-   [Passaggio 4: Testare il pacchetto creato nella lezione 2 dell'esercitazione](../integration-services/lesson-2-4-testing-the-lesson-2-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Inizio della lezione  
[Passaggio 1: Copiare il pacchetto della lezione 1](../integration-services/lesson-2-1-copying-the-lesson-1-package.md)  
  
## <a name="see-also"></a>Vedere anche  
[Contenitore Ciclo For](../integration-services/control-flow/for-loop-container.md)  
  
  
  
