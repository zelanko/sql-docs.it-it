---
title: Componente script| Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.scriptcomponentdetails.f1
- sql13.dts.designer.scriptcomponent.f1
- sql13.dts.designer.scriptcomponent.connections.f1
- sql13.dts.designer.scriptcomponent.inputcolumn.f1
- sql13.dts.designer.scriptcomponent.columnproperties.f1
- sql13.dts.designer.scriptcomponent.script.f1
helpviewer_keywords:
- Script transformation
- scripts [Integration Services], transformations
- Script component [Integration Services], about Script component
- Script component [Integration Services]
ms.assetid: 131c2d0c-2e33-4785-94af-ada5c049821e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a40336899e804ee634cf586078ec7c219f31c486
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "71297873"
---
# <a name="script-component"></a>Componente script

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Il componente Script ospita lo script e consente a un pacchetto di includere ed eseguire codice script personalizzato. È possibile utilizzare il componente script nei pacchetti per gli scopi seguenti:  
  
-   Applicare più trasformazioni ai dati anziché utilizzare più trasformazioni nel flusso di dati. Uno script può ad esempio sommare i valori in due colonne e quindi calcolare la media della somma.  
  
-   Accedere a regole business in un assembly .NET esistente. Uno script può ad esempio applicare una regola business che specifica l'intervallo dei valori validi in una colonna di nome **Income** .  
  
-   Utilizzare formule e funzioni personalizzate, in aggiunta alle funzioni e agli operatori forniti dalla grammatica delle espressioni di [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] . È ad esempio possibile convalidare i numeri delle carte di credito che usano la formula LUHN.  
  
-   Convalidare i dati delle colonne e ignorare i record che contengono dati non validi. Uno script può ad esempio stabilire se l'importo delle spese postali è ragionevole e ignorare i record che includono importi troppo alti o troppo bassi.  
  
 Il componente script consente di includere in modo facile e veloce funzioni personalizzate in un flusso di dati. Se tuttavia si prevede di riutilizzare il codice di script in più pacchetti, è preferibile creare un componente personalizzato anziché utilizzare il componente script. Per altre informazioni, vedere [Sviluppo di un componente del flusso di dati personalizzato](../../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md).  
  
> [!NOTE]  
>  Se il componente script contiene uno script che tenta di leggere il valore di una colonna NULL, quando si esegue il pacchetto si verifica un errore. È consigliabile che lo script usi il metodo <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer.IsNull%2A> per determinare se la colonna è NULL prima di tentare di leggere il valore della colonna.  
  
 Il componente script può essere utilizzato come origine, trasformazione o destinazione. Questo componente supporta un input e più output. A seconda di come viene utilizzato, il componente supporta un input o più output oppure entrambi. Lo script viene richiamato da ogni riga nell'input o nell'output.  
  
-   Se utilizzato come origine, il componente script supporta più output.  
  
-   Se utilizzato come trasformazione, il componente script supporta un input e più output.  
  
-   Se utilizzato come destinazione, il componente script supporta un input.  
  
 Il componente script non supporta output degli errori.  
  
 Una volta stabilito che il componente Script è la scelta più appropriata per il pacchetto, è necessario configurare gli input e gli output, sviluppare lo script utilizzato dal componente e configurare il componente stesso.  
  
## <a name="understanding-the-script-component-modes"></a>Informazioni sulle modalità del componente script  
 In Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] sono disponibili due modalità per il componente script: progettazione metadati e progettazione codice. In modalità progettazione metadati è possibile aggiungere e modificare gli input e gli output del componente script, ma non scrivere codice. Dopo avere configurato tutti gli input e gli output è possibile passare alla modalità progettazione codice per creare lo script. Il componente script genera automaticamente il codice di base dai metadati degli input e degli output. Se si modificano i metadati dopo la generazione del codice di base, non sarà più possibile compilare il codice perché il codice di base aggiornato potrebbe essere incompatibile con quello inserito dall'utente.  
  
