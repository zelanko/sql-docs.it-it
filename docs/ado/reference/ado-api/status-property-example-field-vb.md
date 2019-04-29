---
title: Esempio di proprietà Status (campo) (VB) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Status property [ADO Field], Visual Basic example
ms.assetid: fdd09b60-39c7-44be-8008-e891a031f80e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: caf016190e585aa64ee24f81fdcc0c18a4dab93f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63027589"
---
# <a name="status-property-example-field-vb"></a>Esempio della proprietà Status (Field) (VB)
Nell'esempio seguente viene aperto un documento da una cartella di lettura/scrittura usando il [Internet Publishing Provider](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Il [lo stato](../../../ado/reference/ado-api/status-property-ado-field.md) proprietà di un [campo](../../../ado/reference/ado-api/field-object.md) oggetto del [Record](../../../ado/reference/ado-api/record-object-ado.md) prima di tutto verrà impostato su **adFieldPendingInsert**, quindi verrà aggiornata al **adFieldOk**.  
  
```  
'BeginStatusFieldVB  
  
 ' to integrate this code replace the values in the source string  
  
Sub Main()  
  
   Dim File As ADODB.Record  
   Dim strFile As String  
   Dim Cnxn As ADODB.Connection  
   Dim strCnxn As String  
  
   Set Cnxn = New ADODB.Connection  
   strCnxn = "url=https://MyServer/"  
   Cnxn.Open strCnxn  
  
   Set File = New ADODB.Record  
   strFile = "Folder/FileName"  
   ' Open a read/write document  
   File.Source = strFile  
   File.ActiveConnection = Cnxn  
   File.Mode = adModeReadWrite  
   File.Open  
  
   Debug.Print "Append a couple of fields"  
  
   File.Fields.Append "chektest:fld1", adWChar, 42, adFldUpdatable, "fld1"  
   File.Fields.Append "chektest:fld2", adWChar, 42, adFldUpdatable, "fld2"  
  
   Debug.Print "status for the fields"  
   Debug.Print File.Fields("chektest:fld1").Status 'adfldpendinginsert  
   Debug.Print File.Fields("chektest:fld2").Status 'adfldpendinginsert  
  
    'turn off error-handling to verify field status  
   On Error Resume Next  
  
   File.Fields.Update  
  
   Debug.Print "Update succeeds"  
   Debug.Print File.Fields("chektest:fld1").Status 'adfldpendinginsert + adFieldUnavailable  
   Debug.Print File.Fields("chektest:fld2").Status 'adfldpendinginsert + adFieldUnavailable  
  
    ' resume default error-handling  
   On Error GoTo 0  
  
     ' clean up  
    File.Close  
    Cnxn.Close  
    Set File = Nothing  
    Set Cnxn = Nothing  
  
End Sub  
'EndStatusFieldVB  
```  
  
 L'esempio seguente elimina un noto **campo** da un **Record** aperto da un documento. Il **lo stato** verrà innanzitutto essere impostata su **adFieldOK**, quindi **su adFieldPendingUnknown**.  
  
```  
Attribute VB_Name = "StatusField"  
```  
  
 Il codice seguente elimina un **campo** da un **Record** aperto in un documento di sola lettura. **Lo stato** verrà impostato su **adFieldPendingDelete**. Alla [Update](../../../ado/reference/ado-api/update-method.md), l'eliminazione non riuscirà e **stato** saranno **adFieldPendingDelete** plus **adFieldPermissionDenied**. [Metodo CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) Cancella le in sospeso **stato** impostazione.  
  
```  
Attribute VB_Name = "StatusField"  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Oggetto Field](../../../ado/reference/ado-api/field-object.md)   
 [Record Object (ADO)](../../../ado/reference/ado-api/record-object-ado.md)   
 [Proprietà Status (campo ADO)](../../../ado/reference/ado-api/status-property-ado-field.md)
