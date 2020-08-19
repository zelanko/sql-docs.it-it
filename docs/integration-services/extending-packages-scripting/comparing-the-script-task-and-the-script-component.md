---
description: Confronto tra l'attività Script e il componente script
title: Confronto tra l'attività Script e il componente script | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- Script task [Integration Services], comparing to Script component
- Script component [Integration Services], comparing to Script task
ms.assetid: 4b73753a-4239-491b-b7a6-abc63ba83d2d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 732de7f6d7c9e75d436dca721b370f63a46a4c60
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88430323"
---
# <a name="comparing-the-script-task-and-the-script-component"></a>Confronto tra l'attività Script e il componente script

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  L'attività Script, disponibile nella finestra Flusso di controllo di Progettazione [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], e il componente Script, disponibile nella finestra Flusso di dati, hanno scopi molto diversi in un pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. L'attività è uno strumento generico del flusso di controllo, mentre il componente funge da origine, trasformazione o destinazione nel flusso di dati. Nonostante gli scopi diversi, tuttavia, l'attività Script e il componente script presentano analogie negli strumenti di creazione di codice che utilizzano e negli oggetti del pacchetto che rendono disponibili per lo sviluppatore. Identificando le analogie e le differenze, sarà possibile utilizzare l'attività e il componente in modo più efficace.  
  
## <a name="similarities-between-the-script-task-and-the-script-component"></a>Analogie tra l'attività Script e il componente script  
 L'attività Script e il componente Script condividono le caratteristiche comuni seguenti.  
  
