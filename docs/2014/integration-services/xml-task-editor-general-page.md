---
title: Editor attività XML (pagina generale) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.xmltask.general.f1
helpviewer_keywords:
- XML Task Editor
ms.assetid: b9622c48-3243-4408-a1de-9ba20e32ff70
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 26055dde636d299a2a58fdfe0bdbd3fdfbdab012
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84972351"
---
# <a name="xml-task-editor-general-page"></a>XML Task Editor (General Page)
  Utilizzare il nodo **Generale** della finestra di dialogo **Editor attività XML** per specificare il tipo di operazione e configurarla.  
  
 Per ulteriori informazioni su questa attività, vedere [XML Task](control-flow/xml-task.md). Per ulteriori informazioni sull'utilizzo di documenti e dati XML, vedere "[Employing XML in the .NET Framework](https://go.microsoft.com/fwlink/?LinkId=56214)" (Utilizzo di codice XML in .NET Framework) in MSDN Library.  
  
## <a name="static-options"></a>Opzioni statiche  
 **Tipo operazione**  
 Selezionare il tipo di operazione dall'elenco. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Description|  
|-----------|-----------------|  
|**Convalidare**|Consente di convalidare il documento XML in base a una schema di definizione DTD (Document Type Definition) o XSD (XML Schema Definition). Selezionando questa opzione, verranno visualizzate le opzioni dinamiche nella sezione **Convalida**.|  
|**XSLT**|Consente di eseguire trasformazioni XSL in documenti XML. Selezionando questa opzione, verranno visualizzate le opzioni dinamiche nella sezione **XSLT**.|  
|**XPATH**|Consente di eseguire valutazioni e query XPath. Selezionando questa opzione, verranno visualizzate le opzioni dinamiche nella sezione **XPATH**.|  
|**Unione**|Consente di unire due documenti XML. Selezionando questa opzione, verranno visualizzate le opzioni dinamiche nella sezione **Merge**.|  
|**Diff**|Consente di confrontare due documenti XML. Selezionando questa opzione, verranno visualizzate le opzioni dinamiche nella sezione **Diff**.|  
|**Patch**|Consente di applicare l'output di un'operazione Diff per la creazione di un nuovo documento. Selezionando questa opzione, verranno visualizzate le opzioni dinamiche nella sezione **Patch**.|  
  
 **SourceType**  
 Consente di selezionare il tipo di origine del documento XML. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Description|  
|-----------|-----------------|  
|**Input diretto**|Consente di impostare l'origine su un documento XML.|  
|**Connessione file**|Consente di selezionare un file contenente il documento XML.|  
|**Variabile**|Consente di impostare l'origine su una variabile contenente il documento XML.|  
  
 **origine**  
 Se l'opzione **Origine** è impostata su **Input diretto**, specificare il codice XML oppure fare clic sul pulsante con i puntini di sospensione **(...)** e quindi indicare il codice XML usando la finestra di dialogo **Editor origine documento**.  
  
 Se l' **origine** è impostata su **connessione file**, selezionare una gestione connessione file oppure fare clic su \<**New connection...**> per creare una nuova gestione connessione.  
  
 **Argomenti correlati:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 Se l' **origine** è impostata su **variabile**, selezionare una variabile esistente oppure fare clic su **\<New variable...>** per creare una nuova variabile.  
  
 **Argomenti correlati**: [Variabili di Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md), [Aggiungi variabile](../../2014/integration-services/add-variable.md).  
  
## <a name="operationtype-dynamic-options"></a>Opzioni dinamiche OperationType  
  
### <a name="operationtype--validate"></a>OperationType = Convalida  
 Consente di specificare le opzioni per l'operazione di convalida.  
  
 **SaveOperationResult**  
 Consente di indicare se l'attività XML deve salvare l'output dell'operazione di convalida.  
  
 **OverwriteDestination**  
 Consente di indicare se sovrascrivere il file o la variabile di destinazione.  
  
 **Destinazione**  
 Selezionare una gestione connessione file esistente o fare clic su \<**New connection...**> per creare una nuova gestione connessione.  
  
 **Argomenti correlati:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 **DestinationType**  
 Consente di selezionare il tipo di destinazione del documento XML. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Description|  