## <a name="writing-the-script-that-the-component-uses"></a>Scrittura dello script utilizzato dal componente  
 Il componente script usa [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) come ambiente di scrittura degli script. Si accede a VSTA dall' **Editor trasformazione Script**. Per altre informazioni, vedere [Editor trasformazione Script &#40;pagina Script&#41;](../../../integration-services/data-flow/transformations/script-transformation-editor-script-page.md).  
  
 Il componente script fornisce un progetto VSTA che include una classe generata automaticamente, ScriptMain, che rappresenta i metadati del componente. Se ad esempio il componente script viene utilizzato come trasformazione con tre output, la classe ScriptMain includerà un metodo per ogni output. La classe ScriptMain costituisce il punto di ingresso dello script.  
  
 In VSTA sono disponibili tutte le caratteristiche standard dell'ambiente [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] , come l'editor di [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] con codifica a colori, la tecnologia IntelliSense e il Visualizzatore oggetti. Lo script utilizzato dal componente script è archiviato nella definizione del pacchetto. Durante la progettazione del pacchetto, il codice di script viene scritto temporaneamente in un file di progetto.  
  
 VSTA supporta il linguaggio di programmazione [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# e [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic.  
  
 Per altre informazioni sulla programmazione del componente Script, vedere [Estensione del flusso di dati con il componente script](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md). Per altre informazioni sulla configurazione del componente script come origine, trasformazione o destinazione, vedere [Sviluppo di tipi specifici di componenti script](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md). Per altri esempi, come una destinazione ODBC che dimostri l'uso del componente script, vedere [Ulteriori esempi di componente script](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md).  
  
> [!NOTE]  
>  A differenza delle versioni precedenti in cui era possibile indicare se gli script erano precompilati o meno, in [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)] e versioni successive tutti gli script sono precompilati. Se uno script è precompilato, il motore del linguaggio non verrà caricato in fase di esecuzione e il pacchetto verrà eseguito molto più rapidamente. I file binari precompilati occupano tuttavia una notevole quantità di spazio su disco.  
  
## <a name="configuring-the-script-component"></a>Configurazione del componente script  
 Per configurare il componente script, procedere nel modo seguente:  
  
-   Selezionare le colonne di input a cui fare riferimento.  
  
    > [!NOTE]  
    >  È possibile configurare un solo input quando si usa Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] .  
  
-   Specificare lo script che deve essere eseguito dal componente.  
  
-   Specificare il linguaggio di scripting.  
  
-   Specificare le variabili in sola lettura e in lettura e scrittura in elenchi delimitati da virgole.  
  
-   Aggiungere altri output e le colonne di output a cui lo script assegna valori.  
  
 È possibile impostare le proprietà tramite Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] o a livello di codice.  
  
