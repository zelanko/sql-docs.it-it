---
title: Attività XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.xmltask.f1
helpviewer_keywords:
- XML [Integration Services]
- XML task [Integration Services]
ms.assetid: 9f761846-390e-46d5-9db7-858943d40849
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e89f4835b95b1fe497df32ad9f773be84ccb161b
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/19/2019
ms.locfileid: "75232732"
---
# <a name="xml-task"></a>Attività XML
  L'attività XML consente di eseguire operazioni su dati in formato XML. Tramite questa attività un pacchetto può recuperare documenti XML, applicare operazioni ai documenti utilizzando fogli di stile XSLT (Extensible Stylesheet Language Transformation) ed espressioni XPath, unire più documenti oppure convalidare, confrontare e salvare i documenti aggiornati in file e variabili.  
  
 Questa attività consente ai pacchetti di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] di modificare dinamicamente documenti XML in fase di esecuzione. È possibile utilizzare l'attività XML per gli scopi seguenti:  
  
-   Riformattare un documento XML. L'attività può ad esempio accedere a un report che risiede in un file XML e applicare dinamicamente un foglio di stile XSLT per personalizzare la presentazione del documento.  
  
-   Selezionare sezioni di un documento XML. L'attività può ad esempio accedere a un report che risiede in un file XML e applicare dinamicamente un'espressione XPath per selezionare una sezione del documento. L'operazione può inoltre ottenere ed elaborare valori nel documento.  
  
-   Unire più documenti da numerose origini. L'attività può ad esempio scaricare report da più origini e unirli dinamicamente in un documento XML riepilogativo.  
  
-   Convalidare un documento XML e, facoltativamente, ottenere un output dettagliato degli errori. Per ulteriori informazioni, vedere [Validate XML with the XML Task](xml-task.md).  
  
 È possibile includere dati XML in un flusso di dati utilizzando un'origine XML per estrarre valori da un documento XML. Per altre informazioni, vedere [Origine XML](../data-flow/xml-source.md).  
  
## <a name="xml-operations"></a>Operazioni XML  
 La prima azione eseguita dall'attività XML consiste nel recupero di un documento XML specifico. Tale azione è incorporata nell'attività XML e viene eseguita automaticamente. Il documento XML recuperato viene utilizzato come origine dei dati per l'operazione eseguita dall'attività XML.  
  
 Le operazioni XML Diff, Merge e Patch richiedono due operandi. Il primo operando specifica il documento XML di origine. Il secondo specifica un documento XML il cui contenuto dipende dai requisiti dell'operazione. L'operazione Diff, ad esempio, confronta due documenti. Il secondo operando specifica pertanto un altro documento XML simile, con cui confrontare il documento XML di origine.  
  
 L'attività XML può utilizzare una variabile o una gestione connessione file come origine oppure includere i dati XML in una proprietà dell'attività.  
  
 Se l'origine è una variabile, la variabile specificata conterrà il percorso del documento XML.  
  
 Se l'origine è una gestione connessione file, le informazioni sull'origine verranno fornite dalla gestione connessione file specificata, configurata separatamente, a cui viene fatto riferimento dall'attività XML. La stringa di connessione della gestione connessione file specifica il percorso del file XML. Per ulteriori informazioni, vedere [gestione connessione file](../connection-manager/file-connection-manager.md).  
  
 L'attività XML può essere configurata in modo da salvare il risultato dell'operazione in una variabile o in un file. Se il risultato viene salvato in un file, l'attività XML utilizzerà una gestione connessione file per accedervi. Anche i risultati del Diffgram generato dall'operazione Diff possono essere salvati in file e variabili.  
  
## <a name="predefined-xml-operations"></a>Operazioni XML predefinite  
 L'attività XML include un set predefinito di operazioni applicabili ai documenti XML, descritte nella tabella seguente.  
  
|Operazione|Description|  
|---------------|-----------------|  
|Diff|Consente di confrontare due documenti XML. Utilizzando il documento XML di origine come documento di base, l'operazione Diff esegue un confronto con un secondo documento XML, rileva le differenze e le scrive in un documento Diffgram in formato XML. Questa operazione include proprietà per la personalizzazione del confronto.|  
|Unione|Consente di unire due documenti XML. Utilizzando il documento XML di origine come documento di base, l'operazione Merge aggiunge il contenuto di un secondo documento al documento di base. L'operazione può specificare una posizione di unione nel documento di base.|  
|Patch|Applica l'output dell'operazione Diff, detto documento Diffgram, a un documento XML, per creare un nuovo documento padre che include il contenuto del documento Diffgram.|  
|Validate|Consente di convalidare il documento XML in base a una schema di definizione DTD (Document Type Definition) o XSD (XML Schema Definition).|  
|XPath|Consente di eseguire valutazioni e query XPath.|  
|XSLT|Consente di eseguire trasformazioni XSL in documenti XML.|  
  
### <a name="diff-operation"></a>Operazione Diff  
 L'operazione Diff può essere configurata in modo da utilizzare un algoritmo di confronto diverso a seconda che il confronto debba essere rapido o preciso. L'operazione può essere inoltre configurata in modo da selezionare automaticamente il confronto rapido o preciso, in base alle dimensioni dei documenti da confrontare.  
  
 L'operazione Diff include un set di opzioni per la personalizzazione del confronto XML, Nella tabella seguente vengono descritte le opzioni disponibili.  
  
