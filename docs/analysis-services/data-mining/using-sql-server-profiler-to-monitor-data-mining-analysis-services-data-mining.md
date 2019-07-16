---
title: Usando SQL Server Profiler per il monitoraggio di Data Mining | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4ba9720f87cd41849cc118482ffbf4731049e8c9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "68209555"
---
# <a name="using-sql-server-profiler-to-monitor-data-mining-analysis-services---data-mining"></a>Utilizzo di SQL Server Profiler per il monitoraggio di attività di data mining (Analysis Services - Data mining)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Se si dispone delle autorizzazioni necessarie, è possibile utilizzare SQL Server Profiler per monitorare le attività di data mining emesse come richieste inviate a un'istanza di SQL Server Analysis Services. L'attività di data mining può includere l'elaborazione di modelli o strutture, query di stima o sul contenuto oppure la creazione di nuovi modelli o strutture.  
  
 SQL Server Profiler usa un oggetto **trace** per monitorare le richieste inviate da più client, tra cui [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], SQL Server Management Studio, servizi Web o componenti aggiuntivi Data Mining per Excel, a condizione che per tutte le attività venga usata la stessa istanza di SQL Server Analysis Services. È necessario creare una traccia separata per ciascuna istanza di SQL Server Analysis Services da monitorare. Per informazioni generali sulle tracce e su come usare SQL Server Profiler, vedere [Usare SQL Server Profiler per il monitoraggio di Analysis Services](../../analysis-services/instances/use-sql-server-profiler-to-monitor-analysis-services.md).  
  
 Per informazioni specifiche sui tipi di eventi da acquisire, vedere [Creare tracce del profiler per la riproduzione &#40;Analysis Services&#41;](../../analysis-services/instances/create-profiler-traces-for-replay-analysis-services.md).  
  
## <a name="using-traces-to-monitor-data-mining"></a>Utilizzo di tracce per il monitoraggio di data mining  
 Quando si acquisiscono informazioni contenute in una traccia, è possibile specificare se salvare le informazioni in un file o in una tabella di un'istanza di SQL Server. A prescindere dal metodo di archiviazione dei dati, è possibile utilizzare SQL Server Profiler per visualizzare la traccia e filtrarla in base agli eventi. Nella tabella seguente sono elencati alcuni eventi e sottoclassi contenuti nella traccia [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] predefinita di interesse per il data mining.  
  
|EventClass|EventSubclass|Descrizione|  
|----------------|-------------------|-----------------|  
|**Query Begin**<br /><br /> **Query End**|**0 - MDXQuery**|Contiene il testo di tutte le chiamate a stored procedure [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .|  
|**Query Begin**<br /><br /> **Query End**|**1 - DMXQuery**|Contiene il testo e i risultati di istruzioni DMX (Data Mining Extensions).|  
|**Progress Report Begin**<br /><br /> **Progress Report End**|**34 - DataMiningProgress**|Fornisce informazioni sullo stato di avanzamento dell'algoritmo di data mining: durante la compilazione di un modello di clustering: ad esempio, il messaggio di stato segnala il cluster in corso di compilazione|  
|**Query Begin**<br /><br /> **Query End**|EXECUTESQL|Contiene il testo della query Transact-SQL in esecuzione|  
|**Query Begin**<br /><br /> **Query End**|**2- SQLQuery**|Contiene il testo delle query sui set di righe dello schema nel formato di tabelle del sistema.|  
|**DISCOVER Begin**<br /><br /> **DISCOVER End**|Più di uno|Contiene il testo di chiamate di funzioni DMX o istruzioni DISCOVER, incapsulate in XMLA.|  
|**Errore**|(nessuna)|Contiene il testo degli errori inviati dal server al client.<br /><br /> I messaggi di errore preceduti da **Errore (data mining):** o **Messaggio informativo (data mining):** sono generati in maniera specifica in risposta a richieste DMX. La sola visualizzazione di questi messaggi di errore non è tuttavia sufficiente, perché altri errori, quali quelli generati dal parser, potrebbero essere correlati al data mining senza questi prefissi.|  
  
 La visualizzazione delle istruzioni di comando nel registro di traccia consente di visualizzare anche la sintassi di istruzioni complesse inviate dal client al server [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , comprese chiamate alle stored procedure di sistema. Queste informazioni possono essere utili per il debug oppure è possibile utilizzare le istruzioni valide come modello per la creazione di nuove query o modelli di stima. Per alcuni esempi di chiamate alle stored procedure acquisibili tramite traccia, vedere [Esempi di query sul modello di clustering](../../analysis-services/data-mining/clustering-model-query-examples.md).  
  
## <a name="see-also"></a>Vedere anche  

 [Monitorare Analysis Services con eventi estesi di SQL Server](../../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md)  
  
  
