---
title: Codifica di tipi definiti dall'utente | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
dev_langs:
- VB
- CSharp
helpviewer_keywords:
- validation [CLR integration]
- UDTs [CLR integration], coding
- UserDefined serialization format [CLR integration]
- Point UDT
- Parse method
- null values [CLR integration]
- ToString method
- ValidatePoint method
- attributes [CLR integration]
- coding user-defined types [CLR integration]
- Read method
- Write method
- nullability [CLR integration]
- user-defined types [CLR integration], coding
- Currency UDT
- validating UDT values
- exposing UDT properties [CLR integration]
ms.assetid: 1e5b43b3-4971-45ee-a591-3f535e2ac722
author: rothja
ms.author: jroth
ms.openlocfilehash: 9a26fb1282eb9181af9b1b04f40fd7f7c45c688a
ms.sourcegitcommit: 2a06c87aa195bc6743ebdc14b91eb71ab6b91298
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/25/2019
ms.locfileid: "72907472"
---
# <a name="creating-user-defined-types---coding"></a>Creazione di tipi definiti dall'utente - Codifica
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Quando si codifica la definizione del tipo definito dall'utente (UDT), è necessario implementare varie caratteristiche a seconda che il tipo UDT venga implementato come classe o come struttura, nonché a seconda delle opzioni di formato e di serializzazione scelte.  
  
 Nell'esempio riportato in questa sezione viene illustrata l'implementazione di un tipo definito dall'utente **Point** come **struct** (o **struttura** in Visual Basic). Il tipo definito dall'utente **Point** è costituito da coordinate X e Y implementate come routine di proprietà.  
  
 Quando si definisce un tipo definito dall'utente sono richiesti gli spazi dei nomi seguenti:  
  
```vb  
Imports System  
Imports System.Data.SqlTypes  
Imports Microsoft.SqlServer.Server  
```  
  
```csharp  
using System;  
using System.Data.SqlTypes;  
using Microsoft.SqlServer.Server;  
```  
  
 Lo spazio dei nomi **Microsoft. SqlServer. Server** contiene gli oggetti necessari per diversi attributi del tipo definito dall'utente e lo spazio dei nomi **System. Data. SqlTypes** contiene le classi che rappresentano [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipi di dati nativi disponibili per l'assembly. Naturalmente, per il corretto funzionamento dell'assembly potrebbero essere necessari altri spazi dei nomi. Il tipo definito dall'utente **Point** usa anche lo spazio dei nomi **System. Text** per l'uso delle stringhe.  
  
> [!NOTE]  
>  Gli C++ oggetti Visual Database, ad esempio i tipi definiti dall'utente, compilati con **/CLR: pure** non sono supportati per l'esecuzione.  
  
## <a name="specifying-attributes"></a>Specifica degli attributi  
 Gli attributi consentono di determinare la modalità di utilizzo della serializzazione per costruire la rappresentazione di archiviazione dei tipi definiti dall'utente e per trasmettere tali tipi al client in base al valore.  
  
 **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute** è obbligatorio. L'attributo **Serializable** è facoltativo. È inoltre possibile specificare **Microsoft. SqlServer. Server. SqlFacetAttribute** per fornire informazioni sul tipo restituito di un tipo definito dall'utente. Per altre informazioni, vedere [Attributi personalizzati per routine CLR](../../relational-databases/clr-integration/database-objects/clr-integration-custom-attributes-for-clr-routines.md).  
  
### <a name="point-udt-attributes"></a>Attributi per il tipo definito dall'utente Point  
 **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute** imposta il formato di archiviazione per il tipo definito dall'utente **punto** su **nativo**. **IsByteOrdered** è impostato su **true**, che garantisce che i risultati dei confronti siano uguali in SQL Server come se lo stesso confronto fosse stato effettuato nel codice gestito. Il tipo definito dall'utente implementa l'interfaccia **System. Data. SqlTypes. INullable** per rendere la conoscenza del tipo definito dall'utente null.  
  
 Il frammento di codice seguente Mostra gli attributi per il tipo definito dall'utente **Point** .  
  
```vb  
<Serializable(), SqlUserDefinedTypeAttribute(Format.Native, _  
  IsByteOrdered:=True)> _  
  Public Structure Point  
    Implements INullable  
```  
  
```csharp  
[Serializable]  
[Microsoft.SqlServer.Server.SqlUserDefinedType(Format.Native,  
  IsByteOrdered=true)]  
public struct Point : INullable  
{  
```  
  
