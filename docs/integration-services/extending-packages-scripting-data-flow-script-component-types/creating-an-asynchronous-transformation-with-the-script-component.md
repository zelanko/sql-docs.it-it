---
description: Creazione di una trasformazione asincrona con il componente script
title: Creazione di una trasformazione asincrona con il componente script | Microsoft Docs
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
- asynchronous outputs [Integration Services]
- transformation components [Integration Services]
- Script component [Integration Services], transformation components
ms.assetid: 0d814404-21e4-4a68-894c-96fa47ab25ae
author: chugugrace
ms.author: chugu
ms.openlocfilehash: d271139edbde0f1c67467b6fe880f916fb6c5142
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/19/2020
ms.locfileid: "92193112"
---
# <a name="creating-an-asynchronous-transformation-with-the-script-component"></a>Creazione di una trasformazione asincrona con il componente script

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Utilizzare un componente di trasformazione nel flusso di dati di un pacchetto di [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] per modificare e analizzare i dati quando vengono passati dall'origine alla destinazione. Una trasformazione con output sincroni elabora ogni riga di input non appena viene passata attraverso il componente. Una trasformazione con output asincroni potrebbe invece attendere di ricevere tutte le righe di input prima di completare l'elaborazione oppure inviare determinate righe all'output prima di aver ricevuto tutte le righe di input. In questo argomento viene descritta una trasformazione asincrona. Se l'elaborazione richiede una trasformazione sincrona, vedere [Creazione di una trasformazione sincrona con il componente script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md). Per altre informazioni sulle differenze tra componenti sincroni e asincroni, vedere [Informazioni sulle trasformazioni sincrone e asincrone](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md).  
  
 Per una panoramica sulla programmazione del componente Script, vedere [Estensione del flusso di dati con il componente script](../../integration-services/extending-packages-scripting/data-flow-script-component/extending-the-data-flow-with-the-script-component.md).  
  
 Il componente script e il codice dell'infrastruttura che genera semplificano il processo di sviluppo di un componente del flusso di dati personalizzato. Per comprendere il funzionamento del componente script, può tuttavia risultare utile leggere informazioni sui passaggi necessari per lo sviluppo di un componente del flusso di dati personalizzato nella sezione [Sviluppo di un componente del flusso di dati personalizzato](../../integration-services/extending-packages-custom-objects/data-flow/developing-a-custom-data-flow-component.md) e in particolare in [Sviluppo di un componente di destinazione personalizzato con output sincroni](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-synchronous-outputs.md).  
  
## <a name="getting-started-with-an-asynchronous-transformation-component"></a>Introduzione ai componenti di trasformazione asincroni  
 Quando si aggiunge un componente script alla scheda Flusso di dati di Progettazione [!INCLUDE[ssIS](../../includes/ssis-md.md)] viene visualizzata la finestra di dialogo **Seleziona tipo componente script** che richiede di preconfigurare il componente come origine, trasformazione o destinazione. In questa finestra di dialogo selezionare **Trasformazione**.  
  
## <a name="configuring-an-asynchronous-transformation-component-in-metadata-design-mode"></a>Configurazione di un componente di trasformazione asincrono in modalità di progettazione metadati  
 Dopo aver selezionato l'opzione per creare un componente di trasformazione, configurare il componente mediante **Editor trasformazione Script**. Per altre informazioni, vedere [Configurazione del componente script nell'editor corrispondente](../../integration-services/extending-packages-scripting/data-flow-script-component/configuring-the-script-component-in-the-script-component-editor.md).  
  
 Per selezionare il linguaggio di scripting che verrà usato dal componente script impostare la proprietà **ScriptLanguage** nella pagina **Script** della finestra di dialogo **Editor trasformazione Script**.  
  
> [!NOTE]  
>  Per impostare il linguaggio di scripting predefinito per il componente script, usare l'opzione **Linguaggio di scripting** nella pagina **Generale** della finestra di dialogo **Opzioni**. Per ulteriori informazioni, vedere [General Page](../general-page-of-integration-services-designers-options.md).  
  
 Un componente di trasformazione del flusso di dati include un input e supporta uno o più output. La configurazione dell'input e degli output del componente è uno dei passaggi da completare in modalità di progettazione metadati tramite **Editor trasformazione Script** prima di creare lo script personalizzato.  
  
