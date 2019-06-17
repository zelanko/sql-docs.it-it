---
title: Errori ADO | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 02/15/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- errors [ADO]
ms.assetid: 9bb84114-a1df-4122-a1b8-ad98dcd85cc3
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1fe29d28d3d860b7108972abc1e1f20a10de1edc
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66701036"
---
# <a name="ado-run-time-errors"></a>Errori di Run-Time di ADO
Errori ADO vengono segnalati al programma come errori di run-time. È possibile utilizzare il meccanismo di intercettazione degli errori del linguaggio di programmazione per intercettare e gestirli. Ad esempio, in Visual Basic, usare il **in caso di errore** istruzione. In Visual C++, dipende dal metodo utilizzato per accedere alle librerie ADO. Con #import, usare una **try-catch** blocco. In caso contrario, i programmatori C++ necessari recuperare in modo esplicito un oggetto errore chiamando **GetErrorInfo**. Routine sub Visual Basic seguente viene illustrato come intercettare un errore ADO:

```
' BeginErrorHandlingVB01
Private Sub Form_Load()
' Turn on error handling
On Error GoTo FormLoadError

'Open the database and the recordset for processing.
'
Dim strCnn As String
strCnn = "Provider=sqloledb;" & _
    "Data Source=a-iresmi2000;" & _
    "Initial Catalog=Northwind;Integrated Security=SSPI"

' cnn is a Public Connection Object because
' it was defined WithEvents
Set cnn = New ADODB.Connection
cnn.Open strCnn

' The next line of code intentionally causes
' an error by trying to open a connection
' that has already been opened.
cnn.Open strCnn

' rst is a Public Recordset because it
' was defined WithEvents
Set rst = New ADODB.Recordset
rst.Open "Customers", cnn

Exit Sub

' Error handler
FormLoadError:
    Dim strErr As String
    Select Case Err
        Case adErrObjectOpen
            strErr = "Error #" & Err.Number & ": " & Err.Description & vbCrLf
            strErr = strErr & "Error reported by: " & Err.Source & vbCrLf
            strErr = strErr & "Help File: " & Err.HelpFile & vbCrLf
            strErr = strErr & "Topic ID: " & Err.HelpContext
            MsgBox strErr
            Debug.Print strErr
            Err.Clear
            Resume Next
        ' If some other error occurs that
        ' has nothing to do with ADO, show
        ' the number and description and exit.
        Case Else
            strErr = "Error #" & Err.Number & ": " & Err.Description & vbCrLf
            MsgBox strErr
            Debug.Print strErr
            Unload Me
    End Select
End Sub
' EndErrorHandlingVB01
```

 Ciò **Form_Load** routine evento crea intenzionalmente un errore quando si tenta di aprire lo stesso **connessione** oggetto due volte. La seconda volta il **aperto** viene chiamato il metodo, il gestore degli errori è attivato. In questo caso l'errore è di tipo **adErrObjectOpen**, in modo che il gestore degli errori viene visualizzato il messaggio seguente prima di riprendere l'esecuzione del programma:

```
Error #3705: Operation is not allowed when the object is open.
Error reported by: ADODB.Connection
Help File: E:\WINNT\HELP\ADO260.CHM Topic ID: 1003705
```

 Il messaggio di errore include ogni singola informazione fornita da Visual Basic **Err** dell'oggetto, ad eccezione delle **Err** valore, che non si applica qui. Il numero di errore indica si è verificato un errore. La descrizione è utile nei casi in cui non si desidera gestire personalmente l'errore. È possibile semplicemente passarlo insieme all'utente. Anche se in genere si desidera utilizzare messaggi personalizzati per l'applicazione, non è possibile prevedere ogni errore. la descrizione fornisce alcune informazioni sul mancato per quanto riguarda la causa dell'errore. Nell'esempio di codice, l'errore è stato segnalato per il **connessione** oggetto. Viene visualizzato qui - ID a livello di codice o del tipo dell'oggetto non un nome di variabile.

> [!NOTE]
>  Visual Basic **Err** oggetto contiene solo informazioni relative all'errore più recente. ADO **errori** insieme delle **connessione** oggetto contiene uno **errore** oggetto per ogni errore generato dall'operazione più recente di ADO. Usare il **errori** raccolta anziché le **Err** oggetto per gestire gli errori più. Per altre informazioni sul **errori** raccolta, vedere [errori del Provider](../../../ado/guide/data/provider-errors.md). Tuttavia, se non è non valida **connessione** oggetto, il **Err** oggetto è l'unica fonte per informazioni sugli errori ADO.

 Quali tipi di operazioni possono causare errori ADO? Errori comuni di ADO possono implicare l'apertura di un oggetto, ad esempio un **connessione** o **Recordset**, tentativo di aggiornare i dati o chiamare un metodo o proprietà che non è supportato dal provider.

 Errori OLE DB possono anche essere passati all'applicazione come errori di run-time nel **errori** raccolta.

 L'argomento seguente fornisce altre informazioni sugli errori ADO.

-   [Guida di riferimento degli errori ADO](../../../ado/guide/data/ado-error-reference.md)
