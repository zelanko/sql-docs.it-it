---
title: Esecuzione di operazioni Batch (XMLA) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6c451d13016915c9218efb2963429f8f5a7709e2
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63261653"
---
# <a name="performing-batch-operations-xmla"></a>Esecuzione di operazioni batch (XMLA)
  È possibile usare la [Batch](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla) comando in XML for Analysis (XMLA) per eseguire più comandi XMLA utilizzando un singolo XMLA [Execute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-methods-execute) (metodo). È possibile eseguire più comandi contenuti nel **Batch** comando come una singola transazione o in transazioni separate per ogni comando, in serie o in parallelo. È inoltre possibile specificare associazioni out-of-line e altre proprietà di **Batch** comando per l'elaborazione di più [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oggetti.  
  
## <a name="running-transactional-and-nontransactional-batch-commands"></a>Esecuzione di comandi Batch transazionali e non transazionali  
 Il **Batch** comando esegue comandi in uno dei due modi:  
  
 **Transazionale**  
 Se il **transazione** attributo del **Batch** command è impostato su true, il **Batch** comandi eseguito tutti i comandi contenuti dal comando il **Batch** comando in una singola transazione-a *transazionale* batch.  
  
 Se un comando non riesce in un batch transazionale, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] rollback di qualsiasi comando nel **Batch** comando eseguito prima del comando che non è riuscita e il **Batch** comando termina immediatamente. Tutti i comandi nel **Batch** non vengono eseguiti i comandi che non hanno ancora eseguito. Dopo il **Batch** comando termina, il **Batch** comando segnala tutti gli errori che si sono verificati per il comando non riuscito.  
  
 **Nontransactional**  
 Se il **transazione** attributo è impostato su false, il **Batch** comando viene eseguito ogni comando contenuto il **Batch** comando in una transazione a  *non transazionale* batch. Se un comando non riesce in un batch non transazionale, il **Batch** comando continua a eseguire i comandi successivi al comando non è riuscita. Dopo il **Batch** comando tenta di eseguire tutti i comandi che la **Batch** comando contiene, il **Batch** comando segnala tutti gli errori che si sono verificati.  
  
 Tutti i risultati restituiti dai comandi contenuti in un **Batch** comando vengono restituiti nello stesso ordine in cui i comandi sono contenuti nel **Batch** comando. I risultati restituiti da una **Batch** comandi variano a seconda se il **Batch** comando è transazionale o non transazionale.  
  
> [!NOTE]  
>  Se un **Batch** comando contiene un comando che non restituisce output, ad esempio le [blocco](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/lock-element-xmla) comando e che comando viene eseguito correttamente, il **Batch** comando restituisce un oggetto vuoto [radice](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/root-element-xmla) elemento all'interno dell'elemento results. Vuoto **radice** elemento garantisce che ogni comando contenuto un **Batch** comando può essere associato a appropriato **radice** (elemento) per i risultati del comando.  
  
### <a name="returning-results-from-transactional-batch-results"></a>Restituzione di risultati di un batch transazionale  
 Risultati di comandi eseguiti all'interno di un batch transazionale non vengono restituiti fino all'intera **Batch** completamento del comando. I risultati non vengono restituiti dopo ogni comando viene eseguito poiché qualsiasi comando che ha esito negativo in un batch transazionale provocherebbe l'intera **Batch** comando e tutti i comandi che lo contiene per eseguire il rollback. Se tutti i comandi avviati ed eseguiti correttamente, il [restituire](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/return-element-xmla) elemento delle [ExecuteResponse](https://docs.microsoft.com/bi-reference/xmla/xml-elements-objects-executeresponse) elemento restituito dal **Execute** metodo per il **Batch**  comando contiene uno [risultati](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/results-element-xmla) elemento, che a sua volta contiene uno **radice** (elemento) per ogni comando eseguito correttamente contenuto nel **Batch** comandi. Se un comando nel **Batch** comando non può essere avviato o non viene completata, il **Execute** metodo restituisce un errore SOAP per il **Batch** comando che contiene l'errore dei comando non riuscito.  
  
### <a name="returning-results-from-nontransactional-batch-results"></a>Restituzione di risultati di un batch non transazionale  
 Risultati di comandi eseguiti all'interno di un batch non transazionale vengono restituiti nell'ordine in cui i comandi sono contenuti all'interno di **Batch** comando e come vengono restituiti da ogni comando. Se nessun comando contenuto nel **Batch** comando può essere avviato correttamente, il **Execute** metodo restituisce un errore SOAP che contiene un errore per il **Batch** comando. Se almeno un comando è stato avviato, il **restituire** elemento delle **ExecuteResponse** elemento restituito dal **Execute** metodo per il **Batch**  comando contiene uno **risultati** elemento, che a sua volta contiene uno **radice** (elemento) per ogni comando contenuto nel **Batch** comando . Se uno o più comandi in un batch non transazionale non può essere avviati o non viene completata, il **radice** (elemento) per tale comando non riuscito contiene un [errore](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/error-element-xmla) elemento che descrive l'errore.  
  
> [!NOTE]  
>  Purché almeno un comando in un batch non transazionale può essere avviato, il batch non transazionale è considerato a hanno eseguito correttamente, anche se ogni comando contenuto nel batch non transazionale restituisce un errore nei risultati del **Batch**  comando.  
  