### <a name="configuring-input-columns"></a>Configurazione delle colonne di input  
 Un componente di trasformazione creato tramite il componente script include un unico input.  
  
 Nella pagina **Colonne di input** di **Editor trasformazione Script** l'elenco di colonne contiene le colonne disponibili dell'output del componente a monte nel flusso di dati. Selezionare le colonne che si desidera trasformare o passare. Contrassegnare le colonne che si desidera trasformare sul posto come di lettura/scrittura.  
  
 Per altre informazioni sulla pagina **Colonne di input** di **Editor trasformazione Script**, vedere [Editor trasformazione Script &#40;pagina Colonne di input&#41;](../data-flow/transformations/script-component.md).  
  
### <a name="configuring-inputs-outputs-and-output-columns"></a>Configurazione di input, output e colonne di output  
 Un componente di trasformazione supporta uno o più output.  
  
 In genere una trasformazione con output asincroni include due output. Ad esempio, per il conteggio del numero di indirizzi di una specifica città, è possibile passare i dati degli indirizzi a un output, inviando il risultato dell'aggregazione a un altro output. L'output di aggregazione richiede anche una nuova colonna di output.  
  
 Nella pagina **Input e output** di **Editor trasformazione Script** è possibile verificare che è stato creato un singolo output per impostazione predefinita, ma non sono state create colonne di output. In questa pagina dell'editor è possibile configurare gli elementi seguenti:  
  
-   È possibile creare uno o più output aggiuntivi, ad esempio un output per il risultato di un'aggregazione. Usare i pulsanti **Aggiungi output** e **Rimuovi output** per gestire gli output del componente di trasformazione asincrono. Impostare la proprietà **SynchronousInputID** di ogni output su zero per indicare che l'output non si limita a passare i dati da un componente a monte o a trasformarli sul posto nelle righe e nelle colonne esistenti. Questa impostazione rende gli output asincroni rispetto all'input.  
  
-   È possibile assegnare un nome descrittivo all'input e agli output. Il componente script utilizza questi nomi per generare le proprietà delle funzioni di accesso tipizzate che verranno utilizzate per fare riferimento all'input e agli output nello script.  
  
-   In genere una trasformazione asincrona aggiunge colonne al flusso di dati. Quando la proprietà **SynchronousInputID** di un output è impostata su zero, a indicare che l'output non si limita a passare i dati da un componente a monte o a trasformarli sul posto nelle righe e nelle colonne esistenti, è necessario aggiungere e configurare in modo esplicito le colonne di output nell'output. Tali colonne non devono necessariamente avere gli stessi nomi delle colonne di input a cui sono mappate.  
  
-   È possibile aggiungere più colonne per includere ulteriori informazioni. È necessario scrivere codice personalizzato per inserire dati nelle colonne aggiuntive. Per informazioni sulla riproduzione del comportamento di un output degli errori standard, vedere [Simulazione di un output degli errori per il componente script](../../integration-services/extending-packages-scripting-data-flow-script-component-examples/simulating-an-error-output-for-the-script-component.md).  
  
 Per altre informazioni sulla pagina **Input e output** di **Editor trasformazione Script**, vedere [Editor trasformazione Script &#40;pagina Input e output&#41;](../data-flow/transformations/script-component.md).  
  
### <a name="adding-variables"></a>Aggiunta di variabili  
 Se si vuole usare valori di variabili esistenti nello script, è possibile aggiungerli nei campi delle proprietà ReadOnlyVariables e ReadWriteVariables della pagina **Script** di **Editor trasformazione Script**.  
  
 Quando si aggiungono più variabili nei campi delle proprietà, separare i relativi nomi con virgole. È anche possibile selezionare più variabili facendo clic sul pulsante con i puntini di sospensione ( **...** ) accanto ai campi delle proprietà **ReadOnlyVariables** e **ReadWriteVariables** e selezionando le variabili nella finestra di dialogo **Seleziona variabili**.  
  
 Per informazioni generali sull'uso delle variabili con il componente script, vedere [Uso di variabili nel componente script](../../integration-services/extending-packages-scripting/data-flow-script-component/using-variables-in-the-script-component.md).  
  
 Per altre informazioni sulla pagina **Script** di **Editor trasformazione Script**, vedere [Editor trasformazione Script &#40;pagina Script&#41;](../data-flow/transformations/script-component.md).  
  
## <a name="scripting-an-asynchronous-transformation-component-in-code-design-mode"></a>Scripting di un componente di trasformazione asincrono in modalità di progettazione codice  
 Dopo aver configurato tutti i metadati per il componente, è possibile scrivere lo script personalizzato. Nella pagina **Script** di **Editor trasformazione Script** fare clic su **Modifica script** per aprire l'IDE di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)] Tools for Applications (VSTA), in cui è possibile aggiungere lo script personalizzato. Il linguaggio di scripting che si usa varia a seconda che sia stato selezionato [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual Basic o [!INCLUDE[msCoName](../../includes/msconame-md.md)] Visual C# come linguaggio di scripting per la proprietà **ScriptLanguage** nella pagina **Script**.  
  
 Per importanti informazioni applicabili a tutti i tipi di componenti creati tramite il componente script, vedere [Codifica e debug del componente script](../../integration-services/extending-packages-scripting/data-flow-script-component/coding-and-debugging-the-script-component.md).  
  
### <a name="understanding-the-auto-generated-code"></a>Informazioni sul codice generato automaticamente  
 Quando si apre l'IDE di VSTA dopo la creazione e la configurazione di un componente di trasformazione, la classe modificabile **ScriptMain** viene visualizzata nell'editor del codice con stub per i metodi ProcessInputRow e CreateNewOutputRows. La classe ScriptMain è quella in cui si scriverà il codice personalizzato, mentre ProcessInputRow è il metodo più importante in un componente di trasformazione. Il metodo **CreateNewOutputRows** viene in genere usato in un componente di origine, che è simile a una trasformazione asincrona in quanto entrambi i componenti devono creare le rispettive righe di output.  
  
 Se si apre la finestra **Esplora progetti** in VSTA, è possibile rilevare che il componente script ha generato anche gli elementi del progetto **BufferWrapper** e **ComponentWrapper** di sola lettura. La classe ScriptMain eredita dalla classe UserComponent nell'elemento di progetto **ComponentWrapper**.  
  
 In fase di esecuzione il motore flusso di dati chiama il metodo PrimeOutput nella classe **UserComponent**, che esegue l'override del metodo <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.PrimeOutput%2A> della classe padre <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>. Il metodo PrimeOutput chiama a sua volta il metodo CreateNewOutputRows.  
  
 In fase di esecuzione il motore flusso di dati chiama il metodo ProcessInput nella classe UserComponent, che esegue l'override del metodo <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent.ProcessInput%2A> della classe padre <xref:Microsoft.SqlServer.Dts.Pipeline.ScriptComponent>. A sua volta il metodo ProcessInput esegue il ciclo delle righe nel buffer di input e chiama il metodo ProcessInputRow una volta per ogni riga.  
  
### <a name="writing-your-custom-code"></a>Scrittura di codice personalizzato  
 Per completare la creazione di un componente di trasformazione asincrono, è necessario usare il metodo ProcessInputRow sottoposto a override per elaborare i dati in ogni riga del buffer di input. Poiché gli output non sono sincroni rispetto all'input, è necessario scrivere in modo esplicito le righe di dati negli output.  
  
 In una trasformazione asincrona è possibile usare il metodo AddRow per aggiungere righe all'output, se necessario, dall'interno dei metodi ProcessInputRow o ProcessInput. Non è necessario usare il metodo CreateNewOutputRows. Se si scrive una singola riga di risultati, ad esempio i risultati di un'aggregazione, in un determinato output, è possibile creare prima la riga di output usando il metodo CreateNewOutputRows e inserire i valori in seguito dopo l'elaborazione di tutte le righe di input. Tuttavia non è utile creare più righe nel metodo CreateNewOutputRows, perché il componente script consente di usare solo la riga corrente in un input o in un output. Il metodo CreateNewOutputRows è più importante in un componente di origine, in cui non sono presenti righe di input da elaborare.  
  
 È anche possibile eseguire l'override del metodo ProcessInput stesso, in modo da poter eseguire un'elaborazione aggiuntiva preliminare o finale prima o dopo aver eseguito il ciclo del buffer di input e aver chiamato ProcessInputRow per ogni riga. Uno degli esempi di codice di questo argomento esegue l'override di ProcessInput per contare il numero di indirizzi in una città specifica mentre ProcessInputRow esegue un ciclo sulle righe **.** L'esempio scrive il valore di riepilogo nel secondo output dopo l'elaborazione di tutte le righe. L'output dell'esempio viene completato in ProcessInput, perché quando viene chiamato PostExecute non sono più disponibili buffer di output.  
  
 A seconda delle esigenze è anche possibile creare script nei metodi PreExecute e PostExecute, disponibili nella classe ScriptMain, per eseguire l'elaborazione preliminare o finale.  
  
> [!NOTE]  
>  Se si sviluppa un componente del flusso di dati personalizzato da zero, è importante eseguire l'override del metodo PrimeOutput per memorizzare nella cache i riferimenti ai buffer di output, in modo da poter aggiungere righe di dati ai buffer in un secondo momento. Nel componente script questa operazione non è necessaria perché è disponibile una classe generata automaticamente che rappresenta ogni buffer di output nell'elemento di progetto **BufferWrapper**.  
  
## <a name="example"></a>Esempio  
 In questo esempio è illustrato il codice personalizzato necessario nella classe ScriptMain per creare un componente di trasformazione asincrono.  
  
> [!NOTE]  
>  Gli esempi usano la tabella **Person.Address** del database di esempio **AdventureWorks** e passano la prima e la quarta colonna, ovvero le colonne **intAddressID** e **nvarchar(30)City**, attraverso il flusso di dati. Gli stessi dati vengono utilizzati negli esempi relativi a origine, trasformazione e destinazione in questa sezione. Per ogni esempio, sono documentati ulteriori prerequisiti e presupposti.  
  
 In questo esempio viene illustrato un componente di trasformazione asincrono con due output. Questa trasformazione passa le colonne **AddressID** e **City** a un output mentre conta il numero di indirizzi di una specifica città (Redmond, Washington, U.S.A.), quindi restituisce il valore risultante a un secondo output.  
  
 Se si desidera eseguire questo codice di esempio, è necessario configurare il pacchetto e il componente come segue:  
  
1.  Aggiungere un nuovo componente script all'area di progettazione del flusso di dati e configurarlo come trasformazione.  
  
2.  Connettere l'output di un'origine o di un'altra trasformazione al nuovo componente di trasformazione nella finestra di progettazione. Questo output deve specificare dati della tabella **Person.Address** del database di esempio **AdventureWorks** che contiene almeno le colonne **AddressID** e **City**.  
  
3.  Aprire l'**Editor trasformazione Script**. Nella pagina **Colonne di input** selezionare le colonne **AddressID** e **City**.  
  
4.  Nella pagina **Input e output** aggiungere e configurare le colonne di output **AddressID** e **City** nel primo output. Aggiungere un secondo output, quindi aggiungere una colonna di output per il valore di riepilogo nel secondo output. Impostare la proprietà SynchronousInputID del primo output su 0, perché in questo esempio ogni riga di input viene copiata in modo esplicito nel primo output. La proprietà SynchronousInputID dell'output appena creato è già impostata su 0.  
  
5.  Rinominare l'input, gli output e la nuova colonna di output specificando nomi più descrittivi. Nell'esempio si usano **MyAddressInput** come nome dell'input, **MyAddressOutput** e **MySummaryOutput** per gli output e **MyRedmondCount** per la colonna di output nel secondo output.  
  
6.  Nella pagina **Script** fare clic su **Modifica script** e immettere lo script seguente. Chiudere quindi l'ambiente di sviluppo dello script e **Editor trasformazione Script**.  
  
7.  Creare e configurare un componente di destinazione per il primo output in cui sono previste le colonne **AddressID** e **City**, ad esempio una destinazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], oppure il componente di destinazione di esempio illustrato in [Creazione di una destinazione con il componente script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-destination-with-the-script-component.md). Connettere quindi il primo output della trasformazione, **MyAddressOutput**, al componente di destinazione. È possibile creare una tabella di destinazione eseguendo il comando [!INCLUDE[tsql](../../includes/tsql-md.md)] seguente nel database **AdventureWorks**:  
  
    ```sql
    CREATE TABLE [Person].[Address2]([AddressID] [int] NOT NULL,  
        [City] [nvarchar](30) NOT NULL)  
    ```  
  
8.  Creare e configurare un altro componente di destinazione per il secondo output. Connettere quindi il secondo output della trasformazione, **MySummaryOutput**, al componente di destinazione. Poiché il secondo output scrive una singola riga con un singolo valore, è possibile configurare facilmente una destinazione con una gestione connessione file flat che si connette a un nuovo file con una singola colonna. Nell'esempio questa colonna di destinazione è denominata **MyRedmondCount**.  
  
9. Eseguire l'esempio.  
  
```vb  
Public Class ScriptMain  
    Inherits UserComponent  
  
    Private myRedmondAddressCount As Integer  
  
    Public Overrides Sub CreateNewOutputRows()  
  
        MySummaryOutputBuffer.AddRow()  
  
    End Sub  
  
    Public Overrides Sub MyAddressInput_ProcessInput(ByVal Buffer As MyAddressInputBuffer)  
  
        While Buffer.NextRow()  
            MyAddressInput_ProcessInputRow(Buffer)  
        End While  
  
        If Buffer.EndOfRowset Then  
            MyAddressOutputBuffer.SetEndOfRowset()  
            MySummaryOutputBuffer.MyRedmondCount = myRedmondAddressCount  
            MySummaryOutputBuffer.SetEndOfRowset()  
        End If  
  
    End Sub  
  
    Public Overrides Sub MyAddressInput_ProcessInputRow(ByVal Row As MyAddressInputBuffer)  
  
        With MyAddressOutputBuffer  
            .AddRow()  
            .AddressID = Row.AddressID  
            .City = Row.City  
        End With  
  
        If Row.City.ToUpper = "REDMOND" Then  
            myRedmondAddressCount += 1  
        End If  
  
    End Sub  
  
End Class  
```  
  
```csharp  
public class ScriptMain:  
    UserComponent  
  
{  
    private int myRedmondAddressCount;  
  
    public override void CreateNewOutputRows()  
    {  
  
        MySummaryOutputBuffer.AddRow();  
  
    }  
  
    public override void MyAddressInput_ProcessInput(MyAddressInputBuffer Buffer)  
    {  
  
        while (Buffer.NextRow())  
        {  
            MyAddressInput_ProcessInputRow(Buffer);  
        }  
  
        if (Buffer.EndOfRowset())  
        {  
            MyAddressOutputBuffer.SetEndOfRowset();  
            MySummaryOutputBuffer.MyRedmondCount = myRedmondAddressCount;  
            MySummaryOutputBuffer.SetEndOfRowset();  
        }  
  
    }  
  
    public override void MyAddressInput_ProcessInputRow(MyAddressInputBuffer Row)  
    {  
  
        {  
            MyAddressOutputBuffer.AddRow();  
            MyAddressOutputBuffer.AddressID = Row.AddressID;  
            MyAddressOutputBuffer.City = Row.City;  
        }  
  
        if (Row.City.ToUpper() == "REDMOND")  
        {  
            myRedmondAddressCount += 1;  
        }  
  
    }  
  
}  
  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sulle trasformazioni sincrone e asincrone](../../integration-services/understanding-synchronous-and-asynchronous-transformations.md)   
 [Creazione di una trasformazione sincrona con il componente script](../../integration-services/extending-packages-scripting-data-flow-script-component-types/creating-a-synchronous-transformation-with-the-script-component.md)   
 [Sviluppo di un componente di trasformazione personalizzato con output asincroni](../../integration-services/extending-packages-custom-objects-data-flow-types/developing-a-custom-transformation-component-with-asynchronous-outputs.md)  
  
