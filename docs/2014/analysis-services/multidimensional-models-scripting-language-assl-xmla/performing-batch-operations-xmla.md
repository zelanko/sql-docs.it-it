---
title: Esecuzione di operazioni Batch (XMLA) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- multiple projects
- XML for Analysis, batches
- parallel batch execution [XMLA]
- transactional batches
- serial batch execution [XMLA]
- XMLA, batches
- batches [XML for Analysis]
- nontransactional batches
ms.assetid: 731c70e5-ed51-46de-bb69-cbf5aea18dda
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 2bd661506dbb792eb55194c61d7284d619e63a5f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62702066"
---
# <a name="performing-batch-operations-xmla"></a>Esecuzione di operazioni batch (XMLA)
  È possibile usare la [Batch](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla) comando in XML for Analysis (XMLA) per eseguire più comandi XMLA utilizzando un singolo XMLA [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) (metodo). È possibile eseguire più comandi contenuti nel comando `Batch` come una transazione singola o in transazioni separate per ogni comando, in serie o in parallelo. È inoltre possibile specificare associazioni out-of-line e altre proprietà di `Batch` comando per l'elaborazione di più [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oggetti.  
  
## <a name="running-transactional-and-nontransactional-batch-commands"></a>Esecuzione di comandi Batch transazionali e non transazionali  
 Il comando `Batch` consente di eseguire comandi in una delle due modalità riportate di seguito:  
  
 **Transazionale**  
 Se il `Transaction` attributo del `Batch` comando è impostato su true, il `Batch` comandi eseguito tutti i comandi contenuti dal comando il `Batch` comando in una singola transazione-a *transazionale* batch.  
  
 Se un comando non riesce in un batch transazionale, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] rollback di qualsiasi comando nel `Batch` comando eseguito prima del comando che non è riuscita e `Batch` comando termina immediatamente. Viene inoltre sospesa l'esecuzione di tutti i comandi nel comando `Batch` non ancora eseguiti. Dopo il `Batch` comando termina, il `Batch` comando segnala tutti gli errori che si sono verificati per il comando non riuscito.  
  
 **Nontransactional**  
 Se il `Transaction` attributo è impostato su false, il `Batch` comando viene eseguito ogni comando contenuto il `Batch` comando in una transazione a un *non transazionale* batch. Se in un batch non transazionale un comando non riesce, il comando `Batch` continua a eseguire i comandi successivi al comando non riuscito. Dopo il `Batch` tentato di eseguire tutti i comandi che il `Batch` comando contiene, il `Batch` comando segnala tutti gli errori che si sono verificati.  
  
 Tutti i risultati relativi ai comandi contenuti in un comando `Batch` vengono restituiti nello stesso ordine in cui i comandi sono contenuti nel comando `Batch` stesso. I risultati restituiti da un comando `Batch` possono variare a seconda che il comando `Batch` sia transazionale o non transazionale.  
  
> [!NOTE]  
>  Se un `Batch` comando contiene un comando che non restituisce output, ad esempio il [Lock](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla) comando e che comando viene eseguito correttamente, il `Batch` comando restituisce un oggetto vuoto [radice](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/root-element-xmla) elemento all'interno dell'elemento di risultati. Se l'elemento `root` è vuoto, ogni comando contenuto in un comando `Batch` può essere messo in corrispondenza con l'elemento `root` appropriato per i risultati del comando specifico.  
  
### <a name="returning-results-from-transactional-batch-results"></a>Restituzione di risultati di un batch transazionale  
 I risultati di comandi eseguiti all'interno di un batch transazionale non vengono restituiti fino a quando l'intero comando `Batch` non è stato completato. I risultati non vengono restituiti dopo ciascuna esecuzione di un comando poiché qualsiasi comando che non riesce in un batch transazionale provocherebbe l'esecuzione del rollback dell'intero comando `Batch` e di tutti i comandi che contiene. Se tutti i comandi avviati ed eseguiti correttamente, il [restituire](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/return-element-xmla) elemento delle [ExecuteResponse](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects-executeresponse) elemento restituito dal `Execute` metodo per il `Batch` comando contiene uno [risultati](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/results-element-xmla) elemento, che a sua volta contiene uno `root` (elemento) per ogni comando eseguito correttamente contenuto nel `Batch` comando. Se non è possibile avviare o completare un comando contenuto nel comando `Batch`, il metodo `Execute` restituisce un errore SOAP per il comando `Batch` che contiene l'errore relativo al comando non riuscito.  
  
### <a name="returning-results-from-nontransactional-batch-results"></a>Restituzione di risultati di un batch non transazionale  
 I risultati di comandi eseguiti in un batch non transazionale vengono restituiti nell'ordine in cui tali comandi sono contenuti nel comando `Batch` e nel modo in cui vengono restituiti da ogni comando. Se non è possibile avviare alcun comando contenuto nel comando `Batch`, il metodo `Execute` restituisce un errore SOAP relativo al comando `Batch`. Se almeno un comando viene avviato in modo corretto, l'elemento `return` dell'elemento `ExecuteResponse` restituito dal metodo `Execute` per il comando `Batch` contiene un elemento `results`, che a sua volta contiene un elemento `root` per ogni comando contenuto nel comando `Batch`. Se uno o più comandi in un batch non transazionale non può essere avviati o non viene completata, il `root` (elemento) per tale comando non riuscito contiene un [errore](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/error-element-xmla) elemento che descrive l'errore.  
  
> [!NOTE]  
>  L'esecuzione di un batch non transazionale viene considerata corretta purché sia possibile avviare almeno un comando contenuto nel batch, anche se ogni comando presente nel batch non transazionale restituisce un errore nei risultati del comando `Batch`.  
  
