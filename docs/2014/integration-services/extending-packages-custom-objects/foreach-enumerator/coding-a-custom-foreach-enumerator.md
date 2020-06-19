---
title: Scrittura del codice di un enumeratore Foreach personalizzato | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom foreach enumerators [Integration Services], coding
ms.assetid: 279cf6de-d06f-40e7-b8ca-569310449f36
author: janinezhang
ms.author: janinez
ms.openlocfilehash: d760636fbb80da36f7efe7c3dc6d04b1fe92cf92
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84968783"
---
# <a name="coding-a-custom-foreach-enumerator"></a>Scrittura del codice di un enumeratore Foreach personalizzato
  Dopo avere creato una classe che eredita dalla classe di base <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator> e avere applicato l'attributo <xref:Microsoft.SqlServer.Dts.Runtime.DtsForEachEnumeratorAttribute> alla classe, è necessario eseguire l'override dell'implementazione delle proprietà e dei metodi della classe di base per fornire la funzionalità personalizzata.  
  
 Per un esempio reale di enumeratore personalizzato, vedere [Sviluppo di un'interfaccia utente per un enumeratore Foreach personalizzato](developing-a-user-interface-for-a-custom-foreach-enumerator.md).  
  
## <a name="initializing-the-enumerator"></a>Inizializzazione dell'enumeratore  
 È possibile eseguire l'override del metodo <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.InitializeForEachEnumerator%2A> per memorizzare nella cache i riferimenti alle gestioni connessioni definite nel pacchetto e i riferimenti all'interfaccia degli eventi che è possibile utilizzare per generare errori, avvisi e messaggi informativi.  
  
## <a name="validating-the-enumerator"></a>Convalida dell'enumeratore  
 Eseguire l'override del metodo <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.Validate%2A> per verificare che l'enumeratore sia configurato correttamente. Se il metodo restituisce `Failure`, l'enumeratore e il pacchetto che lo contiene non verranno eseguiti. L'implementazione di questo metodo è specifica di ogni enumeratore, ma se l'enumeratore si basa su oggetti <xref:Microsoft.SqlServer.Dts.Runtime.Variable> o <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager>, è necessario aggiungere codice per verificare che questi oggetti esistano nelle raccolte fornite al metodo.  
  
 Nell'esempio di codice seguente è illustrata un'implementazione di <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.Validate%2A> che verifica una variabile specificata in una proprietà dell'enumeratore.  
  
```csharp  
private string variableNameValue;  
  
public string VariableName  
{  
    get{ return this.variableNameValue; }  
    set{ this.variableNameValue = value; }  
}  
  
public override DTSExecResult Validate(Connections connections, VariableDispenser variableDispenser, IDTSInfoEvents infoEvents, IDTSLogging log)  
{  
    if (!variableDispenser.Contains(this.variableNameValue))  
    {  
        infoEvents.FireError(0, "MyEnumerator", "The Variable " + this.variableNameValue + " does not exist in the collection.", "", 0);  
            return DTSExecResult.Failure;  
    }  
    return DTSExecResult.Success;  
}  
```  
  
```vb  
Private variableNameValue As String  
  
Public Property VariableName() As String  
    Get   
         Return Me.variableNameValue  
    End Get  
    Set (ByVal Value As String)   
         Me.variableNameValue = value  
    End Set  
End Property  
  
Public Overrides Function Validate(ByVal connections As Connections, ByVal variableDispenser As VariableDispenser, ByVal infoEvents As IDTSInfoEvents, ByVal log As IDTSLogging) As DTSExecResult  
    If Not variableDispenser.Contains(Me.variableNameValue) Then  
        infoEvents.FireError(0, "MyEnumerator", "The Variable " + Me.variableNameValue + " does not exist in the collection.", "", 0)  
            Return DTSExecResult.Failure  
    End If  
    Return DTSExecResult.Success  
End Function  
```  
  
## <a name="returning-the-collection"></a>Restituzione della raccolta  
 Durante l'esecuzione il contenitore <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop> chiama il metodo <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A> dell'enumeratore personalizzato. In questo metodo l'enumeratore crea e popola la raccolta di elementi, quindi la restituisce. <xref:Microsoft.SqlServer.Dts.Runtime.ForEachLoop> scorre quindi gli elementi della raccolta ed esegue il flusso di controllo per ognuno di essi.  
  
 Nell'esempio seguente è illustrata un'implementazione di <xref:Microsoft.SqlServer.Dts.Runtime.ForEachEnumerator.GetEnumerator%2A> che restituisce una matrice di numeri interi casuali.  
  
```csharp  
public override object GetEnumerator()  
{  
    ArrayList numbers = new ArrayList();  
  
    Random randomNumber = new Random(DateTime.Now);  
  
    for( int x=0; x < 100; x++ )  
        numbers.Add( randomNumber.Next());  
  
    return numbers;  
}  
```  
  
```vb  
Public Overrides Function GetEnumerator() As Object  
    Dim numbers As ArrayList =  New ArrayList()   
  
    Dim randomNumber As Random =  New Random(DateTime.Now)   
  
        Dim x As Integer  
        For  x = 0 To  100- 1  Step  x + 1  
        numbers.Add(randomNumber.Next())  
        Next  
  
    Return numbers  
End Function  
```  
  
![Integration Services icona (piccola)](../../media/dts-16.gif "Icona di Integration Services (piccola)")  **rimane aggiornata con Integration Services**<br /> Per i download, gli articoli, gli esempi e i video Microsoft più recenti, oltre alle soluzioni selezionate dalla community, visitare la pagina [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] sul sito MSDN:<br /><br /> [Visitare la pagina relativa a Integration Services su MSDN](https://go.microsoft.com/fwlink/?LinkId=136655)<br /><br /> Per ricevere una notifica automatica su questi aggiornamenti, sottoscrivere i feed RSS disponibili nella pagina.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di un enumeratore Foreach personalizzato](creating-a-custom-foreach-enumerator.md)   
 [Sviluppo di un'interfaccia utente per un enumeratore Foreach personalizzato](developing-a-user-interface-for-a-custom-foreach-enumerator.md)  
  
  
