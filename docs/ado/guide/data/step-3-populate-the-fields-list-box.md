---
title: 'Passaggio 3: Popolare la casella di riepilogo Fields | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 315c32dc-aeb1-4629-b30e-87b44e8f84d1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: f69ab97a522e148d8027042ff7e2c6b09a690424
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66704822"
---
# <a name="step-3-populate-the-fields-list-box"></a>Passaggio 3: Popolare la casella di riepilogo Fields
Per popolare la casella di riepilogo di campi, inserire il codice seguente nel gestore dell'evento Click del `lstMain`:  
  
```  
Private Sub lstMain_Click()  
    Dim rec As Record  
    Dim rs As Recordset  
    Set rec = New Record  
    Set rs = New Recordset  
    grs.MoveFirst  
    grs.Move lstMain.ListIndex  
    lstDetails.Clear  
    rec.Open grs  
    Select Case rec.RecordType  
        Case adCollectionRecord:  
            Set rs = rec.GetChildren  
            While Not rs.EOF  
                lstDetails.AddItem rs(0)  
                rs.MoveNext  
            Wend  
        Case adSimpleRecord:  
            recFields rec, lstDetails, txtDetails  
  
        Case adStructDoc:  
    End Select  
  
End Sub  
```  
  
 Questo codice dichiara e crea un'istanza locali oggetti Record e Recordset `rec` e `rs`, rispettivamente.  
  
 La riga corrispondente alla risorsa selezionata nel `lstMain` viene eseguita la riga corrente di `grs`. Quindi viene deselezionata la casella di riepilogo dei dettagli e `rec` viene aperto con la riga corrente di `grs` come origine.  
  
 Se la risorsa è un record, come specificato da [RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md), il Recordset locale `rs` aperta sugli elementi figlio del record. Quindi `lstDetails` viene riempita con i valori dalle righe di `rs`.  
  
 Se la risorsa è un semplice record, `recFields` viene chiamato. Per altre informazioni sulle `recFields`, vedere il passaggio successivo.  
  
 Codice non viene implementato se la risorsa è un documento strutturato.  
  
## <a name="see-also"></a>Vedere anche  
 [Scenario di Internet Publishing](../../../ado/guide/data/internet-publishing-scenario.md)   
 [Passaggio 2: Inizializzare la casella di riepilogo principale](../../../ado/guide/data/step-2-initialize-the-main-list-box.md)   
 [Passaggio 4: Popolare la casella di testo dei dettagli](../../../ado/guide/data/step-4-populate-the-details-text-box.md)
