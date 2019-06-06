---
title: 'Invio di aggiornamenti: Metodo UpdateBatch | Microsoft Docs'
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
manager: jroth
ms.openlocfilehash: 6759f007e652a6a52a1633b021553faa2978f6b7
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66706643"
---
# <a name="sending-the-updates-updatebatch-method"></a>Invio di aggiornamenti: Metodo UpdateBatch
Il codice seguente viene aperto un Recordset in modalità batch impostando la proprietà LockType adLockBatchOptimistic e CursorLocation a adUseClient. Aggiunge due nuovi record e modifica il valore di un campo in un record esistente, salvando i valori originali e quindi chiama il metodo UpdateBatch per restituire le modifiche all'origine dati.  
  
## <a name="remarks"></a>Note  
  
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
  
 Se si modifica il record corrente o aggiungere un nuovo record quando si chiama il metodo UpdateBatch, ADO automaticamente chiamerà il metodo di aggiornamento per salvare eventuali modifiche in sospeso al record corrente prima di trasmettere le modifiche in batch al provider.  
  
## <a name="see-also"></a>Vedere anche  
 [Modalità batch](../../../ado/guide/data/batch-mode.md)