## <a name="implementing-nullability"></a>Implementazione del supporto dei valori Null  
 Oltre a specificare gli attributi per gli assembly in modo corretto, il tipo definito dall'utente deve supportare anche i valori Null. I tipi definiti dall'utente caricati in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono compatibili con i valori null, ma affinché il tipo definito dall'utente riconosca un valore null, il tipo definito dall'utente deve implementare l'interfaccia **System. Data. SqlTypes. INullable** .  
  
 È necessario creare una proprietà denominata **IsNull**, che è necessaria per determinare se un valore è null dall'interno del codice CLR. Quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trova un'istanza Null di un tipo definito dall'utente, tale tipo viene reso persistente utilizzando i normali metodi di gestione dei valori Null. Se non è necessario, nel server non viene eseguita la serializzazione o la deserializzazione del tipo definito dall'utente. Non viene inoltre occupato spazio per l'archiviazione di un tipo definito dall'utente Null. La verifica della presenza di valori Null viene eseguita ogni volta che un tipo definito dall'utente viene importato da CLR. Questo significa che l'utilizzo del costrutto [!INCLUDE[tsql](../../includes/tsql-md.md)] IS NULL per la verifica dei tipi definiti dall'utente Null dovrebbe funzionare sempre. La proprietà **IsNull** viene inoltre utilizzata dal server per verificare se un'istanza è null. Una volta stabilito che il tipo definito dall'utente è Null, il server è in grado di utilizzare la relativa funzionalità di gestione nativa dei valori Null.  
  
 Il metodo **Get ()** di **IsNull** non è in alcun modo speciale. Se una variabile punto **\@p** è **null**, **\@p. IsNull** restituirà, per impostazione predefinita, il valore "null" e non "1". Questo è dovuto al fatto che l'attributo **SqlMethod (OnNullCall)** del metodo **IsNull get ()** è impostato su false. Poiché l'oggetto è **null**, quando la proprietà viene richiesta, l'oggetto non viene deserializzato, il metodo non viene chiamato e viene restituito il valore predefinito "null".  
  
### <a name="example"></a>Esempio  
 Nell'esempio seguente la variabile `is_Null` è privata e mantiene lo stato Null per l'istanza del tipo definito dall'utente. Il codice deve gestire un valore appropriato per `is_Null`. Il tipo definito dall'utente deve avere anche una proprietà statica denominata **null** che restituisce un'istanza di valore null del tipo definito dall'utente. In questo modo il tipo definito dall'utente può restituire un valore Null se l'istanza è Null nel database.  
  
```vb  
Private is_Null As Boolean  
  
Public ReadOnly Property IsNull() As Boolean _  
   Implements INullable.IsNull  
    Get  
        Return (is_Null)  
    End Get  
End Property  
  
Public Shared ReadOnly Property Null() As Point  
    Get  
        Dim pt As New Point  
        pt.is_Null = True  
        Return (pt)  
    End Get  
End Property  
```  
  
```csharp  
private bool is_Null;  
  
public bool IsNull  
{  
    get  
    {  
        return (is_Null);  
    }  
}  
  
public static Point Null  
{  
    get  
    {  
        Point pt = new Point();  
        pt.is_Null = true;  
        return pt;  
    }  
}  
```  
  
### <a name="is-null-vs-isnull"></a>Confronto tra IS NULL e IsNull  
 Si consideri una tabella contenente i punti dello schema (ID int, location Point), dove **Point** è un tipo definito dall'utente CLR e le query seguenti:  
  
```  
--Query 1  
SELECT ID  
FROM Points  
WHERE NOT (location IS NULL) -- Or, WHERE location IS NOT NULL;  
```  
  
