---
title: 'Invio degli aggiornamenti: metodo UpdateBatch | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 87123797-831f-48e0-94b5-f669f9ca194a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 182e444587ce9bb3ca73166fb05dfac2506a39aa
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67924251"
---
# <a name="sending-the-updates-updatebatch-method"></a>Invio di aggiornamenti: metodo UpdateBatch
Il codice seguente apre un recordset in modalità batch impostando la proprietà LockType su adLockBatchOptimistic e CursorLocation su adUseClient. Aggiunge due nuovi record e modifica il valore di un campo in un record esistente, salvando i valori originali, quindi chiama UpdateBatch per restituire le modifiche all'origine dati.  
  
## <a name="remarks"></a>Osservazioni  
  
```  
'BeginBatchUpdate  
    strConn = "Provider=SQLOLEDB;Initial Catalog=Northwind;" & _  
              "Data Source=MySQLServer;Integrated Security=SSPI;"  
  
    strSQL = "SELECT ShipperId, CompanyName, Phone FROM Shippers"  
  
    Set objRs1 = New ADODB.Recordset  
    objRs1.CursorLocation = adUseClient  
    objRs1.Open strSQL, strConn, adOpenStatic, adLockBatchOptimistic, adCmdText  
  
    ' Change value of Phone field for first record in Recordset, saving value  
    ' for later restoration.  
    intId = objRs1("ShipperId")  
    sPhone = objRs1("Phone")  
  
    objRs1("Phone") = "(111) 555-1111"  
  
    'Add two new records  
    For i = 0 To 1  
        objRs1.AddNew  
        objRs1(1) = "New Shipper #" & CStr((i + 1))  
        objRs1(2) = "(nnn) 555-" & i & i & i & i  
    Next i  
  
    ' Send the updates  
    objRs1.UpdateBatch  
'EndBatchUpdate  
```  
  
 Se si modifica il record corrente o si aggiunge un nuovo record quando si chiama il metodo UpdateBatch, ADO chiamerà automaticamente il metodo Update per salvare le modifiche in sospeso apportate al record corrente prima di trasmettere le modifiche in batch al provider.  
  
## <a name="see-also"></a>Vedere anche  
 [Modalità batch](../../../ado/guide/data/batch-mode.md)
