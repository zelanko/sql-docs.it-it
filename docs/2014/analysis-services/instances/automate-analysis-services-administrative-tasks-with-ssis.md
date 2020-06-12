---
title: Automatizzare Analysis Services attività amministrative con SSIS | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Execute DDL Task [Analysis Services]
- Analysis Services Processing task
ms.assetid: e960a9a2-80b4-45da-9369-bc560ecdccac
author: minewiskan
ms.author: owend
ms.openlocfilehash: a8b44e09f929ad6a331bb335e801838ed3de64de
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/09/2020
ms.locfileid: "84544113"
---
# <a name="automate-analysis-services-administrative-tasks-with-ssis"></a>Automatizzare le attività amministrative di Analysis Services con SSIS
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] consente di automatizzare l'esecuzione di script DDL, attività di elaborazione di cubi e modelli di data mining e data mining attività di query. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] può essere considerato come una raccolta di attività di flusso di controllo e manutenzione che possono essere collegate per formare processi di elaborazione dati sequenziali e paralleli.  
  
 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è progettato per l'esecuzione di operazioni di pulitura dei dati durante le attività di elaborazione dei dati e per il raggruppamento di dati da diverse origini dei dati. Quando si usano cubi e modelli di data mining, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] consente di trasformare i dati non numerici in dati numerici e di garantire che i valori dei dati rientrino nei limiti previsti, creando pertanto dati puliti con cui popolare dimensioni e tabelle dei fatti.  
  
## <a name="integration-services-tasks"></a>Attività di Integration Services  
 Ogni attività o processo di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è costituito da due elementi principali, ovvero elementi del flusso di controllo ed elementi del flusso di dati. Gli elementi del flusso di controllo definiscono l'ordinamento logico dell'avanzamento del processo tramite l'applicazione di vincoli di precedenza. Gli elementi del flusso di dati riguardano la connettività tra l'output di un componente e l'input del componente seguente, più eventuali trasformazioni dei dati che potrebbero avvenire nei dati intermedi. Per quanto riguarda la decisione relativa alla destinazione dei dati, i vincoli di precedenza contengono la logica che specifica il componente che riceve l'output. Le [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] attività più rilevanti per [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] includere l'attività Esegui DDL, l'attività Elaborazione Analysis Services e l'attività query di data mining. Per ognuna di queste attività, è possibile utilizzare l'attività Invia messaggi per inviare all'amministratore un messaggio di posta elettronica contenente i risultati dell'attività.  
  
## <a name="the-execute-ddl-task"></a>Attività Esegui DDL  
 In [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] l'attività Esegui DDL consente di inviare script DDL direttamente al server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e di eseguirli automaticamente. In questo modo, l'amministratore di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] può eseguire operazioni di backup, ripristino o sincronizzazione da un pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Un pacchetto è costituito dagli elementi del flusso di dati e di controllo descritti in precedenza, che devono essere tutti eseguiti regolarmente ( **run regularly**), come le altre istruzioni DDL che è possibile aggiungere alle attività. Poiché le attività illustrate in questa sezione vengono spesso eseguite di notte, è particolarmente utile disporre di pacchetti che possano essere eseguiti da qualsiasi applicazione di pianificazione. Tramite [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] è possibile pianificare l'esecuzione di un pacchetto a qualsiasi ora. Per altre informazioni sull'implementazione di questa attività, vedere [Attività Elaborazione Analysis Services](../../integration-services/control-flow/analysis-services-execute-ddl-task.md).  
  
## <a name="analysis-services-processing-task"></a>Elaborazione Analysis Services - attività  
 In [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] l'attività Elaborazione Analysis Services consente di popolare automaticamente i cubi con nuove informazioni quando si eseguono aggiornamenti regolari nel database relazionale di origine. Tramite l'attività Elaborazione Analysis Services è possibile eseguire l'elaborazione a livello di dimensione, cubo o partizione. L'elaborazione stessa può essere di tipo `incremental` o `full`, in base alle esigenze del processo. L'elaborazione incrementale consente di aggiungere nuovi dati ed eseguire un numero sufficiente di nuovi calcoli per mantenere la destinazione aggiornata, mentre l'elaborazione completa consente di eliminare i dati esistenti per ricaricarli completamente ed eseguire nuovi calcoli. L'elaborazione completa richiede più tempo, ma è più esaustiva. Per ulteriori informazioni sull'implementazione di questa attività, vedere [Analysis Services Processing Task](../../integration-services/control-flow/analysis-services-processing-task.md).  
  
## <a name="data-mining-query-task"></a>Attività Query di data mining  
 In [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] l'attività Query di data mining consente di estrarre le informazioni dai modelli di data mining e di archiviarle. Spesso le informazioni vengono archiviate in un database relazionale e possono ad esempio essere utilizzate per isolare un elenco di clienti potenziali per una campagna di marketing diretta. Tramite il data mining è possibile identificare il valore di un cliente e la probabilità con cui il cliente risponderà a una strategia di marketing particolare. L'attività Query di data mining può essere utilizzata per estrarre e modificare i dati nel formato desiderato. Per ulteriori informazioni sull'implementazione di questa attività, vedere [Data Mining Query Task](../../integration-services/control-flow/data-mining-query-task.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Destinazione elaborazione partizione](../../integration-services/data-flow/partition-processing-destination.md)   
 [Destinazione elaborazione dimensione](../../integration-services/data-flow/dimension-processing-destination.md)   
 [Trasformazione query di data mining](../../integration-services/data-flow/transformations/data-mining-query-transformation.md)   
 [Elaborazione di oggetti del modello multidimensionale](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Creare script per le attività amministrative in Analysis Services](../script-administrative-tasks-in-analysis-services.md)  
  
  
