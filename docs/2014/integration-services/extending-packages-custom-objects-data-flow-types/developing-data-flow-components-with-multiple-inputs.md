---
title: Sviluppo di componenti flusso di dati con più input | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
ms.assetid: 3c7b50e8-2aa6-4f6a-8db4-e8293bc21027
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 334d197e9b251225b3ebe7df4445e47f42131075
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52771253"
---
# <a name="developing-data-flow-components-with-multiple-inputs"></a>Sviluppo di componenti flusso di dati con più input
  Un componente flusso di dati con più input può usare una quantità di memoria eccessiva se i relativi input generano dati a frequenze irregolari. Quando si sviluppa un componente flusso di dati personalizzato in grado di supportare due o più input, è possibile gestire l'utilizzo elevato di memoria tramite i membri dello spazio dei nomi Microsoft.SqlServer.Dts.Pipeline seguenti:  
  
-   Proprietà <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> della classe <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>. Impostare il valore di questa proprietà su `true` per implementare il codice necessario affinché il componente flusso di dati personalizzato gestisca i dati generati a frequenze irregolari.  
  
-   Metodo <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> della classe <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>. È necessario fornire un'implementazione di questo metodo se si imposta la proprietà <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> su `true`. Se non si fornisce un'implementazione, nel motore del flusso di dati viene generata un'eccezione durante la fase di esecuzione.  
  
-   Metodo <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> della classe <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>. È inoltre necessario fornire un'implementazione di questo metodo se si imposta la proprietà <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> su `true` e il componente personalizzato supporta più di due input. Se non si fornisce un'implementazione, nel motore del flusso di dati viene generata un'eccezione durante la fase di esecuzione se l'utente collega più di due input.  
  
 Insieme, questi membri consentono di sviluppare una soluzione per richieste elevate di memoria simili alla soluzione sviluppata da Microsoft per le trasformazioni Merge e Merge join.  
  
## <a name="setting-the-supportsbackpressure-property"></a>Impostazione della proprietà SupportsBackPressure  
 Il primo passaggio necessario per implementare una migliore gestione della memoria per un componente flusso di dati personalizzato che supporta più input consiste nell'impostare il valore della proprietà <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> su `true` in <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>. Quando il valore di <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> è `true`, il motore del flusso di dati chiama il metodo <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> e se sono presenti più di due input chiama anche il metodo <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> durante la fase di esecuzione.  
  
### <a name="example"></a>Esempio  
 Nell'esempio seguente l'implementazione di <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute> comporta l'impostazione del valore di <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> su `true`.  
  
```csharp  
[DtsPipelineComponent(ComponentType = ComponentType.Transform,  
        DisplayName = "Shuffler",  
        Description = "Shuffle the rows from input.",  
        SupportsBackPressure = true,  
        LocalizationType = typeof(Localized),  
        IconResource = "Microsoft.Samples.SqlServer.Dts.MIBPComponent.ico")  
]  
public class Shuffler : Microsoft.SqlServer.Dts.Pipeline.PipelineComponent  
        {  
          ...  
        }  
```  
  
## <a name="implementing-the-isinputready-method"></a>Implementazione del metodo IsInputReady  
 Quando si imposta il valore della proprietà <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute.SupportsBackPressure%2A> su `true` nell'oggetto <xref:Microsoft.SqlServer.Dts.Pipeline.DtsPipelineComponentAttribute>, è necessario fornire un'implementazione per il metodo <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> della classe <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>.  
  
> [!NOTE]  
>  L'implementazione del metodo <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> non deve chiamare le implementazioni nella classe di base. L'implementazione predefinita di questo metodo nella classe di base causa semplicemente la generazione di un'eccezione `NotImplementedException`.  
  
 Quando si implementa questo metodo, si imposta lo stato di un elemento nella matrice *NotImplementedException* booleana per ogni input del componente. Gli input sono identificabili tramite i relativi valori ID nella matrice *inputIDs*. Quando si imposta il valore di un elemento nel *canProcess* matrice `true` per un input, il motore flusso di dati chiama il componente <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> (metodo) e offre maggiore quantità di dati per l'input specificato.  
  
 Anche se sono disponibili più dati upstream, il valore della *canProcess* elemento di matrice per almeno un input deve essere sempre `true`, l'elaborazione viene arrestata.  
  
 Il motore del flusso di dati chiama il metodo <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> prima di inviare ogni buffer di dati per determinare quali input sono in attesa di ricevere altri dati. Quando il valore restituito indica che un input è bloccato, il motore del flusso di dati memorizza temporaneamente nella cache buffer aggiuntivi di dati per l'input anziché inviarli al componente.  
  
> [!NOTE]  
>  Il metodo <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> o <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> non viene chiamato nel codice personalizzato. Il motore del flusso di dati chiama questi metodi e gli altri metodi della classe `PipelineComponent` di cui si esegue l'override, quando nel motore del flusso di dati viene eseguito il componente.  
  