### <a name="configuring-the-script-component-in-the-designer"></a>Configurazione del componente script in Progettazione  
 Per altre informazioni sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Impostazione delle proprietà di un componente del flusso di dati](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
### <a name="configuring-the-script-component-programmatically"></a>Configurazione del componente script a livello di codice  
 Per altre informazioni sulle proprietà che è possibile impostare nella finestra **Proprietà** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
-   [Proprietà personalizzate delle trasformazioni](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 Per ulteriori informazioni sulle procedure per l'impostazione delle proprietà, fare clic su uno degli argomenti seguenti:  
  
-   [Impostazione delle proprietà di un componente del flusso di dati](../../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md)  
  
## <a name="select-script-component-type"></a>Seleziona tipo componente script
  Utilizzare la finestra di dialogo **Seleziona tipo componente script** per specificare la creazione di una trasformazione Script preconfigurata da utilizzare come origine, trasformazione o destinazione.  
  
 Per altre informazioni sul componente Script, vedere [Configurazione del componente script nell'editor corrispondente](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md). Per informazioni sulla programmazione del componente Script, vedere [Estensione del flusso di dati con il componente script](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
### <a name="options"></a>Opzioni  
 La selezione dell'opzione **Origine**, **Destinazione**o **Trasformazione** influisce sulla configurazione della trasformazione Script e sulle pagine dell'editor trasformazione Script visualizzate.  
  
## <a name="script-transformation-editor-connection-managers-page"></a>Editor trasformazione Script (pagina Gestioni connessioni)
  Utilizzare la pagina **Gestioni connessioni** dell' **Editor trasformazione Script** per specificare le connessioni che verranno utilizzate dallo script.  
  
 Per altre informazioni sul componente Script, vedere [Configurazione del componente script nell'editor corrispondente](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md). Per informazioni sulla programmazione del componente Script, vedere [Estensione del flusso di dati con il componente script](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
### <a name="options"></a>Opzioni  
 **Connection managers**  
 Consente di visualizzare l'elenco delle connessioni disponibili per l'utilizzo da parte dello script.  
  
 **Nome**  
 Consente di digitare un nome descrittivo univoco per la connessione.  
  
 **Gestione connessione**  
 Selezionare una gestione connessione nell'elenco delle gestioni connessioni disponibili oppure selezionare **\<Nuova connessione>** per aprire la finestra di dialogo **Aggiungi gestione connessione SSIS**.  
  
 **Descrizione**  
 Consente di digitare una descrizione per la connessione.  
  
 **Aggiungere**  
 Consente di aggiungere un'altra connessione all'elenco **Gestioni connessioni** .  
  
 **Rimuovi**  
 Consente di rimuovere la connessione selezionata dall'elenco **Gestioni connessioni** .  
  
## <a name="script-transformation-editor-input-columns-page"></a>Editor trasformazione Script (pagina Colonne di input)
  Usare la pagina **Colonne di input** della finestra di dialogo **Editor trasformazione Script** per impostare le proprietà delle colonne di input.  
  
> [!NOTE]  
>  La pagina **Colonne di input** non viene visualizzata per i componenti di origine, che hanno output ma non input.  
  
 Per altre informazioni sul componente Script, vedere [Configurazione del componente script nell'editor corrispondente](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md). Per informazioni sulla programmazione del componente Script, vedere [Estensione del flusso di dati con il componente script](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
### <a name="options"></a>Opzioni  
 **Nome input**  
 Consente di selezionare un nome nell'elenco degli input disponibili.  
  
 **Colonne di input disponibili**  
 Utilizzando le caselle di controllo, specificare le colonne che verranno utilizzate dalla trasformazione script.  
  
 **Colonna di input**  
 Consente di selezionare una colonna di input nell'elenco delle colonne di input disponibili per ogni riga. Le opzioni selezionate corrispondono alle caselle di controllo selezionate nella tabella **Colonne di input disponibili**.  
  
 **Alias di output**  
 Consente di digitare un alias per ogni colonna di output. Per impostazione predefinita viene suggerito il nome della colonna di input. È comunque possibile scegliere qualsiasi nome descrittivo univoco.  
  
 **Tipo di utilizzo**  
 Consente di specificare se la trasformazione Script deve considerare ogni colonna come **ReadOnly** o **ReadWrite**.  
  
## <a name="script-transformation-editor-inputs-and-outputs-page"></a>Editor trasformazione Script (pagina Input e output)
  Utilizzare la pagina **Input e output** della finestra di dialogo **Editor trasformazione Script** per aggiungere, rimuovere e configurare input e output per la trasformazione script.  
  
> [!NOTE]  
>  I componenti di origine dispongono di output e di nessun input, mentre i componenti di destinazione dispongono di input e di nessun output. Le trasformazioni dispongono sia di input che di output.  
  
 Per altre informazioni sul componente Script, vedere [Configurazione del componente script nell'editor corrispondente](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md). Per informazioni sulla programmazione del componente Script, vedere [Estensione del flusso di dati con il componente script](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
### <a name="options"></a>Opzioni  
 **Inputs and outputs**  
 Selezionare un input o un output a sinistra per visualizzare le proprietà corrispondenti nella tabella a destra. Le proprietà modificabili variano in base alla selezione effettuata. Molte delle proprietà visualizzate sono di sola lettura. Per ulteriori informazioni sulle singole proprietà, vedere gli argomenti seguenti.  
  
 [Proprietà comuni](https://msdn.microsoft.com/library/51973502-5cc6-4125-9fce-e60fa1b7b796)  
  
 [Proprietà personalizzate delle trasformazioni](../../../integration-services/data-flow/transformations/transformation-custom-properties.md)  
  
 **Aggiungi output**  
 Consente di aggiungere un ulteriore output all'elenco.  
  
 **Aggiungi colonna**  
 Selezionare una cartella in cui posizionare la nuova colonna di output e quindi aggiungere la colonna facendo clic su **Aggiungi colonna**.  
  
 **Rimuovi output**  
 Selezionare un output e quindi rimuoverlo facendo clic su **Rimuovi output**.  
  
 **Rimuovi colonna**  
 Selezionare una colonna e quindi rimuoverla facendo clic su **Rimuovi colonna**.  
  
## <a name="script-transformation-editor-script-page"></a>Editor trasformazione Script (pagina Script)
  Usare la scheda **Script** della finestra di dialogo **Editor trasformazione Script** per specificare uno script e le proprietà correlate.  
  
 Per altre informazioni sul componente Script, vedere [Configurazione del componente script nell'editor corrispondente](../../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md). Per informazioni sulla programmazione del componente Script, vedere [Estensione del flusso di dati con il componente script](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
### <a name="options"></a>Opzioni  
 **Proprietà**  
 Consente di visualizzare e modificare le proprietà della trasformazione Script. Molte delle proprietà visualizzate sono di sola lettura. È possibile modificare le proprietà seguenti:  
  
|valore|Descrizione|  
|-----------|-----------------|  
|**Descrizione**|Consente di descrivere gli scopi della trasformazione Script.|  
|**LocaleID**|Consente di stabilire le impostazioni locali per specificare informazioni sul paese/area geografica relative all'ordinamento e alla conversione di data e ora.|  
|**Nome**|Consente di digitare un nome descrittivo per il componente.|  
|**ValidateExternalMetadata**|Consente di specificare se la trasformazione Script convalida i metadati delle colonne in fase di progettazione utilizzando origini dei dati esterne. Il valore **false** consente di ritardare la convalida fino al momento dell'esecuzione.|  
|**ReadOnlyVariables**|Consente di digitare un elenco delimitato da virgole delle variabili per l'accesso di sola lettura da parte della trasformazione Script.<br /><br /> Nota: per i nomi delle variabili viene fatta distinzione tra maiuscole e minuscole.|  
|**ReadWriteVariables**|Consente di digitare un elenco delimitato da virgole delle variabili per l'accesso di lettura/scrittura da parte della trasformazione Script.<br /><br /> Nota: per i nomi delle variabili viene fatta distinzione tra maiuscole e minuscole.|  
|**ScriptLanguage**|Selezionare il linguaggio di scripting che deve essere utilizzato dal componente Script.<br /><br /> Per impostare il linguaggio di scripting predefinito per componenti Script e attività Script, usare l'opzione **Linguaggio di scripting** nella pagina **Generale** della finestra di dialogo **Opzioni** .|  
|**UserComponentTypeName**|Specifica la classe <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponentHost> e l'assembly **Microsoft.SqlServer.TxScript** che supportano l'infrastruttura [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .|  
  
 **Modifica script**  
 Usare [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) per creare o modificare uno script.  
  
## <a name="related-content"></a>Contenuto correlato  
 [Trasformazioni di Integration Services](../../../integration-services/data-flow/transformations/integration-services-transformations.md)  
  
 [Estensione del flusso di dati con il componente script](../../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md)  
  
  