## <a name="using-serial-and-parallel-execution"></a>Esecuzione in serie e parallela  
 È possibile usare la **Batch** comando da eseguire inclusi i comandi in serie o in parallelo. Quando i comandi vengono eseguiti in serie, il comando successivo incluso nella **Batch** comando non è possibile avviare fino al comando attualmente in esecuzione nel **Batch** completamento del comando. Quando i comandi vengono eseguiti in parallelo, più comandi possono eseguire contemporaneamente la **Batch** comando.  
  
 Per eseguire comandi in parallelo, si aggiungono i comandi da eseguire in parallelo per il [parallele](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/parallel-element-xmla) proprietà delle **Batch** comando. Attualmente [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] eseguibili solo contigui e sequenziali [processo](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla) comandi in parallelo. Qualsiasi altro comando XMLA, ad esempio [Create](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/create-element-xmla) oppure [Alter](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/alter-element-xmla), incluso nel **Parallel** proprietà viene eseguita in serie.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] tenta di eseguire tutti i **processo** comandi inclusi nel **parallele** proprietà in parallelo, ma non può garantire che tutti inclusi **processo** comandi possono essere eseguiti in parallelo. L'istanza analizza ogni **processo** comando e, se l'istanza determina che il comando non può essere eseguito in parallelo, il **processo** comando viene eseguito in serie.  
  
> [!NOTE]  
>  Per eseguire i comandi in parallelo, il **transazione** attributo delle **Batch** comando deve essere impostato su true perché [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] supporta solo una transazione attiva per connessione e non transazionali batch eseguono ogni comando in una transazione separata. Se si include il **parallele** si verifica un errore di proprietà in un batch non transazionale.  
  
### <a name="limiting-parallel-execution"></a>Impostazioni di limiti all'esecuzione parallela  
 Un' [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] istanza tenta di eseguire tante **processo** comandi in parallelo possibili, fino ai limiti del computer in cui viene eseguita l'istanza. È possibile limitare il numero di simultaneamente **processo** comandi impostando il **maxParallel** attributo del **parallele** proprietà su un valore che indica il numero massimo di **processo** comandi che possono essere eseguiti in parallelo.  
  
 Ad esempio, un **parallele** proprietà contiene i comandi seguenti nell'ordine elencato:  
  
1.  **Creare**  
  
2.  **Process**  
  
3.  **Alter**  
  
4.  **Process**  
  
5.  **Process**  
  
6.  **Process**  
  
7.  **Elimina**  
  
8.  **Process**  
  
9. **Process**  
  
 Il **maxParalle**attributo l di questo **parallele** è impostata su 2. Di conseguenza l'istanza esegue gli elenchi precedenti di comandi nel modo descritto nell'elenco seguente:  
  
-   Comando 1 viene eseguito in serie poiché il comando 1 è un **Create** comando e unica **processo** comandi possono essere eseguiti in parallelo.  
  
-   Comando 2 viene eseguito in serie dopo il completamento del comando 1.  
  
-   Comando 3 viene eseguito in serie dopo il completamento del comando 2.  
  
-   Comandi 4 e 5 vengono eseguiti in parallelo dopo il completamento del comando 3. Sebbene comando 6 sia anche un **processo** comando, comando 6 non è possibile eseguire in parallelo con i comandi 4 e 5 poiché la **maxParallel** è impostata su 2.  
  
-   Il comando 6 viene eseguito in serie dopo il completamento dei comandi 4 e 5.  
  
-   Il comando 7 viene eseguito in serie dopo il completamento del comando 6.  
  
-   I comandi 8 e 9 vengono eseguiti in parallelo dopo il completamento del comando 7.  
  
## <a name="using-the-batch-command-to-process-objects"></a>Utilizzo del comando Batch per l'elaborazione di oggetti  
 Il **Batch** comando contiene numerose proprietà facoltative e gli attributi inclusi in modo specifico per supportare l'elaborazione di più [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] progetti:  
  
-   Il **ProcessAffectedObjects** attributo il **Batch** comando indica se l'istanza deve elaborare anche qualsiasi oggetto che richiede la rielaborazione in seguito a un **processo** inclusi nel comando i **Batch** comando elabora un oggetto specificato.  
  
-   Il [associazioni](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/bindings-element-xmla) proprietà contiene una raccolta di associazioni out-of-line utilizzate da tutti i **processo** comandi nel **Batch** comando.  
  
-   Il [DataSource](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasource-element-xmla) proprietà contiene un'associazione out-of-line per un'origine dati utilizzata da tutti i **processo** comandi nel **Batch** comando.  
  
-   Il [DataSourceView](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/datasourceview-element-xmla) proprietà contiene un'associazione out-of-line per una vista origine dati utilizzata da tutti i **processo** comandi nel **Batch** comando.  
  
-   Il [ErrorConfiguration](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/errorconfiguration-element-xmla) proprietà specifica il modo in cui le **Batch** comando gestisce gli errori rilevati da tutti **processo** comandi contenuti nel **Batch** comando.  
  
    > [!IMPORTANT]  
    >  Oggetto **processo** comando non è possibile includere le **associazioni**, **DataSource**, **DataSourceView**, o **ErrorConfiguration**  proprietà, se il **processo** comando è contenuto in un **Batch** comando. Se è necessario specificare queste proprietà per un **processo** comando, specificare le informazioni necessarie nelle proprietà corrispondenti delle **Batch** comando che contiene il **processo** comandi.  
  
## <a name="see-also"></a>Vedere anche  
 [Elemento batch &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/batch-element-xmla)   
 [Elaborare l'elemento &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/process-element-xmla)   
 [Elaborazione di un modello multidimensionale &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)   
 [Sviluppo con XMLA in Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
