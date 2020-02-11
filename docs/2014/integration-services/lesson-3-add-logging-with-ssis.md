---
title: 'Lezione 3: aggiunta della registrazione | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 64cd24cc-ba8e-4bd7-b10b-6b80d8b04af6
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e716b808d5d9ada8aeaf50d92006cc6453c6e47d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67046759"
---
# <a name="lesson-3-adding-logging"></a>Lezione 3: Aggiunta delle funzionalità di registrazione
  [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] include funzionalità di registrazione che consentono di risolvere i problemi e monitorare l'esecuzione dei pacchetti fornendo una traccia degli eventi di attività e contenitori. Le caratteristiche di registrazione sono flessibili ed è possibile attivarle a livello di pacchetto o a livello di singole attività o contenitori del pacchetto. È possibile selezionare gli eventi che si desidera registrare e creare più log per un singolo pacchetto.  
  
 La registrazione è garantita da un provider di log. Ogni provider di log è in grado di scrivere le informazioni di registrazione in diversi formati e tipi di destinazione. 
  [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] rende disponibili i provider di log seguenti:  
  
-   File di testo  
  
-   [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)]  
  
-   Registro eventi di Windows  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]  
  
-   File XML  
  
 In questa lezione verrà creata una copia del pacchetto creato nella [lezione 2: aggiunta del ciclo](lesson-2-adding-looping-with-ssis.md). Usando questo nuovo pacchetto, verranno aggiunte e configurate funzionalità di registrazione per monitorare eventi specifici durante l'esecuzione del pacchetto. Se non è stata completata nessuna delle lezioni precedenti, è possibile copiare il pacchetto della lezione 2 completato incluso nell'esercitazione.  
  
> [!IMPORTANT]  
>  Per eseguire questa esercitazione, è necessario il database di esempio **AdventureWorksDW2012** . Per altre informazioni su come installare e distribuire **AdventureWorksDW2012**, [Reporting Services esempi di prodotto su GitHub](https://github.com/Microsoft/sql-server-samples/releases/tag/adventureworks).  
  
## <a name="lesson-tasks"></a>Argomenti della lezione  
 In questa lezione sono incluse le attività seguenti:  
  
-   [Passaggio 1: Copia del pacchetto della lezione 2](lesson-3-1-copying-the-lesson-2-package.md)  
  
-   [Passaggio 2: Aggiunta e configurazione di funzionalità di registrazione](lesson-3-2-adding-and-configuring-logging.md)  
  
-   [Passaggio 3: Test del pacchetto creato nella lezione 3 dell'esercitazione](../integration-services/lesson-3-3-testing-the-lesson-3-tutorial-package.md)  
  
## <a name="start-the-lesson"></a>Inizio della lezione  
 [Passaggio 1: Copia del pacchetto della lezione 2](lesson-3-1-copying-the-lesson-2-package.md)  
  
  
