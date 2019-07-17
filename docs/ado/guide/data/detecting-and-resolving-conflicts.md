---
title: Rilevamento e risoluzione dei conflitti | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- conflicts [ADO], detecting and resolving
- ADO, detecting and resolving conflicts
ms.assetid: b28fdd26-c1a4-40ce-a700-2b0c9d201514
author: MightyPen
ms.author: genemi
ms.openlocfilehash: bce9917f144e8c63160f571a986263d8d7e97b21
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67925568"
---
# <a name="detecting-and-resolving-conflicts"></a>Rilevamento e risoluzione di conflitti
Se è necessario gestire in modalità immediata del Recordset, vi è molto meno possibilità di problemi di concorrenza si verifichi. D'altra parte, se l'applicazione usa l'aggiornamento in modalità batch, potrebbe esserci un'ottima possibilità che un utente modifichi un record prima che vengano salvate le modifiche apportate da un altro utente modifica il record stesso. In tal caso, è consigliabile l'applicazione per gestire normalmente il conflitto. Potrebbe essere ogni vostro desiderio che ultima persona che ha inviato un aggiornamento nel server "wins". In alternativa, è possibile consentire all'utente più recente per decidere quali update deve avere la precedenza fornendo quest'ultimo con una scelta tra i due valori in conflitto.  
  
 In entrambi i casi, ADO fornisce le proprietà di esempio di OriginalValue e UnderlyingValue dell'oggetto campo per gestire questi tipi di conflitti. Usare queste proprietà in combinazione con il metodo Resync e la proprietà di filtro del set di record.  
  
## <a name="remarks"></a>Note  
 Quando ADO rileva un conflitto durante un aggiornamento batch, un avviso verrà aggiunto alla raccolta di errori. Pertanto, è consigliabile sempre ricercare gli errori immediatamente dopo aver chiamato il metodo BatchUpdate e se si trova, iniziare il test si presuppone che si è verificato un conflitto. Il primo passaggio consiste nell'impostare la proprietà di filtro nel Recordset uguale a adFilterConflictingRecords. Questo limita la vista sul Recordset in modo che solo i record in conflitto. Se la proprietà RecordCount è uguale a zero dopo questo passaggio, si conosce che l'errore è stato generato da un valore diverso da un conflitto.  
  
 Quando si chiama il metodo BatchUpdate, ADO e il provider generano istruzioni SQL per eseguire aggiornamenti sull'origine dati. Tenere presente che determinate origini dati presentano limitazioni in cui i tipi di colonne possono essere utilizzati in una clausola WHERE.  
  
 Successivamente, chiamare il metodo di risincronizzazione sul set di record con l'argomento AffectRecords impostato su adAffectGroup e l'argomento ResyncValues impostato su adResyncUnderlyingValues. Il metodo Resync aggiorna i dati nell'oggetto Recordset corrente dal database sottostante. Usando adAffectGroup, si garantisce che solo i record visibili con il filtro corrente l'impostazione, vale a dire, solo i record in conflitto, vengono sincronizzati con il database. Questo potrebbe rendere una differenza significativa se è necessario gestire un set di record di grandi dimensioni. Se si imposta l'argomento ResyncValues adResyncUnderlyingValues durante la chiamata di risincronizzazione, assicurarsi che la proprietà UnderlyingValue conterrà il valore (in conflitto) dal database, che la proprietà Value manterrà il valore immesso dall'utente, e che la proprietà OriginalValue conterrà il valore originale del campo (il valore che aveva prima è stato effettuato l'ultima chiamata riuscita UpdateBatch). È quindi possibile usare questi valori per risolvere il conflitto a livello di codice o richiedere all'utente di selezionare il valore che verrà utilizzato.  
  
 Questa tecnica è illustrata nell'esempio di codice seguente. L'esempio artificially crea un conflitto con un set di record separato per modificare un valore nella tabella sottostante prima che venga chiamato UpdateBatch.  
  
```  
'BeginConflicts  
    strConn = "Provider=SQLOLEDB;Initial Catalog=Northwind;" & _  
              "Data Source=MySQLServer;Integrated Security=SSPI;"  
  
    strSQL = "SELECT * FROM Shippers WHERE ShipperID = 2"  
  
    'Open Rs and change a value  
    Set objRs1 = New ADODB.Recordset  
    Set objRs2 = New ADODB.Recordset  
    objRs1.CursorLocation = adUseClient  
    objRs1.Open strSQL, strConn, adOpenStatic, adLockBatchOptimistic, adCmdText  
    objRs1("Phone") = "(111) 555-1111"  
  
    'Introduce a conflict at the db...  
    objRs2.Open strSQL, strConn, adOpenKeyset, adLockOptimistic, adCmdText  
    objRs2("Phone") = "(999) 555-9999"  
    objRs2.Update  
    objRs2.Close  
    Set objRs2 = Nothing  
  
    On Error Resume Next  
    objRs1.UpdateBatch  
  
    If objRs1.ActiveConnection.Errors.Count <> 0 Then  
        Dim intConflicts As Integer  
  
        intConflicts = 0  
  
        objRs1.Filter = adFilterConflictingRecords  
  
        intConflicts = objRs1.RecordCount  
  
        'Resync so we can see the UnderlyingValue and offer user a choice.  
        'This sample only displays all three values and resets to original.  
        objRs1.Resync adAffectGroup, adResyncUnderlyingValues  
  
        If intConflicts > 0 Then  
            strMsg = "A conflict occurred with updates for " & intConflicts & _  
                     " record(s)." & vbCrLf & "The values will be restored" & _  
                     " to their original values." & vbCrLf & vbCrLf  
  
            objRs1.MoveFirst  
            While Not objRs1.EOF  
              strMsg = strMsg & "SHIPPER = " & objRs1("CompanyName") & vbCrLf  
              strMsg = strMsg & "Value = " & objRs1("Phone").Value & vbCrLf  
              strMsg = strMsg & "UnderlyingValue = " & _  
                                 objRs1("Phone").UnderlyingValue & vbCrLf  
              strMsg = strMsg & "OriginalValue = " & _  
                                 objRs1("Phone").OriginalValue & vbCrLf  
              strMsg = strMsg & vbCrLf & "Original value has been restored."  
  
              MsgBox strMsg, vbOKOnly, _  
                    "Conflict " & objRs1.AbsolutePosition & _  
                    " of " & intConflicts  
  
              objRs1("Phone").Value = objRs1("Phone").OriginalValue  
              objRs1.MoveNext  
            Wend  
  
            objRs1.UpdateBatch adAffectGroup  
        Else  
            'Other error occurred. Minimal handling in this example.  
             strMsg = "Errors occurred during the update. " & _  
                        objRs1.ActiveConnection.Errors(0).Number & " " & _  
                        objRs1.ActiveConnection.Errors(0).Description  
        End If  
  
        On Error GoTo 0  
    End If  
  
    objRs1.MoveFirst  
    objRs1.Close  
    Set objRs1 = Nothing  
'EndConflicts  
```  
  
 È possibile usare la proprietà Status del Record corrente o di un campo specifico per determinare il tipo di un conflitto si è verificato.  
  
 Per informazioni dettagliate sulla gestione degli errori, vedere [Error Handling](../../../ado/guide/data/error-handling.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Modalità batch](../../../ado/guide/data/batch-mode.md)