### <a name="example"></a>Esempio  
 Nell'esempio seguente l'implementazione del metodo <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> indica che un input è in attesa di ricevere altri dati quando sussistono le condizioni seguenti:  
  
-   È disponibile una maggiore quantità di dati upstream per l'input (`!inputEOR`).  
  
-   Per il componente non sono attualmente disponibili dati da elaborare per l'input nei buffer già ricevuti dal componente (`inputBuffers[inputIndex].CurrentRow() == null`).  
  
 Se un input è in attesa di ricevere altri dati, il componente del flusso di dati indica questa impostazione per `true` il valore dell'elemento nel *canProcess* array che corrisponde a quell'input.  
  
 Viceversa, se per il componente sono ancora disponibili dati da elaborare per l'input, viene sospesa l'elaborazione dell'input. L'esempio esegue questa impostazione per `false` il valore dell'elemento nel *canProcess* array che corrisponde a quell'input.  
  
```csharp  
public override void IsInputReady(int[] inputIDs, ref bool[] canProcess)  
{  
    for (int i = 0; i < inputIDs.Length; i++)  
    {  
        int inputIndex = ComponentMetaData.InputCollection.GetObjectIndexByID(inputIDs[i]);  
  
        canProcess[i] = (inputBuffers[inputIndex].CurrentRow() == null)  
            && !inputEOR[inputIndex];  
    }  
}  
```  
  
 Nell'esempio precedente viene usata la matrice `inputEOR` booleana per indicare se sono disponibili più dati upstream per ogni input. `EOR` nel nome della matrice rappresenta "la fine del set di righe" e fa riferimento alla proprietà <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> dei buffer del flusso di dati. In una parte dell'esempio non inclusa in questo argomento, il metodo <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.ProcessInput%2A> controlla il valore della proprietà <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineBuffer.EndOfRowset%2A> per ogni buffer di dati ricevuto. Se un valore `true` indica che per un input non sono disponibili altri dati upstream, il valore dell'elemento di matrice `inputEOR` per quell'input viene impostato su `true`. In questo esempio del <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> metodo imposta il valore dell'elemento corrispondente nel *canProcess* matrice `false` per un input quando il valore del `inputEOR` elemento della matrice indica che vi sia nessun altro upstream sono disponibili dati per l'input.  
  
## <a name="implementing-the-getdependentinputs-method"></a>Implementazione del metodo GetDependentInputs  
 Se il componente flusso di dati personalizzato supporta più di due input, è necessario fornire un'implementazione per il metodo <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> della classe <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent>.  
  
> [!NOTE]  
>  L'implementazione del metodo <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> non deve chiamare le implementazioni nella classe di base. L'implementazione predefinita di questo metodo nella classe di base causa semplicemente la generazione di un'eccezione `NotImplementedException`.  
  
 Il motore del flusso di dati chiama solo il metodo <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> quando l'utente collega più di due input al componente. Quando un componente dispone solo di due input e il <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> metodo indica che un input è bloccato (*canProcess* = `false`), il motore flusso di dati riconosce che l'altro input è in attesa di ricevere altri dati. Se tuttavia sono presenti più di due input e il metodo <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> indica che un input è bloccato, il codice aggiuntivo nel metodo <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> identifica quali input sono in attesa di ricevere altri dati.  
  
> [!NOTE]  
>  Il metodo <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.IsInputReady%2A> o <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> non viene chiamato nel codice personalizzato. Il motore del flusso di dati chiama questi metodi e gli altri metodi della classe `PipelineComponent` di cui si esegue l'override, quando nel motore del flusso di dati viene eseguito il componente.  
  
### <a name="example"></a>Esempio  
 Per un input specifico bloccato, l'implementazione seguente del metodo <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> restituisce una raccolta degli input in attesa di ricevere altri dati che quindi bloccano l'input specificato. Il componente identifica gli input di blocco cercando gli input diversi da quello bloccato per i quali non sono attualmente disponibili dati da elaborare nei buffer già ricevuti dal componente (`inputBuffers[i].CurrentRow() == null`). Il metodo <xref:Microsoft.SqlServer.Dts.Pipeline.PipelineComponent.GetDependentInputs%2A> restituisce quindi la raccolta di input di blocco come una raccolta di ID di input.  
  
```csharp  
public override Collection<int> GetDependentInputs(int blockedInputID)  
{  
    Collection<int> currentDependencies = new Collection<int>();  
    for (int i = 0; i < ComponentMetaData.InputCollection.Count; i++)  
    {  
        if (ComponentMetaData.InputCollection[i].ID != blockedInputID  
            && inputBuffers[i].CurrentRow() == null)  
        {  
            currentDependencies.Add(ComponentMetaData.InputCollection[i].ID);  
        }  
    }  
  
    return currentDependencies;  
}  
```  
  
  
