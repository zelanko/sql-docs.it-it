---
title: Configurazione del componente script nell'editor corrispondente | Microsoft Docs
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
- SSIS Script component
- Script Component Editor
- SSIS Script component, configuring
- Script component [Integration Services], configuring
ms.assetid: 586dd799-f383-4d6d-b1a1-f09233d14f0a
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 98333f81a1e7c50434936c2df958da21366c6e9d
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "71296982"
---
# <a name="configuring-the-script-component-in-the-script-component-editor"></a>Configurazione del componente script nell'editor corrispondente

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Prima di scrivere codice personalizzato nel componente script, è necessario selezionare il tipo di componente flusso di dati che si vuole creare, ovvero origine, trasformazione o destinazione, quindi configurare i relativi metadati e le relative proprietà nell'**Editor trasformazione Script**.  
  
## <a name="selecting-the-type-of-component-to-create"></a>Selezione del tipo di componente da creare  
 Quando si aggiunge un componente script nel riquadro Flusso di dati di Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)], viene visualizzata la finestra di dialogo **Seleziona tipo componente script**. Preconfigurare il componente come origine, trasformazione o destinazione. Dopo aver eseguito la selezione iniziale, è possibile continuare a configurare il componente nell'**Editor trasformazione Script**.  
  
 Per impostare il linguaggio di scripting predefinito per il componente script, usare l'opzione **Linguaggio di scripting** nella pagina **Generale** della finestra di dialogo **Opzioni**. Per ulteriori informazioni, vedere [General Page](../../general-page-of-integration-services-designers-options.md).  
  
## <a name="understanding-the-two-design-time-modes"></a>Informazioni sulle due modalità della fase di progettazione  
 In Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] sono disponibili due modalità per il componente script: progettazione metadati e progettazione codice.  
  
 Quando si apre l'**Editor trasformazione Script**, il componente passa alla modalità di progettazione metadati. In questa modalità è possibile selezionare colonne di input e aggiungere o configurare output e colonne di output, ma non è possibile scrivere codice. Dopo aver configurato i metadati del componente, è possibile passare in modalità di progettazione codice per scrivere lo script.  
  
 Quando si passa alla modalità di progettazione codice facendo clic su **Modifica script**, il componente script blocca i metadati per impedire modifiche aggiuntive, quindi genera automaticamente il codice di base dai metadati dell'input e dell'output. Quando il codice generato automaticamente è completo, sarà possibile immettere il codice personalizzato. Il codice utilizza le classi di base generate automaticamente per elaborare le righe di input, per accedere a buffer e colonne nei buffer e per recuperare gestioni connessioni e variabili dal pacchetto, tutti come oggetti fortemente tipizzati.  
  
 Dopo aver immesso il codice personalizzato in modalità di progettazione codice, è possibile tornare in modalità di progettazione metadati. In questo modo il codice immesso non viene eliminato. Tuttavia, le successive modifiche ai metadati causano la rigenerazione della classe di base. In seguito, la convalida del componente può non riuscire perché è possibile che gli oggetti a cui fa riferimento il codice personalizzato non esistano più o siano stati modificati. In questo caso, è necessario correggere manualmente il codice in modo che possa essere compilato correttamente rispetto alla classe di base rigenerata.  
  
## <a name="configuring-the-component-in-metadata-design-mode"></a>Configurazione del componente in modalità di progettazione metadati  
 In modalità di progettazione metadati è possibile selezionare colonne di input e aggiungere e configurare output e colonne di output, ma non è possibile scrivere codice. Dopo aver configurato i metadati del componente, passare in modalità di progettazione codice per scrivere lo script.  
  
 Le proprietà che è necessario configurare nell'editor personalizzato dipendono dall'utilizzo del componente script. Il componente script può essere configurato come origine, trasformazione o destinazione. A seconda di come viene utilizzato, il componente supporta un input o più output oppure entrambi. Il codice personalizzato che verrà scritto elabora le righe e le colonne di input e output.  
  
### <a name="inputs-columns-page-of-the-script-transformation-editor"></a>Pagina Colonne di input dell'editor trasformazione Script  
 La pagina **Colonne di input** dell'**Editor trasformazione Script** viene visualizzata per trasformazioni e destinazioni, ma non per le origini. In questa pagina selezionare le colonne di input che si desidera rendere disponibili per lo script personalizzato, quindi specificare l'accesso di sola lettura o di lettura/scrittura a tali colonne.  
  
 Nel progetto di codice che verrà generato in base a questi metadati, l'elemento di progetto BufferWrapper contiene una classe per ogni input, la quale contiene proprietà delle funzioni di accesso tipizzate per ogni colonna di input selezionata. Se ad esempio si seleziona una colonna **CustomerID** integer e una colonna **CustomerName** stringa da un input denominato **CustomerInput**, l'elemento di progetto BufferWrapper conterrà una classe **CustomerInput** che deriva da <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> e la classe **CustomerInput** esporrà una proprietà integer denominata **CustomerID** e una proprietà stringa denominata **CustomerName**. Con questa convenzione è possibile scrivere codice con controllo dei tipi come riportato di seguito:  
  