|Opzione|Description|  
|------------|-----------------|  
|**IgnoreComments**|Valore che specifica se i nodi dei commenti devono essere confrontati.|  
|**IgnoreNamespaces**|Valore che specifica se l'URI (Uniform Resource Identifier) dello spazio dei nomi di un elemento e i nomi dei suoi attributi devono essere confrontati. Se questa opzione è impostata su `true`, due elementi con lo stesso nome locale e spazio dei nomi diverso verranno considerati identici.|  
|**IgnorePrefixes**|Valore che specifica se i prefissi degli elementi e i nomi degli attributi vengono confrontati. Se questa opzione è impostata su `true,` due elementi con lo stesso nome locale ma prefisso e URI dello spazio dei nomi diversi verranno considerati identici.|  
|**IgnoreXMLDeclaration**|Valore che specifica se le dichiarazioni XML devono essere confrontate.|  
|**IgnoreOrderOfChildElements**|Valore che specifica se l'ordine degli elementi figli viene confrontato. Se questa opzione è impostata su `true`, gli elementi figli che differiscono solo per la posizione in un elenco di elementi di pari livelli vengono considerati identici.|  
|**IgnoreWhiteSpaces**|Valore che specifica se gli spazi devono essere confrontati.|  
|**IgnoreProcessingInstructions**|Valore che specifica se le istruzioni di elaborazione devono essere confrontate.|  
|**IgnoreDTD**|Valore che specifica se il DTD deve essere ignorato.|  
  
### <a name="merge-operation"></a>Operazione Merge  
 Quando si utilizza un'istruzione XPath per identificare la posizione di unione nel documento di origine, è previsto che tale istruzione restituisca un unico nodo. Se l'istruzione restituisce più nodi, viene utilizzato solo il primo nodo. Il contenuto del secondo documento viene unito sotto il primo nodo restituito dalla query XPath.  
  
### <a name="xpath-operation"></a>Operazione XPath  
 L'operazione XPath può essere configurata in modo da utilizzare diversi tipi di funzionalità XPath.  
  
-   Per implementare funzioni XPath come sum(), selezionare l'opzione **Valutazione** .  
  
-   Per restituire come frammento XML i nodi selezionati, selezionare l'opzione **Elenco dei nodi** .  
  
-   Per restituire il valore del testo interno di tutti i nodi selezionati, concatenato in modo da formare una stringa, selezionare l'opzione **Valori** .  
  
### <a name="validation-operation"></a>Operazione Validation  
 L'operazione Validate può essere configurata in modo da utilizzare un file DTD (Document Type Definition) o uno schema XSD (XML Schema Definition).  
  
 Abilitare `ValidationDetails` per ottenere output dettagliato degli errori. Per ulteriori informazioni, vedere [Validate XML with the XML Task](xml-task.md).  
  
## <a name="xml-document-encoding"></a>Codifica dei documenti XML  
 L'attività XML supporta solo l'unione di documenti Unicode. È pertanto possibile applicare l'operazione Merge solo a documenti con codifica Unicode. Se si utilizzano altre codifiche, l'attività XML non verrà completata.  
  
> [!NOTE]  
>  Le operazioni Diff e Patch includono un'opzione che consente di ignorare la dichiarazione XML nei dati XML del secondo operando e questo consente di utilizzare documenti con altre codifiche in tali operazioni.  
  
 Per verificare se il documento XML può essere utilizzato, esaminare la dichiarazione XML. La dichiarazione deve specificare esplicitamente UTF-8, che indica la codifica Unicode a 8 bit.  
  
 Nel tag seguente è specificata la codifica Unicode a 8 bit.  
  
 `<?xml version="1.0" encoding="UTF-8"?>`  
  
## <a name="custom-logging-messages-available-on-the-xml-task"></a>Messaggi di registrazione personalizzati disponibili nell'attività XML  
 Nella tabella seguente è indicata la voce di log personalizzata disponibile per l'attività XML. Per altre informazioni, vedere [Registrazione di Integration Services &#40;SSIS&#41;](../performance/integration-services-ssis-logging.md) e [Messaggi personalizzati per la registrazione](../custom-messages-for-logging.md).  
  
|Voce di log|Description|  
|---------------|-----------------|  
|`XMLOperation`|Fornisce informazioni sull'operazione eseguita dall'attività.|  
  
## <a name="configuration-of-the-xml-task"></a>Configurazione dell'attività XML  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] o a livello di codice.  
  
 Per ulteriori informazioni sulle proprietà che è possibile impostare in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic su uno degli argomenti seguenti:  
  
-   [Editor attività XML &#40;pagina generale&#41;](../general-page-of-integration-services-designers-options.md)  
  
-   [Convalidare XML con l'attività XML](xml-task.md)  
  
-   [Pagina espressioni](../expressions/expressions-page.md)  
  
 Per ulteriori informazioni sull'impostazione delle proprietà in Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Impostare le proprietà di un'attività o di un contenitore](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="programmatic-configuration-of-the-xml-task"></a>Configurazione a livello di codice dell'attività XML  
 Per ulteriori informazioni sull'impostazione di queste proprietà a livello di codice, fare clic sull'argomento seguente:  
  
-   <xref:Microsoft.SqlServer.Dts.Tasks.XMLTask.XMLTask>  
  
## <a name="related-tasks"></a>Related Tasks  
 [Impostare le proprietà di un'attività o di un contenitore](../set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-content"></a>Contenuti correlati  
  
-   Intervento nel blog sul [componente script di destinazione XML](http://agilebi.com/jwelch/2007/06/02/xml-destination-script-component/)sul sito Web agilebi.com  
  
-   Esempio di CodePlex sull' [esempio di elaborazione di pacchetti dati XML](https://msftisprodsamples.codeplex.com/wikipage?title=SS2008!Process%20XML%20Data%20Package%20Sample&version=10&ProjectName=msftisprodsamples), su www.codeplex.com  
  
