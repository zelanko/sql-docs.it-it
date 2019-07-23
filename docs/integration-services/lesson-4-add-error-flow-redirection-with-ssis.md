---
title: 'Lezione 4: Aggiungere il reindirizzamento del flusso errato con SSIS | Microsoft Docs'
ms.custom: ''
ms.date: 01/07/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 0c8dbda2-75e3-4278-9b4e-dcd220c92522
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 3ad643a65eb83b1593b21782ad9784d5062c3899
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68055766"
---
# <a name="lesson-4-add-error-flow-redirection-with-ssis"></a>Lezione 4: Aggiungere il reindirizzamento del flusso degli errori con SSIS

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



Per gestire gli errori che si verificano durante il processo di trasformazione, [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] consente di decidere sulla base dei singoli componenti e delle singole colonne come gestire i dati che [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] non può trasformare. È possibile scegliere di ignorare un errore in alcune colonne, reindirizzare l'intera riga con esito negativo o interrompere l'esecuzione del componente. Per impostazione predefinita, i componenti di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] sono configurati in modo da interrompersi quando si verificano errori. L'arresto di un componente determina l'arresto del pacchetto e l'elaborazione viene quindi interrotta.  
  
Anziché arrestare l'esecuzione del pacchetto a causa degli errori, è possibile configurare e gestire potenziali errori di elaborazione nel momento stesso in cui si verificano. Una possibilità consiste nell'ignorare gli errori completamente in modo che il pacchetto venga sempre eseguito correttamente. È inoltre possibile reindirizzare la riga con esito negativo a un altro percorso di elaborazione, in cui i dati e gli errori possono essere resi persistenti, esaminati o rielaborati.  
  
In questa lezione vengono illustrate le procedure per la creazione di una copia del pacchetto sviluppato nella [Lezione 3: Aggiungere la registrazione con SSIS](../integration-services/lesson-3-add-logging-with-ssis.md). L'utilizzo di questo nuovo pacchetto consente di creare una versione danneggiata di uno dei file di dati di esempio. Durante l'esecuzione del pacchetto il file danneggiato genera un errore di elaborazione.  
  
Per gestire i dati di errore, aggiungere e configurare una destinazione File Flat che scrive le righe con esito negativo in un file di errore. 
  
Prima che [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] scriva i dati di errore nel file, includere un componente script che ottenga le descrizioni degli errori. La trasformazione Lookup Currency Key viene quindi riconfigurata in modo che i dati che non possono essere elaborati vengano reindirizzati alla trasformazione Script.  
  
## <a name="prerequisites"></a>Prerequisites

> [!NOTE]
> Se non è ancora stato fatto, vedere [Lezione 1: Prerequisiti](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites).
 
## <a name="lesson-task"></a>Attività della lezione
In questa lezione sono incluse le attività seguenti:  
  
-   [Passaggio 1: Copiare il pacchetto della lezione 3](../integration-services/lesson-4-1-copying-the-lesson-3-package.md)  
  
-   [Passaggio 2: Creare un file danneggiato](../integration-services/lesson-4-2-creating-a-corrupted-file.md)  
  
-   [Passaggio 3: Aggiungere il reindirizzamento del flusso degli errori](../integration-services/lesson-4-3-adding-error-flow-redirection.md)  
  
-   [Passaggio 4: Aggiungere una destinazione file flat](../integration-services/lesson-4-4-adding-a-flat-file-destination.md)  
  
-   [Passaggio 5: Testare il pacchetto creato nella lezione 4 dell'esercitazione](../integration-services/lesson-4-5-testing-the-lesson-4-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Inizio della lezione  
[Passaggio 1: Copiare il pacchetto della lezione 3](../integration-services/lesson-4-1-copying-the-lesson-3-package.md)  
  
  
  