```vb  
Dim currentCustomerID as Integer = CustomerInput.CustomerID  
Dim currentCustomerName as String = CustomerInput.CustomerName  
```  
  
 Per altre informazioni sulla configurazione di colonne di input per un tipo specifico di componente flusso di dati, vedere l'esempio appropriato in [Sviluppo di tipi specifici di componenti script](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md).  
  
### <a name="inputs-and-outputs-page-of-the-script-transformation-editor"></a>Pagina Input e output dell'editor trasformazione Script  
 La pagina **Input e output** dell'**Editor trasformazione Script** viene visualizzata per origini, trasformazioni e destinazioni. In questa pagina è possibile aggiungere, rimuovere e configurare input, output e colonne di output che si desidera utilizzare nello script personalizzato, con le limitazioni seguenti:  
  
-   Se utilizzato come origine, il componente script non include input e supporta più output.  
  
-   Se utilizzato come trasformazione, il componente script supporta un input e più output.  
  
-   Se utilizzato come destinazione, il componente script supporta un input e non include output.  
  
 Nel progetto di codice che verrà generato in base a questi metadati, l'elemento di progetto BufferWrapper contiene una classe per ogni input e output. Se ad esempio si crea un output denominato **CustomerOutput**, l'elemento di progetto BufferWrapper conterrà una classe **CustomerOutput** che deriva da <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptBuffer> e la classe **CustomerOutput** conterrà le proprietà delle funzioni di accesso tipizzate per ogni colonna di output creata.  
  
 È possibile configurare colonne di output solo nella pagina **Input e output**. È possibile selezionare colonne di input per trasformazioni e destinazioni nella pagina **Colonne di input**. Le proprietà delle funzioni di accesso tipizzate create nell'elemento di progetto BufferWrapper saranno di sola scrittura per le colonne di output. Le proprietà delle funzioni di accesso per le colonne di input saranno di sola lettura o di lettura/scrittura a seconda del tipo di utilizzo selezionato per ogni colonna nella pagina **Colonne di input**.  
  
 Per altre informazioni sulla configurazione di input e output per un tipo specifico di componente flusso di dati, vedere l'esempio appropriato in [Sviluppo di tipi specifici di componenti script](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md).  
  
> [!NOTE]  
>  Anche se non è possibile configurare direttamente un output come output degli errori nel componente script per la gestione automatica delle righe di errore, è possibile riprodurre la funzionalità di un output degli errori creando un output aggiuntivo e utilizzando lo script per indirizzare le righe a questo output quando è appropriato. Per altre informazioni, vedere [Simulazione di un output degli errori per il componente script](../../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md).  
  
#### <a name="exclusiongroup-and-synchronousinputid-properties-of-outputs"></a>Proprietà ExclusionGroup e SynchronousInputID degli output  
 La proprietà **ExclusionGroup** ha un valore diverso da zero solo nelle trasformazioni con output sincroni, in cui il codice esegue operazioni di filtro o diramazione e indirizza ogni riga a uno degli output che condividono lo stesso valore di **ExclusionGroup** diverso da zero. Ad esempio, la trasformazione può indirizzare le righe all'output predefinito o a un output degli errori. Quando si creano output aggiuntivi per questo scenario, assicurarsi di impostare il valore della proprietà **SynchronousInputID** sul numero intero che corrisponde al valore **ID** dell'input del componente.  
  
 La proprietà **SynchronousInputID** ha un valore diverso da zero solo nelle trasformazioni con output sincrono. Se il valore di questa proprietà è zero, significa che l'output è asincrono. Per un output sincrono, in cui le righe vengono passate all'output o agli output selezionati senza l'aggiunta di nuove righe, questa proprietà deve contenere il valore **ID** dell'input del componente.  
  
> [!NOTE]  
>  Quando l'**Editor trasformazione Script** crea il primo output, la proprietà **SynchronousInputID** dell'output viene impostata sul valore **ID** dell'input del componente. Quando l'editor crea gli output successivi, tuttavia, le proprietà **SynchronousInputID** di questi output vengono impostate su zero.  
>   
>  Se si crea un componente con output sincroni, per ogni output è necessario che la proprietà **SynchronousInputID** sia impostata sul valore **ID** dell'input del componente. È quindi necessario che il valore **SynchronousInputID** di ogni output creato dall'editor dopo il primo venga modificato da zero nel valore **ID** dell'input del componente.  
>   
>  Se si crea un componente con output asincroni, per ogni output è necessario che la proprietà **SynchronousInputID** sia impostata su zero. È quindi necessario che il valore **SynchronousInputID** del primo output venga modificato in zero dal valore **ID** dell'input del componente.  
  
 Per un esempio di indirizzamento delle righe a uno dei due output sincroni nel componente script, vedere [Creazione di una trasformazione sincrona con il componente script](../../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md).  
  
