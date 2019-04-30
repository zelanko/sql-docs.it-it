---
title: Accesso alle righe in un Recordset gerarchico | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- hierarchical Recordsets [ADO]
- data shaping [ADO], hierarchical Recordsets
ms.assetid: 25f1d2a1-6d5e-4457-aa07-5db5c75dee18
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 83b8334b4891d0b12cac59030ebf7fced871c5dd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63294355"
---
# <a name="accessing-rows-in-a-hierarchical-recordset-example"></a>Accesso alle righe in un Recordset gerarchico (ad esempio)
Nell'esempio seguente illustra i passaggi necessari per accedere alle righe in un modello gerarchico [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md):

1.  **Recordset** oggetti dal **autori** e **titleauthor** tabelle correlate da ID autore.

2.  Il ciclo esterno viene visualizzato il nome e cognome, stato e identificazione ogni autore.

3.  L'oggetto aggiunto **Recordset** per ogni riga viene recuperato dalle [campi](../../../ado/reference/ado-api/fields-collection-ado.md) insieme e assegnato al *rstTitleAuthor*.

4.  Il ciclo interno sono visualizzati quattro campi di ogni riga l'oggetto aggiunto **Recordset**.

 Il [StayInSync](../../../ado/reference/ado-api/stayinsync-property.md) è impostata su **false** ai fini dell'illustrazione, in modo che è possibile vedere il capitolo modificare in modo esplicito in ogni iterazione del ciclo esterno. Per rendere più efficiente l'esempio di codice, è possibile spostare l'assegnazione nel passaggio 3 prima della prima riga nel passaggio 2, in modo che l'assegnazione viene eseguita una sola volta. Impostare quindi le [StayInSync](../../../ado/reference/ado-api/stayinsync-property.md) proprietà **true**, in modo che *rstTitleAuthor* verrà modificato in modo implicito e automaticamente il capitolo corrispondente ogni volta che *rst* passa a una nuova riga.

## <a name="example"></a>Esempio

```
Sub datashape()
   Dim cnn As New ADODB.Connection
   Dim rst As New ADODB.Recordset
   Dim rstTitleAuthor As New ADODB.Recordset

   cnn.Provider = "MSDataShape"
   cnn.Open    "Data Provider=MSDASQL;" & _
               "Data Source=SRV;Integrated Security=SSPI;Database=Pubs"
' STEP 1
   rst.StayInSync = FALSE
   rst.Open    "SHAPE  {select * from authors} "  & _
               "APPEND ({select * from titleauthor} " & _
               "RELATE au_id TO au_id) AS chapTitleAuthor", _
               cnn
' STEP 2
   While Not rst.EOF
      Debug.Print    rst("au_fname"), rst("au_lname"), _
                     rst("state"), rst("au_id")
' STEP 3
      Set rstTitleAuthor = rst("chapTitleAuthor").Value
' STEP 4
      While Not rstTitleAuthor.EOF
         Debug.Print rstTitleAuthor(0), rstTitleAuthor(1), _
                     rstTitleAuthor(2), rstTitleAuthor(3)
         rstTitleAuthor.MoveNext
      Wend
      rst.MoveNext
   Wend
End Sub
```

## <a name="see-also"></a>Vedere anche
 [Panoramica del Data Shaping](../../../ado/guide/data/data-shaping-overview.md) [oggetto Field](../../../ado/reference/ado-api/field-object.md) [insieme (ADO) Fields](../../../ado/reference/ado-api/fields-collection-ado.md) [grammatica formale per Shape](../../../ado/guide/data/formal-shape-grammar.md) [Microsoft Data Shaping Service per OLE DB (Provider di servizi di ADO) ](../../../ado/guide/appendixes/microsoft-data-shaping-service-for-ole-db-ado-service-provider.md) [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md) [necessarie di provider per il Data Shaping](../../../ado/guide/data/required-providers-for-data-shaping.md) [forma clausola APPEND](../../../ado/guide/data/shape-append-clause.md) [comandi in forma Generali](../../../ado/guide/data/shape-commands-in-general.md) [clausola COMPUTE di Shape](../../../ado/guide/data/shape-compute-clause.md) [funzioni di applicazioni Visual Basic](../../../ado/guide/data/visual-basic-for-applications-functions.md)