|Feature|Descrizione|  
|-------------|-----------------|  
|Due modalità della fase di progettazione|Nell'attività e nel componente si inizia specificando proprietà nell'editor e quindi si passa all'ambiente di sviluppo per scrivere codice.|  
|[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA)|L'attività e il componente utilizzano entrambi lo stesso IDE di VSTA e supportano codice scritto in [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C#.|  
|Script precompilati|A partire da [!INCLUDE[ssISversion10](../../includes/ssisversion10-md.md)] tutti gli script sono precompilati. Nelle versioni precedenti è possibile specificare se gli script sono precompilati.<br /><br /> Lo script è precompilato in codice binario, permettendo un'esecuzione più veloce, ma a discapito dell'aumento delle dimensioni dei pacchetti.|  
|Debug|L'attività e il componente supportano entrambi i punti di interruzione e l'esecuzione di codice istruzione per istruzione durante il debug in un ambiente di progettazione. Per altre informazioni, vedere [Scrittura di codice e debug dell'attività Script](../../integration-services/extending-packages-scripting/task/coding-and-debugging-the-script-task.md) e [Codifica e debug del componente Script](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).|  
  
## <a name="differences-between-the-script-task-and-the-script-component"></a>Differenze tra l'attività Script e il componente script  
 L'attività Script e il componente script presentano le seguenti differenze di rilievo.  
  
|Feature|Attività Script|Componente script|  
|-------------|-----------------|----------------------|  
|Flusso di controllo/flusso di dati|L'attività Script viene configurata nella scheda Flusso di controllo della finestra di progettazione e viene eseguita all'esterno del flusso di dati del pacchetto.|Il componente script viene configurato nella pagina Flusso di dati della finestra di progettazione e rappresenta un'origine, una trasformazione o una destinazione nell'attività Flusso di dati.|  
|Scopo|Un'attività Script è in grado di completare qualsiasi attività generica.|È necessario specificare se si desidera creare un'origine, una trasformazione o una destinazione con il componente script.|  
|Esecuzione|Un'attività Script esegue codice personalizzato in un punto del flusso di lavoro del pacchetto. Se non viene inserita in un contenitore Ciclo o in un gestore eventi, viene eseguita una sola volta.|Anche un componente script viene eseguito una sola volta, ma in genere esegue la propria routine di elaborazione principale una volta per ogni riga di dati del flusso di dati.|  
|Editor|**Editor attività Script** include tre pagine: **Generale**, **Script** e **Espressioni**. Solo le proprietà **ReadOnlyVariables**, **ReadWriteVariables** e **ScriptLanguage** influiscono direttamente sul codice che è possibile scrivere.|**Editor trasformazione Script** può includere fino a quattro pagine: **Colonne di input**, **Input e output**, **Script** e **Gestioni connessioni**. I metadati e le proprietà che si configurano in ognuna di queste pagine determinano i membri delle classi di base generate automaticamente che è possibile utilizzare nel codice.|  
|Interazione con il pacchetto|Nel codice scritto per un'attività Script si usa la proprietà **Dts** per accedere ad altre funzionalità del pacchetto. La proprietà **Dts** è un membro della classe **ScriptMain**.|Nel codice del componente script si utilizzano le proprietà delle funzioni di accesso tipizzate per accedere a determinate caratteristiche del pacchetto, ad esempio variabili e gestioni connessioni.<br /><br /> Il metodo **PreExecute** può accedere unicamente a variabili di sola lettura. Il metodo **PostExecute** può accedere sia a variabili di sola lettura sia a variabili di lettura/scrittura.<br /><br /> Per ulteriori informazioni su questi metodi, vedere [Codifica e debug del componente script](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).|  
|Utilizzo di variabili|L'attività Script usa la proprietà <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Variables%2A> dell'oggetto **Dts** per accedere a variabili disponibili tramite le proprietà <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask.ReadOnlyVariables%2A> e <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptTask.ReadWriteVariables%2A> dell'attività. Ad esempio:<br /><br /> [Visual Basic]<br /><br /> `Dim myVar as String` <br /> `myVar = Dts.Variables("MyStringVariable").Value.ToString`<br /><br /> [C#]<br /><br /> `string myVar;` <br /> `myVar = Dts.Variables["MyStringVariable"].Value.ToString();`|Il componente Script usa le proprietà delle funzioni di accesso tipizzate della classe di base generata automaticamente, create dalle proprietà <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadOnlyVariables%2A> e <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadWriteVariables%2A> del componente. Ad esempio:<br /><br /> [Visual Basic]<br /><br /> `Dim myVar as String` <br /> `myVar = Me.Variables.MyStringVariable`<br /><br /> [C#]<br /><br /> `string myVar;` <br /> `myVar = this.Variables.MyStringVariable;`|  
|Utilizzo delle connessioni|L'attività Script usa la proprietà <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Connections%2A> dell'oggetto **Dts** per accedere alle gestioni connessioni definite nel pacchetto. Ad esempio:<br /><br /> [Visual Basic]<br /><br /> `Dim myFlatFileConnection As String` <br /> `myFlatFileConnection = _     DirectCast(Dts.Connections("Test Flat File Connection").AcquireConnection(Dts.Transaction), _     String)`<br /><br /> [C#]<br /><br /> `string myFlatFileConnection;` <br /> `myFlatFileConnection = (Dts.Connections["Test Flat File Connection"].AcquireConnection(Dts.Transaction) as String);`|Il componente script utilizza le proprietà delle funzioni di accesso tipizzate della classe di base generata automaticamente, create dall'elenco di gestioni connessioni immesso dall'utente nella pagina corrispondente dell'editor. Ad esempio:<br /><br /> [Visual Basic]<br /><br /> `Dim connMgr As IDTSConnectionManager100` <br /> `connMgr = Me.Connections.MyADONETConnection`<br /><br /> [C#]<br /><br /> `IDTSConnectionManager100 connMgr;` <br /> `connMgr = this.Connections.MyADONETConnection;`|  
|Generazione di eventi|L'attività Script usa la proprietà <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Events%2A> dell'oggetto **Dts** per generare eventi. Ad esempio:<br /><br /> [Visual Basic]<br /><br /> `Dts.Events.FireError(0, "Event Snippet", _     ex.Message & ControlChars.CrLf & ex.StackTrace, _     "", 0)`<br /><br /> [C#]<br /><br /> `Dts.Events.FireError(0, "Event Snippet", ex.Message + "\r" + ex.StackTrace, "", 0);`|Il componente script genera errori, avvisi e messaggi informativi utilizzando i metodi dell'interfaccia <xref:Microsoft.SqlServer.Dts.Pipeline.Wrapper.IDTSComponentMetaData100> restituita dalla proprietà <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ComponentMetaData%2A>. Ad esempio:<br /><br /> [Visual Basic]<br /><br /> `Dim myMetadata as IDTSComponentMetaData100 myMetaData = Me.ComponentMetaData myMetaData.FireError(...)`|  
|Registrazione|L'attività Script usa il metodo <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.Log%2A> dell'oggetto **Dts** per registrare informazioni nei provider di log abilitati. Ad esempio:<br /><br /> [Visual Basic]<br /><br /> `Dim bt(0) As Byte Dts.Log("Test Log Event", _     0, _     bt)`<br /><br /> [C#]<br /><br /> `byte[] bt = new byte[0];` <br /> `Dts.Log("Test Log Event", 0, bt);`|Il componente script utilizza il metodo <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.Log%2A> della classe di base generata automaticamente per registrare informazioni nei provider di log abilitati. Ad esempio:<br /><br /> [Visual Basic]<br /><br /> `Dim bt(0) As Byte`<br /><br /> `Me.Log("Test Log Event", _`<br /><br /> `0, _`<br /><br /> `bt)`<br /><br /> [C#]<br /><br /> `byte[] bt = new byte[0]; this.Log("Test Log Event", 0, bt);`|  
|Restituzione di risultati|L'attività Script usa sia la proprietà <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.TaskResult%2A> che la proprietà facoltativa <xref:Microsoft.SqlServer.Dts.Tasks.ScriptTask.ScriptObjectModel.ExecutionValue%2A> dell'oggetto **Dts** per notificare i risultati al runtime.|Il componente script viene eseguito come parte dell'attività Flusso di dati e non restituisce risultati utilizzando queste proprietà.|  
  
## <a name="see-also"></a>Vedere anche  
 [Estensione del pacchetto con l'attività Script](../../integration-services/extending-packages-scripting/task/extending-the-package-with-the-script-task.md)   
 [Estensione del flusso di dati con il componente script](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)   
  
  