### <a name="object-names-in-generated-script"></a>Nomi di oggetti nello script generato  
 Il componente script analizza i nomi di input e output, nonché i nomi di colonne negli input e negli output, e in base a tali nomi genera classi e proprietà nell'elemento di progetto BufferWrapper. Se i nomi individuati includono caratteri che non appartengono alle categorie Unicode **UppercaseLetter**, **LowercaseLetter**, **TitlecaseLetter**, **ModifierLetter**, **OtherLetter** o **DecimalDigitLetter**, i caratteri non validi vengono eliminati nei nomi generati. Ad esempio, poiché gli spazi vengono eliminati, due colonne di input denominate **FirstName** e [**First Name**] vengono entrambe interpretate come se avessero il nome **FirstName**, con risultati imprevedibili. Per evitare questa situazione, i nomi di input e output e di colonne di input e output utilizzati dal componente script devono contenere solo caratteri delle categorie Unicode elencate in questa sezione.  
  
### <a name="script-page-of-the-script-transformation-editor"></a>Pagina Script dell'editor trasformazione Script  
 Nella pagina **Script** di **Editor attività Script** è possibile assegnare un nome univoco e una descrizione per l'attività Script. È anche possibile assegnare valori per le proprietà seguenti.  
  
> [!NOTE]  
>  In [!INCLUDE[ssISversion10](../../../includes/ssisversion10-md.md)] e versioni successive, tutti gli script sono precompilati. Nelle versioni precedenti era possibile specificare se gli script dovessero essere precompilati impostando la proprietà **Precompile** per l'attività.  
  
#### <a name="validateexternalmetadata-property"></a>Proprietà ValidateExternalMetadata  
 Il valore booleano della proprietà **ValidateExternalMetadata** specifica se il componente deve eseguire la convalida delle origini dati esterne in fase di progettazione o se deve posticiparla fino alla fase di esecuzione. Per impostazione predefinita, il valore di questa proprietà è **True**, ovvero i metadati esterni vengono convalidati sia in fase di progettazione che in fase di esecuzione. È necessario impostare il valore di questa proprietà su **False** quando un'origine dati esterna non è disponibile in fase di progettazione, ad esempio se il pacchetto scarica l'origine o crea la destinazione solo in fase di esecuzione.  
  
#### <a name="readonlyvariables-and-readwritevariables-properties"></a>Proprietà ReadOnlyVariables e ReadWriteVariables  
 È possibile immettere elenchi delimitati da virgole di variabili esistenti come valori di queste proprietà per rendere le variabili disponibili per l'accesso di sola lettura o di lettura/scrittura all'interno del codice del componente script. Le variabili sono accessibili nel codice tramite le proprietà <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadOnlyVariables%2A> e <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ReadWriteVariables%2A> della classe di base generata automaticamente. Per altre informazioni, vedere [Uso di variabili nel componente script](../../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md).  
  
> [!NOTE]  
>  Per i nomi delle variabili viene fatta distinzione tra maiuscole e minuscole.  
  
#### <a name="scriptlanguage"></a>ScriptLanguage  
 È possibile selezionare [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic o [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# come linguaggio di programmazione per il componente Script.  
  
#### <a name="edit-script-button"></a>Pulsante Modifica script  
 Il pulsante **Modifica script** consente di aprire l'IDE di [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) in cui scrivere lo script personalizzato. Per altre informazioni, vedere [Codifica e debug del componente script](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).  
  
### <a name="connection-managers-page-of-the-script-transformation-editor"></a>Pagina Gestioni connessioni dell'editor trasformazione Script  
 Nella pagina **Gestioni connessioni** dell'**Editor trasformazione Script** è possibile aggiungere e rimuovere le gestioni connessioni che si vogliono usare nello script personalizzato. Normalmente, è necessario fare riferimento a gestioni connessioni quando si crea un componente di origine o di destinazione.  
  
 Nel progetto di codice che verrà generato in base a questi metadati, l'elemento di progetto **ComponentWrapper** contiene una classe di raccolta **Connections** che include una proprietà di funzione di accesso tipizzata per ogni gestione connessione selezionata. Ogni proprietà di funzione di accesso tipizzata ha lo stesso nome della gestione connessione e restituisce un riferimento alla gestione connessione come istanza di <xref:Microsoft.SqlServer.Dts.Runtime.Wrapper.IDTSConnectionManager100>. Ad esempio, se è stata aggiunta una gestione connessione denominata `MyADONETConnection` nella pagina **Gestioni connessioni** dell'editor, è possibile ottenere un riferimento alla gestione connessione nello script tramite il codice seguente:  
  
```vb  
Dim myADONETConnectionManager As IDTSConnectionManager100 = _  
    Me.Connections.MyADONETConnection  
```  
  
 Per altre informazioni, vedere [Connessione a origini dati nel componente script](../../../integration-services/extending-packages-scripting/data-flow-script-component/connecting-to-data-sources-in-the-script-component.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Codifica e debug del componente script](../../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md)  
  
  