|-----------|-----------------|  
|**Connessione file**|Consente di selezionare un file contenente il documento XML.|  
|**Variabile**|Consente di impostare l'origine su una variabile contenente il documento XML.|  
  
 **ValidationType**  
 Consente di selezionare il tipo di convalida. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Description|  
|-----------|-----------------|  
|**DTD**|Consente di utilizzare una definizione DTD.|  
|**XSD**|Consente di utilizzare una definizione XSD. Selezionando questa opzione, verranno visualizzate le opzioni dinamiche nella sezione **ValidationType**.|  
  
 **FailOnValidationFail**  
 Consente di indicare se l'operazione deve essere interrotta in caso di errore della convalida.  
  
 **ValidationDetails**  
 Fornisce output avanzato degli errori quando il valore di questa proprietà è True. Per ulteriori informazioni, vedere [Validate XML with the XML Task](control-flow/validate-xml-with-the-xml-task.md).  
  
### <a name="validationtype-dynamic-options"></a>Opzioni dinamiche ValidationType  
  
#### <a name="validationtype--xsd"></a>ValidationType = XSD  
 **SecondOperandType**  
 Consente di selezionare il tipo di origine del secondo documento XML. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Description|  
|-----------|-----------------|  
|**Input diretto**|Consente di impostare l'origine su un documento XML.|  
|**Connessione file**|Consente di selezionare un file contenente il documento XML.|  
|**Variabile**|Consente di impostare l'origine su una variabile contenente il documento XML.|  
  
 **SecondOperand**  
 Se la proprietà **SecondOperandType** è impostata su **Input diretto**, specificare il codice XML oppure fare clic sul pulsante con i puntini di sospensione **(...)** e quindi indicare il codice XML usando la finestra di dialogo **Editor origine**.  
  
 Se **Proprietà SecondOperandType** è impostato su **connessione file**, selezionare una gestione connessione file oppure fare clic su \<**New connection...**> per creare una nuova gestione connessione.  
  
 **Argomenti correlati:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 Se **XPathStringSourceType** è impostato su **variabile**, selezionare una variabile esistente oppure fare clic su \<**New variable...**> per creare una nuova variabile.  
  
 **Argomenti correlati**: [Variabili di Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md), [Aggiungi variabile](../../2014/integration-services/add-variable.md).  
  
### <a name="operationtype--xslt"></a>OperationType = XSLT  
 Consente di specificare le opzioni per l'operazione di trasformazione XSLT.  
  
 **SaveOperationResult**  
 Consente di indicare se l'attività XML deve salvare l'output dell'operazione di trasformazione XSLT.  
  
 **OverwriteDestination**  
 Consente di indicare se sovrascrivere il file o la variabile di destinazione.  
  
 **Destinazione**  
 Se **destinationType** è impostato su **connessione file**, selezionare una gestione connessione file oppure fare clic su \<**New connection...**> per creare una nuova gestione connessione.  
  
 **Argomenti correlati:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 Se **destinationType** è impostato su **variabile**, selezionare una variabile esistente oppure fare clic su \<**New variable...**> per creare una nuova variabile.  
  
 **Argomenti correlati**: [Variabili di Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md), [Aggiungi variabile](../../2014/integration-services/add-variable.md).  
  
 **DestinationType**  
 Consente di selezionare il tipo di destinazione del documento XML. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Description|  
|-----------|-----------------|  
|**Connessione file**|Consente di selezionare un file contenente il documento XML.|  
|**Variabile**|Consente di impostare l'origine su una variabile contenente il documento XML.|  
  
 **SecondOperandType**  
 Consente di selezionare il tipo di origine del secondo documento XML. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Description|  