```  
--Query 2:  
SELECT ID  
FROM Points  
WHERE location.IsNull = 0;  
```  
  
 Entrambe le query restituiscono gli ID dei punti con posizioni non**null** . Nella Query 1 viene utilizzata la normale gestione dei valori Null e non è necessaria la deserializzazione dei tipi definiti dall'utente. La query 2, d'altra parte, deve deserializzare ogni oggetto non**null** e chiamare in CLR per ottenere il valore della proprietà **IsNull** . Ovviamente, l'utilizzo di **is null presenta** prestazioni migliori e non dovrebbe mai esserci un motivo per leggere la proprietà **IsNull** di un tipo definito dall'utente dal codice [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 Quindi, qual è l'uso della proprietà **IsNull** ? Per prima cosa, è necessario determinare se un valore è **null** dall'interno del codice CLR. In secondo luogo, il server necessita di un modo per verificare se un'istanza è **null**, quindi questa proprietà viene utilizzata dal server. Una volta determinato che è **null**, può utilizzare la gestione nativa dei valori null per gestirla.  
  
## <a name="implementing-the-parse-method"></a>Implementazione del metodo Parse  
 I metodi **Parse** e **ToString** consentono le conversioni da e verso le rappresentazioni di stringa del tipo definito dall'utente. Il metodo **Parse** consente la conversione di una stringa in un tipo definito dall'utente. Deve essere dichiarato come **static** (o **Shared** in Visual Basic) e accetta un parametro di tipo **System. Data. SqlTypes. SqlString**.  
  
 Il codice seguente implementa il metodo **Parse** per il tipo definito dall'utente **Point** , che separa le coordinate X e Y. Il metodo **Parse** ha un solo argomento di tipo **System. Data. SqlTypes. SqlString**e presuppone che i valori X e Y siano specificati come stringa delimitata da virgole. Se si imposta l'attributo **Microsoft. SqlServer. Server. SqlMethodAttribute. OnNullCall** su **false** , il metodo **Parse** non viene chiamato da un'istanza null di Point.  
  
```vb  
<SqlMethod(OnNullCall:=False)> _  
Public Shared Function Parse(ByVal s As SqlString) As Point  
    If s.IsNull Then  
        Return Null  
    End If  
  
    ' Parse input string here to separate out points.  
    Dim pt As New Point()  
    Dim xy() As String = s.Value.Split(",".ToCharArray())  
    pt.X = Int32.Parse(xy(0))  
    pt.Y = Int32.Parse(xy(1))  
    Return pt  
End Function  
```  
  
```csharp  
[SqlMethod(OnNullCall = false)]  
public static Point Parse(SqlString s)  
{  
    if (s.IsNull)  
        return Null;  
  
    // Parse input string to separate out points.  
    Point pt = new Point();  
    string[] xy = s.Value.Split(",".ToCharArray());  
    pt.X = Int32.Parse(xy[0]);  
    pt.Y = Int32.Parse(xy[1]);  
    return pt;  
}  
```  
  
## <a name="implementing-the-tostring-method"></a>Implementazione del metodo ToString  
 Il metodo **ToString** converte il tipo definito dall'utente **Point** in un valore stringa. In questo caso, viene restituita la stringa "NULL" per un'istanza null del tipo **Point** . Il metodo **ToString** inverte il metodo **Parse** usando un oggetto **System. Text. StringBuilder** per restituire un oggetto **System. String** delimitato da virgole costituito dai valori delle coordinate X e Y. Poiché il valore predefinito di **InvokeIfReceiverIsNull** è false, il controllo della presenza di un'istanza null di **Point** non è necessario.  
  
```vb  
Private _x As Int32  
Private _y As Int32  
  
Public Overrides Function ToString() As String  
    If Me.IsNull Then  
        Return "NULL"  
    Else  
        Dim builder As StringBuilder = New StringBuilder  
        builder.Append(_x)  
        builder.Append(",")  
        builder.Append(_y)  
        Return builder.ToString  
    End If  
End Function  
```  
  
```csharp  
private Int32 _x;  
private Int32 _y;  
  
public override string ToString()  
{  
    if (this.IsNull)  
        return "NULL";  
    else  
    {  
        StringBuilder builder = new StringBuilder();  
        builder.Append(_x);  
        builder.Append(",");  
        builder.Append(_y);  
        return builder.ToString();  
    }  
}  
```  
  
## <a name="exposing-udt-properties"></a>Esposizione delle proprietà dei tipi definiti dall'utente  
 Il tipo definito dall'utente **Point** espone le coordinate X e Y implementate come proprietà pubbliche di lettura/scrittura di tipo **System. Int32**.  
  
```vb  
Public Property X() As Int32  
    Get  
        Return (Me._x)  
    End Get  
  
    Set(ByVal Value As Int32)  
        _x = Value  
    End Set  
End Property  
  
Public Property Y() As Int32  
    Get  
        Return (Me._y)  
    End Get  
  
    Set(ByVal Value As Int32)  
        _y = Value  
    End Set  
End Property  
```  
  
```csharp  
public Int32 X  
{  
    get  
    {  
        return this._x;  
    }  
    set   
    {  
        _x = value;  
    }  
}  
  
public Int32 Y  
{  
    get  
    {  
        return this._y;  
    }  
    set  
    {  
        _y = value;  
    }  
}  
```  
  
## <a name="validating-udt-values"></a>Convalida dei valori dei tipi definiti dall'utente  
 Quando si utilizzano i dati dei tipi definiti dall'utente, il [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] converte automaticamente i valori binari in valori dei tipi definiti dall'utente. Ai fini di tale processo di conversione, viene verificato che i valori siano appropriati al formato di serializzazione del tipo e che il valore possa essere deserializzato correttamente. In questo modo si garantisce che il valore possa essere convertito di nuovo in formato binario. Nel caso dei tipi definiti dall'utente ordinati per byte, questo processo assicura anche che il valore binario risultante corrisponda al valore binario originale. In questo modo si impedisce che valori non validi vengano resi persistenti nel database. In alcuni casi, questo livello di controllo può risultare inadeguato. Una convalida aggiuntiva può essere necessaria quando è necessario che i valori dei tipi definiti dall'utente si trovino in un dominio o in un intervallo previsto. Un tipo definito dall'utente che implementa, ad esempio, una data potrebbe richiedere che il valore del giorno sia un numero positivo compreso in un determinato intervallo di valori validi.  
  
 La proprietà **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute. ValidationMethodName** di **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute** consente di specificare il nome di un metodo di convalida eseguito dal server. Quando i dati vengono assegnati a un tipo definito dall'utente o convertiti in un tipo definito dall'utente. **ValidationMethodName** viene chiamato anche durante l'esecuzione dell'utilità bcp, BULK INSERT, DBCC CHECKDB, DBCC CHECKFILEGROUP, DBCC CHECKTABLE, Distributed query e le operazioni RPC (Remote Procedure Call) TDS (Tabular Data Stream). Il valore predefinito per **ValidationMethodName** è null, a indicare che non esiste alcun metodo di convalida.  
  
### <a name="example"></a>Esempio  
 Nel frammento di codice seguente viene illustrata la dichiarazione per la classe **Point** , che specifica un **ValidationMethodName** di **ValidatePoint**.  
  
```vb  
<Serializable(), SqlUserDefinedTypeAttribute(Format.Native, _  
  IsByteOrdered:=True, _  
  ValidationMethodName:="ValidatePoint")> _  
  Public Structure Point  
```  
  
```csharp  
[Serializable]  
[Microsoft.SqlServer.Server.SqlUserDefinedType(Format.Native,  
  IsByteOrdered=true,   
  ValidationMethodName = "ValidatePoint")]  
public struct Point : INullable  
{  
```  
  
 Se si specifica un metodo di convalida, è necessario che includa una firma simile al frammento di codice seguente:  
  
```vb  
Private Function ValidationFunction() As Boolean  
    If (validation logic here) Then  
        Return True  
    Else  
        Return False  
    End If  
End Function  
```  
  
```csharp  
private bool ValidationFunction()  
{  
    if (validation logic here)  
    {  
        return true;  
    }  
    else  
    {  
        return false;  
    }  
}  
```  
  
 Il metodo di convalida può avere qualsiasi ambito e deve restituire **true** se il valore è valido e **false** in caso contrario. Se il metodo restituisce **false** o genera un'eccezione, il valore viene considerato non valido e viene generato un errore.  
  
 Nell'esempio riportato di seguito il codice accetta solo valori pari a zero o superiori per le coordinate X e Y.  
  
```vb  
Private Function ValidatePoint() As Boolean  
    If (_x >= 0) And (_y >= 0) Then  
        Return True  
    Else  
        Return False  
    End If  
End Function  
```  
  
```csharp  
private bool ValidatePoint()  
{  
    if ((_x >= 0) && (_y >= 0))  
    {  
        return true;  
    }  
    else  
    {  
        return false;  
    }  
}  
```  
  
### <a name="validation-method-limitations"></a>Limitazioni del metodo di convalida  
 Il server chiama il metodo di convalida durante l'esecuzione delle conversioni e non quando i dati vengono inseriti impostando singole proprietà o utilizzando un'istruzione INSERT [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 È necessario chiamare in modo esplicito il metodo di convalida da Setter di proprietà e il metodo **Parse** se si desidera che il metodo di convalida venga eseguito in tutte le situazioni. Questa operazione non è obbligatoria e in alcuni casi può essere anche sconsigliata.  
  
### <a name="parse-validation-example"></a>Esempio di convalida del metodo Parse  
 Per assicurarsi che il metodo **ValidatePoint** venga richiamato nella classe **Point** , è necessario chiamarlo dal metodo **Parse** e dalle routine di proprietà che impostano i valori delle coordinate X e Y. Nel frammento di codice seguente viene illustrato come chiamare il metodo di convalida **ValidatePoint** dalla funzione **Parse** .  
  
```vb  
<SqlMethod(OnNullCall:=False)> _  
Public Shared Function Parse(ByVal s As SqlString) As Point  
    If s.IsNull Then  
        Return Null  
    End If  
  
    ' Parse input string here to separate out points.  
    Dim pt As New Point()  
    Dim xy() As String = s.Value.Split(",".ToCharArray())  
    pt.X = Int32.Parse(xy(0))  
    pt.Y = Int32.Parse(xy(1))  
  
    ' Call ValidatePoint to enforce validation  
    ' for string conversions.  
    If Not pt.ValidatePoint() Then  
        Throw New ArgumentException("Invalid XY coordinate values.")  
    End If  
    Return pt  
End Function  
```  
  
```csharp  
[SqlMethod(OnNullCall = false)]  
public static Point Parse(SqlString s)  
{  
    if (s.IsNull)  
        return Null;  
  
    // Parse input string to separate out points.  
    Point pt = new Point();  
    string[] xy = s.Value.Split(",".ToCharArray());  
    pt.X = Int32.Parse(xy[0]);  
    pt.Y = Int32.Parse(xy[1]);  
  
    // Call ValidatePoint to enforce validation  
    // for string conversions.  
    if (!pt.ValidatePoint())   
        throw new ArgumentException("Invalid XY coordinate values.");  
    return pt;  
}  
```  
  
### <a name="property-validation-example"></a>Esempio di convalida delle proprietà  
 Nel frammento di codice seguente viene illustrato come chiamare il metodo di convalida **ValidatePoint** dalle routine di proprietà che impostano le coordinate X e Y.  
  
```vb  
Public Property X() As Int32  
    Get  
        Return (Me._x)  
    End Get  
  
    Set(ByVal Value As Int32)  
        Dim temp As Int32 = _x  
        _x = Value  
        If Not ValidatePoint() Then  
            _x = temp  
            Throw New ArgumentException("Invalid X coordinate value.")  
        End If  
    End Set  
End Property  
  
Public Property Y() As Int32  
    Get  
        Return (Me._y)  
    End Get  
  
    Set(ByVal Value As Int32)  
        Dim temp As Int32 = _y  
        _y = Value  
        If Not ValidatePoint() Then  
            _y = temp  
            Throw New ArgumentException("Invalid Y coordinate value.")  
        End If  
    End Set  
End Property  
```  
  
```csharp  
    public Int32 X  
{  
    get  
    {  
        return this._x;  
    }  
    // Call ValidatePoint to ensure valid range of Point values.  
    set   
    {  
        Int32 temp = _x;  
        _x = value;  
        if (!ValidatePoint())  
        {  
            _x = temp;  
            throw new ArgumentException("Invalid X coordinate value.");  
        }  
    }  
}  
  
public Int32 Y  
{  
    get  
    {  
        return this._y;  
    }  
    set  
    {  
        Int32 temp = _y;  
        _y = value;  
        if (!ValidatePoint())  
        {  
            _y = temp;  
            throw new ArgumentException("Invalid Y coordinate value.");  
        }  
    }  
}  
```  
  
## <a name="coding-udt-methods"></a>Codifica dei metodi UDT  
 Quando si codificano i metodi UDT, è consigliabile valutare la possibilità che l'algoritmo utilizzato possa cambiare nel tempo. In questo caso è possibile creare una classe separata per i metodi utilizzati dal tipo definito dall'utente. Se l'algoritmo cambia, è possibile ricompilare la classe con il nuovo codice e caricare l'assembly in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] senza influire sul tipo definito dall'utente. In molti casi i tipi definiti dall'utente possono essere ricaricati utilizzando l'istruzione ALTER ASSEMBLY [!INCLUDE[tsql](../../includes/tsql-md.md)], anche se tale operazione potrebbe provocare problemi con i dati esistenti. Ad esempio, il tipo definito dall'utente **Currency** incluso nel database di esempio **AdventureWorks** usa una funzione **ConvertCurrency** per convertire i valori di valuta, implementati in una classe separata. È possibile che gli algoritmi di conversione cambino nel tempo in modo imprevedibile o che venga richiesta una nuova funzionalità. La separazione della funzione **ConvertCurrency** dall'implementazione di tipo definito dall'utente **Currency** offre una maggiore flessibilità durante la pianificazione di modifiche future.  
  
### <a name="example"></a>Esempio  
 La classe **Point** contiene tre metodi semplici per il calcolo della distanza, ovvero **distance**, **DistanceFrom** e **DistanceFromXY**. Ogni restituisce un **valore Double** che calcola la distanza da **punto** a zero, la distanza da un punto specificato a un **punto**e la distanza tra le coordinate X e Y **specificate.** **Distance** e **DistanceFrom** ogni chiamata **DistanceFromXY**e illustrano come usare argomenti diversi per ogni metodo.  
  
```vb  
' Distance from 0 to Point.  
<SqlMethod(OnNullCall:=False)> _  
Public Function Distance() As Double  
    Return DistanceFromXY(0, 0)  
End Function  
  
' Distance from Point to the specified point.  
<SqlMethod(OnNullCall:=False)> _  
Public Function DistanceFrom(ByVal pFrom As Point) As Double  
    Return DistanceFromXY(pFrom.X, pFrom.Y)  
End Function  
  
' Distance from Point to the specified x and y values.  
<SqlMethod(OnNullCall:=False)> _  
Public Function DistanceFromXY(ByVal ix As Int32, ByVal iy As Int32) _  
    As Double  
    Return Math.Sqrt(Math.Pow(ix - _x, 2.0) + Math.Pow(iy - _y, 2.0))  
End Function  
```  
  
```csharp  
// Distance from 0 to Point.  
[SqlMethod(OnNullCall = false)]  
public Double Distance()  
{  
    return DistanceFromXY(0, 0);  
}  
  
// Distance from Point to the specified point.  
[SqlMethod(OnNullCall = false)]  
public Double DistanceFrom(Point pFrom)  
{  
    return DistanceFromXY(pFrom.X, pFrom.Y);  
}  
  
// Distance from Point to the specified x and y values.  
[SqlMethod(OnNullCall = false)]  
public Double DistanceFromXY(Int32 iX, Int32 iY)  
{  
    return Math.Sqrt(Math.Pow(iX - _x, 2.0) + Math.Pow(iY - _y, 2.0));  
}  
```  
  
### <a name="using-sqlmethod-attributes"></a>Utilizzo degli attributi SqlMethod  
 La classe **Microsoft. SqlServer. Server. SqlMethodAttribute** fornisce attributi personalizzati che possono essere utilizzati per contrassegnare le definizioni dei metodi per specificare il determinismo, il comportamento della chiamata null e per specificare se un metodo è un mutatore. Per queste proprietà si presuppone l'uso dei valori predefiniti e l'attributo personalizzato viene utilizzato solo quando è necessario un valore non predefinito.  
  
> [!NOTE]  
>  La classe **SqlMethodAttribute** eredita dalla classe **SqlFunctionAttribute** , quindi **SqlMethodAttribute** eredita i campi **FillRowMethodName** e **TableDefinition** da **SqlFunctionAttribute**. Questo implica, contrariamente al vero, la possibilità di scrivere un metodo con valori di tabella. Il metodo viene compilato e l'assembly viene distribuito, ma viene generato un errore relativo al tipo restituito **IEnumerable** in fase di esecuzione con il messaggio seguente: "metodo, proprietà o campo '\<Name >' nella classe '\<Class >' nell'assembly '\<il tipo restituito dell'assembly >' non è valido. "  
  
 Nella tabella seguente vengono descritte alcune delle proprietà **Microsoft. SqlServer. Server. SqlMethodAttribute** rilevanti che è possibile utilizzare nei metodi UDT e vengono elencati i valori predefiniti.  
  
 DataAccess  
 Indica se la funzione comporta l'accesso ai dati dell'utente archiviati nell'istanza locale di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Il valore predefinito è **DataAccessKind**. **Nessuno**.  
  
 IsDeterministic  
 Indica se la funzione produce gli stessi valori di output quando vengono specificati gli stessi valori di input e lo stesso stato del database. Il valore predefinito è **false**.  
  
 IsMutator  
 Indica se il metodo causa una modifica dello stato dell'istanza UDT. Il valore predefinito è **false**.  
  
 IsPrecise  
 Indica se la funzione comporta calcoli imprecisi, quali operazioni a virgola mobile. Il valore predefinito è **false**.  
  
 OnNullCall  
 Indica se il metodo viene chiamato quando vengono specificati argomenti di input con riferimento Null. Il valore predefinito è **true**.  
  
### <a name="example"></a>Esempio  
 La proprietà **Microsoft. SqlServer. Server. SqlMethodAttribute. Immutator** consente di contrassegnare un metodo che consente di modificare lo stato di un'istanza di un tipo definito dall'utente. [!INCLUDE[tsql](../../includes/tsql-md.md)] non consente all'utente di impostare due proprietà del tipo definito dall'utente nella clausola SET di un'istruzione UPDATE. È tuttavia possibile contrassegnare un metodo come mutatore che modifica i due membri.  
  
> [!NOTE]  
>  Nelle query non è consentito l'uso di metodi di tipo mutatore. Tali metodi possono essere chiamati solo nelle istruzioni di assegnazione o nelle istruzioni di modifica dei dati. Se un metodo contrassegnato come mutatore non restituisce **void** (o non è un **Sub** in Visual Basic), create Type ha esito negativo con un errore.  
  
 Nell'istruzione seguente si presuppone l'esistenza di un tipo definito dall'utente **triangoli** con un metodo **Rotate** . L'istruzione [!INCLUDE[tsql](../../includes/tsql-md.md)] Update seguente richiama il metodo **Rotate** :  
  
```  
UPDATE Triangles SET t.RotateY(0.6) WHERE id=5  
```  
  
 Il metodo **Rotate** viene decorato con l'impostazione dell'attributo **SqlMethod** e l'oggetto **immutator** su **true** , in modo che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possibile contrassegnare il metodo come metodo mutatore. Il codice imposta inoltre **OnNullCall** su **false**, che indica al server che il metodo restituisce un riferimento null (**Nothing** in Visual Basic) se uno dei parametri di input è un riferimento null.  
  
```vb  
<SqlMethod(IsMutator:=True, OnNullCall:=False)> _  
Public Sub Rotate(ByVal anglex as Double, _  
  ByVal angley as Double, ByVal anglez As Double)   
   RotateX(anglex)  
   RotateY(angley)  
   RotateZ(anglez)  
End Sub  
```  
  
```csharp  
[SqlMethod(IsMutator = true, OnNullCall = false)]  
public void Rotate(double anglex, double angley, double anglez)   
{  
   RotateX(anglex);  
   RotateY(angley);  
   RotateZ(anglez);  
}  
```  
  
## <a name="implementing-a-udt-with-a-user-defined-format"></a>Implementazione di un tipo definito dall'utente con un formato definito dall'utente  
 Quando si implementa un tipo definito dall'utente con un formato definito dall'utente, è necessario implementare i metodi di **lettura** e **scrittura** che implementano l'interfaccia Microsoft. SqlServer. Server. IBinarySerialize per gestire la serializzazione e la deserializzazione dei dati UDT. È inoltre necessario specificare la proprietà **MaxByteSize** di **Microsoft. SqlServer. Server. SqlUserDefinedTypeAttribute**.  
  
### <a name="the-currency-udt"></a>Tipo definito dall'utente Currency  
 Il tipo definito dall'utente **Currency** è incluso negli esempi CLR che possono essere installati con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a partire da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
 Il tipo definito dall'utente **Currency** supporta la gestione di quantità di denaro nel sistema monetario di determinate impostazioni cultura. È necessario definire due campi: una **stringa** per **CultureInfo**, che specifica chi ha emesso la valuta (ad esempio, en-US) e un **numero decimale** per **CurrencyValue**, la quantità di denaro.  
  
 Sebbene non venga utilizzato dal server per l'esecuzione di confronti, il tipo definito dall'utente **Currency** implementa l'interfaccia **System. IComparable** , che espone un singolo metodo, **System. IComparable. CompareTo**. Tale metodo viene utilizzato sul lato client nelle situazioni in cui è consigliabile confrontare o ordinare i valori relativi alla valuta in modo accurato all'interno delle diverse impostazioni cultura.  
  
 Il codice eseguito in CLR confronta le impostazioni cultura separatamente dal valore della valuta. Per il codice [!INCLUDE[tsql](../../includes/tsql-md.md)], il confronto viene determinato dalle azioni seguenti:  
  
1.  Impostare l'attributo **IsByteOrdered** su true, che indica [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di utilizzare la rappresentazione binaria permanente sul disco per i confronti.  
  
2.  Utilizzare il metodo **Write** per il tipo definito dall'utente **Currency** per determinare il modo in cui il tipo definito dall'utente viene reso permanente sul disco e pertanto il modo in cui i valori UDT vengono confrontati e ordinati per [!INCLUDE[tsql](../../includes/tsql-md.md)]  
  
3.  Salvare il tipo definito dall'utente **Currency** usando il formato binario seguente:  

    1.  Salvare le impostazioni cultura come stringa codificata UTF-16 per i byte 0-19 con riempimento a destra con caratteri Null.  
  
    2.  Utilizzare i byte 20 e successivi per contenere il valore decimale della valuta.  
  
 Lo scopo del riempimento è assicurare che le impostazioni cultura vengano separate completamente dal valore di valuta, in modo che quando un tipo definito dall'utente viene confrontato con un altro tipo nel codice [!INCLUDE[tsql](../../includes/tsql-md.md)], i byte delle impostazioni cultura vengono confrontati con i byte delle impostazioni cultura e i valori dei byte della valuta vengono confrontati con i valori dei byte della valuta.  
  
 Per il listato di codice completo per il tipo definito dall'utente **Currency** , seguire le istruzioni per l'installazione degli esempi CLR in [SQL Server motore di database esempi](https://msftengprodsamples.codeplex.com/).  
  
### <a name="currency-attributes"></a>Attributi di Currency  
 Il tipo definito dall'utente **Currency** viene definito con gli attributi seguenti.  
  
```vb  
<Serializable(), Microsoft.SqlServer.Server.SqlUserDefinedType( _  
    Microsoft.SqlServer.Server.Format.UserDefined, _  
    IsByteOrdered:=True, MaxByteSize:=32), _  
    CLSCompliant(False)> _  
Public Structure Currency  
Implements INullable, IComparable, _  
Microsoft.SqlServer.Server.IBinarySerialize  
```  
  
```csharp  
[Serializable]  
[SqlUserDefinedType(Format.UserDefined,   
    IsByteOrdered = true, MaxByteSize = 32)]  
    [CLSCompliant(false)]  
    public struct Currency : INullable, IComparable, IBinarySerialize  
    {  
```  
  
## <a name="creating-read-and-write-methods-with-ibinaryserialize"></a>Creazione di metodi di lettura e scrittura con IBinarySerialize  
 Quando si sceglie il formato di serializzazione **UserDefined** , è necessario implementare anche l'interfaccia **IBinarySerialize** e creare i propri metodi di **lettura** e **scrittura** . Le procedure seguenti del tipo definito dall'utente **Currency** utilizzano **System. io. BinaryReader** e **System. io. BinaryWriter** per leggere e scrivere nel tipo definito dall'utente.  
  
```vb  
' IBinarySerialize methods  
' The binary layout is as follow:  
'    Bytes 0 - 19: Culture name, padded to the right with null  
'    characters, UTF-16 encoded  
'    Bytes 20+: Decimal value of money  
' If the culture name is empty, the currency is null.  
Public Sub Write(ByVal w As System.IO.BinaryWriter) _  
  Implements Microsoft.SqlServer.Server.IBinarySerialize.Write  
    If Me.IsNull Then  
        w.Write(nullMarker)  
        w.Write(System.Convert.ToDecimal(0))  
        Return  
    End If  
  
    If cultureName.Length > cultureNameMaxSize Then  
        Throw New ApplicationException(String.Format(CultureInfo.CurrentUICulture, _  
           "{0} is an invalid culture name for currency as it is too long.", cultureNameMaxSize))  
    End If  
  
    Dim paddedName As String = cultureName.PadRight(cultureNameMaxSize, CChar(vbNullChar))  
  
    For i As Integer = 0 To cultureNameMaxSize - 1  
        w.Write(paddedName(i))  
    Next i  
  
    ' Normalize decimal value to two places  
    currencyVal = Decimal.Floor(currencyVal * 100) / 100  
    w.Write(currencyVal)  
End Sub  
  
Public Sub Read(ByVal r As System.IO.BinaryReader) _  
  Implements Microsoft.SqlServer.Server.IBinarySerialize.Read  
    Dim name As Char() = r.ReadChars(cultureNameMaxSize)  
    Dim stringEnd As Integer = Array.IndexOf(name, CChar(vbNullChar))  
  
    If stringEnd = 0 Then  
        cultureName = Nothing  
        Return  
    End If  
  
    cultureName = New String(name, 0, stringEnd)  
    currencyVal = r.ReadDecimal()  
End Sub  
  
```  
  
```csharp  
// IBinarySerialize methods  
// The binary layout is as follow:  
//    Bytes 0 - 19:Culture name, padded to the right   
//    with null characters, UTF-16 encoded  
//    Bytes 20+:Decimal value of money  
// If the culture name is empty, the currency is null.  
public void Write(System.IO.BinaryWriter w)  
{  
    if (this.IsNull)  
    {  
        w.Write(nullMarker);  
        w.Write((decimal)0);  
        return;  
    }  
  
    if (cultureName.Length > cultureNameMaxSize)  
    {  
        throw new ApplicationException(string.Format(  
            CultureInfo.InvariantCulture,   
            "{0} is an invalid culture name for currency as it is too long.",   
            cultureNameMaxSize));  
    }  
  
    String paddedName = cultureName.PadRight(cultureNameMaxSize, '\0');  
    for (int i = 0; i < cultureNameMaxSize; i++)  
    {  
        w.Write(paddedName[i]);  
    }  
  
    // Normalize decimal value to two places  
    currencyValue = Decimal.Floor(currencyValue * 100) / 100;  
    w.Write(currencyValue);  
}  
public void Read(System.IO.BinaryReader r)  
{  
    char[] name = r.ReadChars(cultureNameMaxSize);  
    int stringEnd = Array.IndexOf(name, '\0');  
  
    if (stringEnd == 0)  
    {  
        cultureName = null;  
        return;  
    }  
  
    cultureName = new String(name, 0, stringEnd);  
    currencyValue = r.ReadDecimal();  
}  
```  
  
 Per il listato di codice completo per il tipo definito dall'utente **Currency** , vedere [SQL Server motore di database Samples](https://msftengprodsamples.codeplex.com/).  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di un tipo definito dall'utente](../../relational-databases/clr-integration-database-objects-user-defined-types/creating-user-defined-types.md)  
  
  
