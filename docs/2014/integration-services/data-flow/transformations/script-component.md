---
title: Componente script| Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.scriptcomponentdetails.f1
helpviewer_keywords:
- Script transformation
- scripts [Integration Services], transformations
- Script component [Integration Services], about Script component
- Script component [Integration Services]
ms.assetid: 131c2d0c-2e33-4785-94af-ada5c049821e
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 65a5c846313ad6d7d840c272c23c16698530547f
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/26/2020
ms.locfileid: "85437558"
---
# <a name="script-component"></a>Componente script
  Il componente Script ospita lo script e consente a un pacchetto di includere ed eseguire codice script personalizzato. È possibile utilizzare il componente script nei pacchetti per gli scopi seguenti:  
  
-   Applicare più trasformazioni ai dati anziché utilizzare più trasformazioni nel flusso di dati. Uno script può ad esempio sommare i valori in due colonne e quindi calcolare la media della somma.  
  
-   Accedere a regole business in un assembly .NET esistente. Uno script può ad esempio applicare una regola business che specifica l'intervallo dei valori validi in una colonna di nome `Income`.  
  
-   Utilizzare formule e funzioni personalizzate, in aggiunta alle funzioni e agli operatori forniti dalla grammatica delle espressioni di [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] . È ad esempio possibile convalidare i numeri delle carte di credito che usano la formula LUHN.  
  
-   Convalidare i dati delle colonne e ignorare i record che contengono dati non validi. Uno script può ad esempio stabilire se l'importo delle spese postali è ragionevole e ignorare i record che includono importi troppo alti o troppo bassi.  
  
 Il componente script consente di includere in modo facile e veloce funzioni personalizzate in un flusso di dati. Se tuttavia si prevede di riutilizzare il codice di script in più pacchetti, è preferibile creare un componente personalizzato anziché utilizzare il componente script. Per altre informazioni, vedere [Sviluppo di un componente del flusso di dati personalizzato](../../extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md).  
  
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
 Il componente script usa [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] Tools for Applications (VSTA) come ambiente di scrittura degli script. Si accede a VSTA dall' **Editor trasformazione Script**. Per altre informazioni, vedere [Editor trasformazione Script &#40;pagina Script&#41;](../../script-transformation-editor-script-page.md).  
  
 Il componente script fornisce un progetto VSTA che include una classe generata automaticamente, ScriptMain, che rappresenta i metadati del componente. Se ad esempio il componente script viene utilizzato come trasformazione con tre output, la classe ScriptMain includerà un metodo per ogni output. La classe ScriptMain costituisce il punto di ingresso dello script.  
  
 In VSTA sono disponibili tutte le caratteristiche standard dell'ambiente [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] , come l'editor di [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] con codifica a colori, la tecnologia IntelliSense e il Visualizzatore oggetti. Lo script utilizzato dal componente script è archiviato nella definizione del pacchetto. Durante la progettazione del pacchetto, il codice di script viene scritto temporaneamente in un file di progetto.  
  
 VSTA supporta il linguaggio di programmazione [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual C# e [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Visual Basic.  
  
 Per altre informazioni sulla programmazione del componente Script, vedere [Estensione del flusso di dati con il componente script](script-component.md). Per altre informazioni sulla configurazione del componente script come origine, trasformazione o destinazione, vedere [Sviluppo di tipi specifici di componenti script](../../extending-packages-scripting-data-flow-script-component-types/developing-specific-types-of-script-components.md). Per altri esempi, come una destinazione ODBC che dimostri l'uso del componente script, vedere [Ulteriori esempi di componente script](../../extending-packages-scripting-data-flow-script-component-examples/additional-script-component-examples.md).  
  
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
 Per altre informazioni sulle proprietà che è possibile impostare nella finestra di dialogo **Editor trasformazione Script**, fare clic su uno degli argomenti seguenti:  
  
-   [Editor trasformazione Script &#40;pagina Colonne di input&#41;](../../script-transformation-editor-input-columns-page.md)  
  
-   [Editor trasformazione Script &#40;pagina Input e output&#41;](../../script-transformation-editor-inputs-and-outputs-page.md)  
  
-   [Editor trasformazione Script &#40;pagina Script&#41;](../../script-transformation-editor-script-page.md)  
  
-   [Editor trasformazione Script &#40;pagina Gestioni connessioni&#41;](../../script-transformation-editor-connection-managers-page.md)  
  
 Per altre informazioni sull'impostazione di queste proprietà in Progettazione [!INCLUDE[ssIS](../../../includes/ssis-md.md)] , fare clic sull'argomento seguente:  
  
-   [Impostazione delle proprietà di un componente del flusso di dati](../set-the-properties-of-a-data-flow-component.md)  
  
### <a name="configuring-the-script-component-programmatically"></a>Configurazione del componente script a livello di codice  
 Per altre informazioni sulle proprietà che è possibile impostare nella finestra **Proprietà** o a livello di codice, fare clic su uno degli argomenti seguenti:  
  
-   [Proprietà comuni](../../common-properties.md)  
  
-   [proprietà personalizzate della trasformazione](transformation-custom-properties.md)  
  
 Per ulteriori informazioni sulle procedure per l'impostazione delle proprietà, fare clic su uno degli argomenti seguenti:  
  
-   [Impostazione delle proprietà di un componente del flusso di dati](../set-the-properties-of-a-data-flow-component.md)  
  
## <a name="related-content"></a>Contenuto correlato  
 [Trasformazioni di Integration Services](integration-services-transformations.md)  
  
 [Estensione del flusso di dati con il componente script](script-component.md)  
  
  