|-----------|-----------------|  
|**Input diretto**|Consente di impostare l'origine su un documento XML.|  
|**Connessione file**|Consente di selezionare un file contenente il documento XML.|  
|**Variabile**|Consente di impostare l'origine su una variabile contenente il documento XML.|  
  
 **SecondOperand**  
 Se la proprietà **SecondOperandType** è impostata su **Input diretto**, specificare il codice XML oppure fare clic sul pulsante con i puntini di sospensione **(...)** e quindi indicare il codice XML usando la finestra di dialogo **Editor origine**.  
  
 Se **Proprietà SecondOperandType** è impostato su **connessione file**, selezionare una gestione connessione file oppure fare clic su \<**New connection...**> per creare una nuova gestione connessione.  
  
 **Argomenti correlati:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 Se **XPathStringSourceType** è impostato su **variabile**, selezionare una variabile esistente oppure fare clic su \<**New variable...**> per creare una nuova variabile.  
  
 **Argomenti correlati**: [Variabili di Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md), [Aggiungi variabile](../../2014/integration-services/add-variable.md).  
  
### <a name="operationtype--xpath"></a>OperationType = XPATH  
 Consente di specificare le opzioni per l'operazione XPath.  
  
 **SaveOperationResult**  
 Consente di indicare se l'attività XML deve salvare l'output dell'operazione XPath.  
  
 **OverwriteDestination**  
 Consente di indicare se sovrascrivere il file o la variabile di destinazione.  
  
 **Destinazione**  
 Se **destinationType** è impostato su **connessione file**, selezionare una gestione connessione file oppure fare clic su \<**New connection...**> per creare una nuova gestione connessione.  
  
 **Argomenti correlati:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 Se **destinationType** è impostato su **variabile**, selezionare una variabile esistente oppure fare clic su \<**New variable...**> per creare una nuova variabile.  
  
 **Argomenti correlati**: [Variabili di Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md), [Aggiungi variabile](../../2014/integration-services/add-variable.md).  
  
 **DestinationType**  
 Consente di selezionare il tipo di destinazione del documento XML. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Description|  
|-----------|-----------------|  
|**Connessione file**|Consente di selezionare un file contenente il documento XML.|  
|**Variabile**|Consente di impostare l'origine su una variabile contenente il documento XML.|  
  
 **SecondOperandType**  
 Consente di selezionare il tipo di origine del secondo documento XML. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Description|  
|-----------|-----------------|  
|**Input diretto**|Consente di impostare l'origine su un documento XML.|  
|**Connessione file**|Consente di selezionare un file contenente il documento XML.|  
|**Variabile**|Consente di impostare l'origine su una variabile contenente il documento XML.|  
  
 **SecondOperand**  
 Se la proprietà **SecondOperandType** è impostata su **Input diretto**, specificare il codice XML oppure fare clic sul pulsante con i puntini di sospensione **(...)** e quindi indicare il codice XML usando la finestra di dialogo **Editor origine**.  
  
 Se **Proprietà SecondOperandType** è impostato su **connessione file**, selezionare una gestione connessione file oppure fare clic su \<**New connection...**> per creare una nuova gestione connessione.  
  
 **Argomenti correlati:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 Se **XPathStringSourceType** è impostato su **variabile**, selezionare una variabile esistente oppure fare clic su \<**New variable...**> per creare una nuova variabile.  
  
 **Argomenti correlati**: [Variabili di Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md), [Aggiungi variabile](../../2014/integration-services/add-variable.md).  
  
 **PutResultInOneNode**  
 Consente di indicare se il risultato deve essere scritto in un singolo nodo.  
  
 **XPathOperation**  
 Consente di selezionare il tipo di risultato XPath. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Description|  
|-----------|-----------------|  
|**Valutazione**|Restituisce i risultati di una funzione XPath.|  
|**Elenco dei nodi**|Restituisce i nodi selezionati come frammento XML.|  
|**Valori**|Restituisce il valore di testo interno di tutti i nodi selezionati, concatenato all'interno di una stringa.|  
  