## <a name="using-serial-and-parallel-execution"></a>Esecuzione in serie e parallela  
 Il comando `Batch` consente di eseguire i comandi inclusi serie o in parallelo. Quando i comandi vengono eseguiti in serie, il comando successivo incluso nel comando `Batch` non può essere avviato fino a quando il comando attualmente in esecuzione nel comando `Batch` non è completato. Quando i comandi vengono eseguiti in parallelo, il comando `Batch` può eseguire contemporaneamente più comandi.  
  
 Per eseguire comandi in parallelo, si aggiungono i comandi da eseguire in parallelo per il [parallele](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/parallel-element-xmla) proprietà del `Batch` comando. Attualmente [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] eseguibili solo contigui e sequenziali [processo](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla) comandi in parallelo. Qualsiasi altro comando XMLA, ad esempio [Create](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla) oppure [Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla), incluso nel `Parallel` proprietà viene eseguita in serie.  
  
 In [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] viene effettuato un tentativo di eseguire tutti i comandi `Process` inclusi nella proprietà `Parallel` in parallelo, ma non è possibile garantire che questa operazione sia possibile per tutti i comandi `Process` inclusi. L'istanza analizza ogni comando `Process`. Un comando `Process` viene eseguito in serie se l'istanza determina che non può essere eseguito in parallelo.  
  
> [!NOTE]  
>  Per eseguire comandi in parallelo, l'attributo `Transaction` del comando `Batch` deve essere impostato su true poiché in [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] è supportata solo una transazione attiva per connessione e i batch non transazionali eseguono ogni comando in una transazione separata. Se in un batch non transazionale viene inclusa la proprietà `Parallel`, si verifica un errore.  
  
### <a name="limiting-parallel-execution"></a>Impostazioni di limiti all'esecuzione parallela  
 Un'istanza di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tenta di eseguire in parallelo il maggior numero di comandi `Process` possibile, fino ai limiti specifici del computer in cui è eseguita l'istanza. Per limitare il numero di comandi `Process` eseguiti simultaneamente, è possibile impostare l'attributo `maxParallel` della proprietà `Parallel` su un valore che indica il numero massimo di comandi `Process` che possono essere eseguiti in parallelo.  
  
 Una proprietà `Parallel`, ad esempio, contiene i comandi seguenti nella sequenza elencata:  
  
1.  `Create`  
  
2.  `Process`  
  
3.  `Alter`  
  
4.  `Process`  
  
5.  `Process`  
  
6.  `Process`  
  
7.  `Delete`  
  
8.  `Process`  
  
9. `Process`  
  
 L'attributo `maxParalle`l di tale proprietà `Parallel` è impostato su 2. Di conseguenza l'istanza esegue gli elenchi precedenti di comandi nel modo descritto nell'elenco seguente:  
  
-   Il comando 1 viene eseguito in serie poiché è un comando `Create` e solo i comandi `Process` possono essere eseguiti in parallelo.  
  
-   Comando 2 viene eseguito in serie dopo il completamento del comando 1.  
  
-   Comando 3 viene eseguito in serie dopo il completamento del comando 2.  
  
-   Comandi 4 e 5 vengono eseguiti in parallelo dopo il completamento del comando 3. Sebbene il comando 6 sia anche un comando `Process`, non può essere eseguito in parallelo con i comandi 4 e 5 poiché la proprietà `maxParallel` è impostata su 2.  
  
-   Il comando 6 viene eseguito in serie dopo il completamento dei comandi 4 e 5.  
  
-   Il comando 7 viene eseguito in serie dopo il completamento del comando 6.  
  
-   I comandi 8 e 9 vengono eseguiti in parallelo dopo il completamento del comando 7.  
  
## <a name="using-the-batch-command-to-process-objects"></a>Utilizzo del comando Batch per l'elaborazione di oggetti  
 Il comando `Batch` contiene numerosi attributi e proprietà facoltativi specifici per supportare l'elaborazione di più progetti di [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], come indicato di seguito.  
  
-   L'attributo `ProcessAffectedObjects` del comando `Batch` indica se l'istanza deve elaborare anche qualsiasi oggetto per cui è necessario rieseguire l'elaborazione a seguito del risultato di un comando `Process` incluso in un comando `Batch` che elabora un oggetto specificato.  
  
-   Il [associazioni](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/bindings-element-xmla) proprietà contiene una raccolta di associazioni out-of-line utilizzate da tutti i `Process` comandi nel `Batch` comando.  
  
-   Il [DataSource](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/source-element-xmla) proprietà contiene un'associazione out-of-line per un'origine dati utilizzata da tutti i `Process` comandi nel `Batch` comando.  
  
-   Il [DataSourceView](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasourceview-element-xmla) proprietà contiene un'associazione out-of-line per una vista origine dati utilizzata da tutti i `Process` comandi nel `Batch` comando.  
  
-   Il [ErrorConfiguration](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/errorconfiguration-element-xmla) proprietà specifica il modo in cui le `Batch` comando gestisce gli errori rilevati da tutti `Process` comandi contenuti nel `Batch` comando.  
  
    > [!IMPORTANT]  
    >  Un comando `Process` non può includere la proprietà `Bindings`, `DataSource`, `DataSourceView` o `ErrorConfiguration` se il comando `Process` è contenuto in un comando `Batch`. Se è necessario specificare queste proprietà per un comando `Process`, fornire le informazioni necessarie nelle proprietà corrispondenti del comando `Batch` che contiene il comando `Process`.  
  
## <a name="see-also"></a>Vedere anche  
 [Elemento batch &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla)   
 [Elaborare l'elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla)   
 [Elaborazione degli oggetti modello multidimensionale](../multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Sviluppo con XMLA in Analysis Services](developing-with-xmla-in-analysis-services.md)  
  
  
