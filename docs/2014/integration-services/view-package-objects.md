---
title: Visualizzare oggetti di pacchetto | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, properties
- properties [Integration Services]
- Package Explorer window [Integration Services]
- packages [Integration Services], properties
- explorer view [Integration Services]
- SSIS packages, properties
- viewing package objects
- SQL Server Integration Services packages, properties
ms.assetid: a85c0245-0a68-4eb0-83b1-9b11df80bd10
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ec6d819d48ba5307e4c5c9e61ef8f7c375d6d96c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "78176090"
---
# <a name="view-package-objects"></a>Visualizzazione di oggetti di pacchetto
  In Progettazione [!INCLUDE[ssIS](../includes/ssis-md.md)] è disponibile la scheda **Esplora pacchetti** , che consente di visualizzare i pacchetti in una modalità simile a quella di Esplora risorse. La visualizzazione riflette la gerarchia dei contenitori dell'architettura di [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Il contenitore del pacchetto si trova al livello principale della gerarchia. Espandendo il pacchetto è possibile visualizzare le connessioni, gli eseguibili, i gestori di eventi, i provider di log, i vincoli di precedenza e le variabili del pacchetto.

 Gli eseguibili, ovvero i contenitori e le attività nel pacchetto, possono includere gestori di eventi, vincoli di precedenza e variabili. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] supporta una gerarchia nidificata di contenitori. A loro volta, i contenitori Ciclo For, Ciclo Foreach e Sequenza possono includere altri eseguibili.

 Se un pacchetto include un flusso di dati, in **Esplora pacchetti** verranno visualizzate l'attività Flusso di dati e una cartella **Componenti** contenente l'elenco dei componenti del flusso di dati.

 Dalla scheda **Esplora pacchetti** è possibile eliminare oggetti da un pacchetto e accedere alla finestra **Proprietà** per visualizzare le proprietà degli oggetti.

 Nella figura seguente viene illustrata l'albero di un semplice pacchetto.

 ![Screenshot della scheda Esplora pacchetti](media/packageexplorer.gif "Screenshot della scheda Esplora pacchetti")

### <a name="to-view-package-content"></a>Per visualizzare il contenuto di un pacchetto

-   [Visualizzazione degli oggetti dei pacchetti in Esplora pacchetti](../../2014/integration-services/view-package-objects-in-package-explorer.md)

## <a name="see-also"></a>Vedere anche
 [Integration Services attività](control-flow/integration-services-tasks.md) [Integration Services](control-flow/integration-services-containers.md) [vincoli di precedenza](control-flow/precedence-constraints.md) [Integration Services &#40;variabili SSIS](integration-services-ssis-variables.md)&#41; Integration Services i [gestori eventi &#40;SSIS](integration-services-ssis-event-handlers.md)&#41; [Integration Services la registrazione SSIS](performance/integration-services-ssis-logging.md) &#40;


