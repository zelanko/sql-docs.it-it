---
title: 'Lezione 3: Aggiungere la registrazione con SSIS | Microsoft Docs'
ms.custom: ''
ms.date: 01/04/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: tutorial
ms.assetid: 64cd24cc-ba8e-4bd7-b10b-6b80d8b04af6
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 6ebbc82f5570fb97d7b1169563bfde7c67f5be0d
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "71296016"
---
# <a name="lesson-3-add-logging-with-ssis"></a>Lezione 3: Aggiungere la registrazione con SSIS

[!INCLUDE[ssis-appliesto](../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]



[!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] include funzionalità di registrazione che consentono di risolvere i problemi e monitorare l'esecuzione dei pacchetti offrendo una traccia degli eventi generati dalle attività e dai contenitori. Le funzionalità di registrazione sono flessibili. È possibile abilitare la registrazione a livello di pacchetto o in singole attività o contenitori all'interno del pacchetto. Selezionare gli eventi da registrare e creare più log per un singolo pacchetto.  
  
I provider di log creano i log. Ogni provider di log è in grado di scrivere le informazioni di registrazione in diversi formati e tipi di destinazione. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] rende disponibili i provider di log seguenti:  
  
-   File di testo  
  
-   [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]  
  
-   Registro eventi di Windows  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   File XML  
  
In questa lezione vengono illustrate le procedure per la creazione di una copia del pacchetto creato nella [Lezione 2: Aggiungere cicli con SSIS](../integration-services/lesson-2-adding-looping-with-ssis.md). Usando questo nuovo pacchetto, vengono aggiunte e configurate funzionalità di registrazione per monitorare eventi specifici durante l'esecuzione del pacchetto. Se non è stata completata una delle lezioni precedenti, è anche possibile copiare il pacchetto della lezione 2 completato incluso nell'esercitazione.  

> [!NOTE]
> Se non è ancora stato fatto, vedere [Lezione 1: Prerequisiti](../integration-services/lesson-1-create-a-project-and-basic-package-with-ssis.md#prerequisites).

## <a name="lesson-tasks"></a>Argomenti della lezione  
In questa lezione sono incluse le attività seguenti:  
  
-   [Passaggio 1: Copiare il pacchetto della lezione 2](../integration-services/lesson-3-1-copying-the-lesson-2-package.md)  
  
-   [Passaggio 2: Aggiungere e configurare le funzionalità di registrazione](../integration-services/lesson-3-2-adding-and-configuring-logging.md)  
  
-   [Passaggio 3: Testare il pacchetto della lezione 3](../integration-services/lesson-3-3-testing-the-lesson-3-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Inizio della lezione  
[Passaggio 1: Copiare il pacchetto della lezione 2](../integration-services/lesson-3-1-copying-the-lesson-2-package.md)  
  
