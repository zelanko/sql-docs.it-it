---
title: Metodo AddNew (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::AddNew
- Recordset15::raw_AddNew
helpviewer_keywords:
- AddNew method [ADO]
ms.assetid: a9f54be9-5763-45d0-a6eb-09981b03bc08
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a2f9efa8f5042fab603c794edada5aacab001936
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67921322"
---
# <a name="addnew-method-ado"></a>Metodo AddNew (ADO)
Crea un nuovo record per un oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) aggiornabile.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
recordset.AddNew FieldList, Values  
```  
  
#### <a name="parameters"></a>Parametri  
 *Recordset*  
 Oggetto **Recordset** .  
  
 *FieldList*  
 Facoltativa. Un singolo nome o una matrice di nomi o posizioni ordinali dei campi nel nuovo record.  
  
 *Valori*  
 Facoltativa. Un singolo valore o una matrice di valori per i campi nel nuovo record. Se *FieldName* è una matrice, *i valori* devono essere anche una matrice con lo stesso numero di membri. in caso contrario, si verifica un errore. L'ordine dei nomi di campo deve corrispondere all'ordine dei valori di campo in ogni matrice.  
  
## <a name="remarks"></a>Osservazioni  
 Usare il metodo **AddNew** per creare e inizializzare un nuovo record. Utilizzare il metodo [Supports](../../../ado/reference/ado-api/supports-method.md) con **adAddNew** (un valore [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md) ) per verificare se è possibile aggiungere record all'oggetto **Recordset** corrente.  
  
 Dopo aver chiamato il metodo **AddNew** , il nuovo record diventa il record corrente e rimane aggiornato dopo la chiamata al metodo [Update](../../../ado/reference/ado-api/update-method.md) . Poiché il nuovo record viene aggiunto al **Recordset**, una chiamata a **MoveNext** che segue l'aggiornamento viene spostata oltre la fine del **Recordset**, rendendo **EOF** true. Se l'oggetto **Recordset** non supporta i segnalibri, potrebbe non essere possibile accedere al nuovo record dopo lo spostamento in un altro record. A seconda del tipo di cursore, potrebbe essere necessario chiamare il metodo [Requery](../../../ado/reference/ado-api/requery-method.md) per rendere accessibile il nuovo record.  
  
 Se si chiama **AddNew** durante la modifica del record corrente o durante l'aggiunta di un nuovo record, ADO chiama il metodo **Update** per salvare le modifiche e quindi crea il nuovo record.  
  
 Il comportamento del metodo **AddNew** dipende dalla modalità di aggiornamento dell'oggetto **Recordset** e dal fatto che vengano passati gli argomenti *FieldName* e *values* .  
  
 In *modalità di aggiornamento immediato* , in cui il provider scrive le modifiche nell'origine dati sottostante una volta chiamato il metodo **Update** , la chiamata al metodo **AddNew** senza argomenti imposta la proprietà [EditMode](../../../ado/reference/ado-api/editmode-property.md) su **adEditAdd** (un valore [EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md) ). Il provider memorizza nella cache le modifiche del valore del campo in locale. Se si chiama il metodo di **aggiornamento** , il nuovo record viene inserito nel database e la proprietà **EditMode** viene reimpostata su **adEditNone** (valore **EditModeEnum** ). Se si passano gli argomenti *FieldName* e *values* , ADO inserisce immediatamente il nuovo record nel database (non è necessaria alcuna chiamata di **aggiornamento** ); il valore della proprietà **EditMode** non cambia (**adEditNone**).  
  
 In *modalità di aggiornamento batch* , in cui il provider memorizza nella cache più modifiche e le scrive nell'origine dati sottostante solo quando si chiama il metodo [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) , la chiamata al metodo **AddNew** senza argomenti imposta la proprietà **EditMode** su **adEditAdd**. Il provider memorizza nella cache le modifiche del valore del campo in locale. La chiamata al metodo **Update** aggiunge il nuovo record al **Recordset**corrente, ma il provider non pubblica le modifiche nel database sottostante o Reimposta **EditMode** su **AdEditNone**finché non viene chiamato il metodo **UpdateBatch** . Se si passano gli argomenti *FieldName* e *values* , ADO invia il nuovo record al provider per l'archiviazione in una cache e imposta **EditMode** su **adEditAdd**; è necessario chiamare il metodo **UpdateBatch** per inserire il nuovo record nel database sottostante.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come utilizzare il metodo AddNew con l'elenco dei campi e l'elenco di valori inclusi, per vedere come includere l'elenco dei campi e l'elenco di valori come matrici.  
  
```  
create table aa1 (intf int, charf char(10))  
insert into aa1 values (2, 'aa')  
  
Dim cn As New adodb.Connection  
Dim rs As New adodb.Recordset  
Dim cmd As New adodb.Command  
  
cn.ConnectionString = "Provider=SQLOLEDB;Data Source=alexverb2;uid=sa;pwd=foo$bar00;"  
  
cn.Open  
rs.Open "select * from xxx..aa1", cn, adOpenKeyset, adLockOptimistic  
  
Dim fieldsArray(1) As Variant  
fieldsArray(0) = "intf"  
fieldsArray(1) = "charf"  
Dim values(1) As Variant  
values(0) = 4  
values(1) = "as"  
rs.AddNew fieldsArray, values  
rs.Update  
```  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo AddNew (VB)](../../../ado/reference/ado-api/addnew-method-example-vb.md)   
 [Esempio di metodo AddNew (VBScript)](../../../ado/reference/ado-api/addnew-method-example-vbscript.md)   
 [Esempio di metodo AddNew (VC + +)](../../../ado/reference/ado-api/addnew-method-example-vc.md)   
 [Metodo CancelUpdate (ADO)](../../../ado/reference/ado-api/cancelupdate-method-ado.md)   
 [Proprietà EditMode](../../../ado/reference/ado-api/editmode-property.md)   
 [Metodo Requery](../../../ado/reference/ado-api/requery-method.md)   
 [Metodo Supports](../../../ado/reference/ado-api/supports-method.md)   
 [Metodo Update](../../../ado/reference/ado-api/update-method.md)   
 [Metodo UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)