### <a name="operationtype--merge"></a>OperationType = Merge  
 Consente di specificare le opzioni per l'operazione di unione.  
  
 **XPathStringSourceType**  
 Consente di selezionare il tipo di origine del documento XML. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Description|  
|-----------|-----------------|  
|**Input diretto**|Consente di impostare l'origine su un documento XML.|  
|**Connessione file**|Consente di selezionare un file contenente il documento XML.|  
|**Variabile**|Consente di impostare l'origine su una variabile contenente il documento XML.|  
  
 **XPathStringSource**  
 Se la proprietà **XPathStringSourceType** è impostata su **Input diretto**, specificare il codice XML oppure fare clic sul pulsante con i puntini di sospensione **(...)** e quindi indicare il codice XML usando la finestra di dialogo **Editor origine documento**.  
  
 Se **XPathStringSourceType** è impostato su **connessione file**, selezionare una gestione connessione file oppure fare clic su \<**New connection...**> per creare una nuova gestione connessione.  
  
 **Argomenti correlati:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 Se **XPathStringSourceType** è impostato su **variabile**, selezionare una variabile esistente oppure fare clic su \<**New variable...**> per creare una nuova variabile.  
  
 **Argomenti correlati**: [Integration Services &#40;variabili di&#41; SSIS](integration-services-ssis-variables.md), [Aggiungi variabile](../../2014/integration-services/add-variable.md)  
  
 Quando si utilizza un'istruzione XPath per identificare la posizione di unione nel documento di origine, è previsto che tale istruzione restituisca un unico nodo. Se l'istruzione restituisce più nodi, viene utilizzato solo il primo nodo. Il contenuto del secondo documento viene unito sotto il primo nodo restituito dalla query XPath.  
  
 **SaveOperationResult**  
 Consente di indicare se l'attività XML deve salvare l'output dell'operazione di unione.  
  
 **OverwriteDestination**  
 Consente di indicare se sovrascrivere il file o la variabile di destinazione.  
  
 **Destinazione**  
 Se **destinationType** è impostato su **connessione file**, selezionare una gestione connessione file oppure fare clic su \<**New connection...**> per creare una nuova gestione connessione.  
  
 **Argomenti correlati:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 Se **destinationType** è impostato su **variabile**, selezionare una variabile esistente oppure fare clic su \<**New variable...**> per creare una nuova variabile.  
  
 **Argomenti correlati**: [Variabili di Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md), [Aggiungi variabile](../../2014/integration-services/add-variable.md).  
  
 **DestinationType**  
 Consente di selezionare il tipo di destinazione del documento XML. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Description|  
|-----------|-----------------|  
|**Connessione file**|Consente di selezionare un file contenente il documento XML.|  
|**Variabile**|Consente di impostare l'origine su una variabile contenente il documento XML.|  
  
 **SecondOperandType**  
 Consente di selezionare il tipo di destinazione del secondo documento XML. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Description|  
|-----------|-----------------|  
|**Input diretto**|Consente di impostare l'origine su un documento XML.|  
|**Connessione file**|Consente di selezionare un file contenente il documento XML.|  
|**Variabile**|Consente di impostare l'origine su una variabile contenente il documento XML.|  
  
 **SecondOperand**  
 Se la proprietà **SecondOperandType** è impostata su **Input diretto**, specificare il codice XML oppure fare clic sul pulsante con i puntini di sospensione **(...)** e quindi indicare il codice XML usando la finestra di dialogo **Editor origine documento**.  
  
 Se **Proprietà SecondOperandType** è impostato su **connessione file**, selezionare una gestione connessione file oppure fare clic su \<**New connection...**> per creare una nuova gestione connessione.  
  
 **Argomenti correlati:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 Se **Proprietà SecondOperandType** è impostato su **variabile**, selezionare una variabile esistente oppure fare clic su \<**New variable...**> per creare una nuova variabile.  
  
 **Argomenti correlati**: [Integration Services &#40;variabili di&#41; SSIS](integration-services-ssis-variables.md), [Aggiungi variabile](../../2014/integration-services/add-variable.md)  
  
### <a name="operationtype--diff"></a>OperationType = Diff  
 Consente di specificare le opzioni per l'operazione Diff.  
  
 **DiffAlgorithm**  
 Consente di selezionare l'algoritmo Diff da utilizzare per il confronto dei documenti. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Description|  
|-----------|-----------------|  
|**Auto**|Fa sì che l'attività XML determini automaticamente se utilizzare l'algoritmo veloce o esatto.|  
|**Veloce**|Consente di utilizzare un algoritmo Diff veloce, ma meno preciso.|  
|**Preciso**|Consente di utilizzare un algoritmo Diff preciso.|  
  
 **Opzioni Diff**  
 Consente di impostare le opzioni Diff da applicare all'operazione Diff. Nella tabella seguente vengono elencate le opzioni.  
  
|valore|Description|  
|-----------|-----------------|  
|**IgnoreXMLDeclaration**|Consente di indicare se confrontare la dichiarazione XML.|  
|**IgnoreDTD**|Consente di indicare se ignorare la definizione DTD.|  
|**IgnoreWhiteSpaces**|Consente di specificare se ignorare le differenze riguardanti la quantità di spazio bianco nel confronto tra documenti.|  
|**IgnoreNamespaces**|Consente di indicare se confrontare l'URL dello spazio dei nomi di un elemento e i nomi dei relativi attributi.<br /><br /> Nota: se questa opzione è impostata su `True`, due elementi che hanno lo stesso nome locale ma spazi dei nomi diversi verranno considerati identici.|  
|**IgnoreProcessingInstructions**|Consente di indicare se confrontare le istruzioni di elaborazione.|  
|**IgnoreOrderOfChildElements**|Consente di indicare se confrontare l'ordine degli elementi figlio.<br /><br /> Nota: se questa opzione è impostata su `True`, gli elementi figlio che differiscono solo per la posizione in un elenco di elementi di pari livello verranno considerati identici.|  
|**IgnoreComments**|Consente di indicare se confrontare i nodi di commento.|  
|**IgnorePrefixes**|Consente di indicare se confrontare i prefissi dei nomi degli elementi e degli attributi.<br /><br /> Nota: se questa opzione è impostata su `True`, due elementi che hanno lo stesso nome locale ma prefissi e URL dello spazio dei nomi diversi verranno considerati identici.|  
  
 **FailOnDifference**  
 Consente di indicare se l'attività deve essere interrotta in caso di errore dell'operazione Diff.  
  
 **SaveDiffGram**  
 Consente di indicare se salvare il risultato del confronto, un documento DiffGram.  
  
 **SaveOperationResult**  
 Consente di indicare se l'attività XML deve salvare l'output dell'operazione Diff.  
  
 **OverwriteDestination**  
 Consente di indicare se sovrascrivere il file o la variabile di destinazione.  
  
 **Destinazione**  
 Se **destinationType** è impostato su **connessione file**, selezionare una gestione connessione file oppure fare clic su \<**New connection...**> per creare una nuova gestione connessione.  
  
 **Argomenti correlati:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 Se **destinationType** è impostato su **variabile**, selezionare una variabile esistente oppure fare clic su \<**New variable...**> per creare una nuova variabile.  
  
 **Argomenti correlati**: [Variabili di Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md), [Aggiungi variabile](../../2014/integration-services/add-variable.md).  
  
 **DestinationType**  
 Consente di selezionare il tipo di destinazione del documento XML. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Description|  
|-----------|-----------------|  
|**Connessione file**|Consente di selezionare un file contenente il documento XML.|  
|**Variabile**|Consente di impostare l'origine su una variabile contenente il documento XML.|  
  
 **SecondOperandType**  
 Consente di selezionare il tipo di destinazione del documento XML. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Description|  
|-----------|-----------------|  
|**Input diretto**|Consente di impostare l'origine su un documento XML.|  
|**Connessione file**|Consente di selezionare un file contenente il documento XML.|  
|**Variabile**|Consente di impostare l'origine su una variabile contenente il documento XML.|  
  
 **SecondOperand**  
 Se la proprietà **SecondOperandType** è impostata su **Input diretto**, specificare il codice XML oppure fare clic sul pulsante con i puntini di sospensione **(...)** e quindi indicare il codice XML usando la finestra di dialogo **Editor origine documento**.  
  
 Se **Proprietà SecondOperandType** è impostato su **connessione file**, selezionare una gestione connessione file oppure fare clic su \<**New connection...**> per creare una nuova gestione connessione.  
  
 **Argomenti correlati:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 Se **Proprietà SecondOperandType** è impostato su **variabile**, selezionare una variabile esistente oppure fare clic su \<**New variable...**> per creare una nuova variabile.  
  
 **Argomenti correlati**: [Integration Services &#40;variabili di&#41; SSIS](integration-services-ssis-variables.md), [Aggiungi variabile](../../2014/integration-services/add-variable.md)  
  
### <a name="operationtype--patch"></a>OperationType = Patch  
 Consente di specificare le opzioni per l'operazione Patch.  
  
 **SaveOperationResult**  
 Consente di indicare se l'attività XML deve salvare l'output dell'operazione Patch.  
  
 **OverwriteDestination**  
 Consente di indicare se sovrascrivere il file o la variabile di destinazione.  
  
 **Destinazione**  
 Se **destinationType** è impostato su **connessione file**, selezionare una gestione connessione file oppure fare clic su \<**New connection...**> per creare una nuova gestione connessione.  
  
 **Argomenti correlati:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 Se **destinationType** è impostato su **variabile**, selezionare una variabile esistente oppure fare clic su \<**New variable...**> per creare una nuova variabile.  
  
 **Argomenti correlati**: [Variabili di Integration Services &#40;SSIS&#41;](integration-services-ssis-variables.md), [Aggiungi variabile](../../2014/integration-services/add-variable.md).  
  
 **DestinationType**  
 Consente di selezionare il tipo di destinazione del documento XML. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Description|  
|-----------|-----------------|  
|**Connessione file**|Consente di selezionare un file contenente il documento XML.|  
|**Variabile**|Consente di impostare l'origine su una variabile contenente il documento XML.|  
  
 **SecondOperandType**  
 Consente di selezionare il tipo di destinazione del documento XML. Per questa proprietà sono disponibili le opzioni elencate nella tabella seguente.  
  
|valore|Description|  
|-----------|-----------------|  
|**Input diretto**|Consente di impostare l'origine su un documento XML.|  
|**Connessione file**|Consente di selezionare un file contenente il documento XML.|  
|**Variabile**|Consente di impostare l'origine su una variabile contenente il documento XML.|  
  
 **SecondOperand**  
 Se la proprietà **SecondOperandType** è impostata su **Input diretto**, specificare il codice XML oppure fare clic sul pulsante con i puntini di sospensione **(...)** e quindi indicare il codice XML usando la finestra di dialogo **Editor origine documento**.  
  
 Se **Proprietà SecondOperandType** è impostato su **connessione file**, selezionare una gestione connessione file oppure fare clic su \<**New connection...**> per creare una nuova gestione connessione.  
  
 **Argomenti correlati:** [File Connection Manager](connection-manager/file-connection-manager.md), [File Connection Manager Editor](../../2014/integration-services/file-connection-manager-editor.md)  
  
 Se **Proprietà SecondOperandType** è impostato su **variabile**, selezionare una variabile esistente oppure fare clic su \<**New variable...**> per creare una nuova variabile.  
  
 **Argomenti correlati**: [Integration Services &#40;variabili di&#41; SSIS](integration-services-ssis-variables.md), [Aggiungi variabile](../../2014/integration-services/add-variable.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Integration Services riferimento a errori e messaggi](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Pagina Espressioni](expressions/expressions-page.md)  
  
  
