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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67921322"
---
# <a name="addnew-method-ado"></a>Metodo AddNew (ADO)
Crea un nuovo record per un aggiornabile [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
recordset.AddNew FieldList, Values  
```  
  
#### <a name="parameters"></a>Parametri  
 *recordset*  
 Oggetto **Recordset** oggetto.  
  
 *FieldList*  
 Facoltativo. Un singolo nome o una matrice di nomi o le posizioni ordinali dei campi nel nuovo record.  
  
 *Valori*  
 facoltativo. Un singolo valore o una matrice di valori per i campi nel nuovo record. Se *Fieldlist* è una matrice *valori* deve anche essere una matrice con lo stesso numero di membri; in caso contrario, si verifica un errore. L'ordine dei nomi di campo deve corrispondere all'ordine dei valori di campo in ogni matrice.  
  
## <a name="remarks"></a>Note  
 Usare la **AddNew** metodo per creare e inizializzare un nuovo record. Usare la [supporta](../../../ado/reference/ado-api/supports-method.md) metodo con **adAddNew** (una [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md) valore) per verificare se è possibile aggiungere record corrente **Recordset**oggetto.  
  
 Dopo aver chiamato il **AddNew** metodo, il nuovo record del record corrente e rimane tale dopo la chiamata il [Update](../../../ado/reference/ado-api/update-method.md) (metodo). Poiché viene aggiunto il nuovo record per il **Recordset**, una chiamata a **MoveNext** dopo l'aggiornamento verrà spostato oltre la fine del **Recordset**, rendendo **EOF**  True. Se il **Recordset** objekt nepodporuje segnalibri, potrebbe non essere in grado di accedere al record di nuovo dopo il passaggio a un altro record. A seconda del tipo di cursore, potrebbe essere necessario chiamare il [Requery](../../../ado/reference/ado-api/requery-method.md) metodo per rendere accessibile il nuovo record.  
  
 Se si chiama **AddNew** durante la modifica del record corrente o durante l'aggiunta di un nuovo record, chiama il metodo ADO le **Update** metodo per salvare eventuali modifiche e quindi crea il nuovo record.  
  
 Il comportamento dei **AddNew** metodo dipende dalla modalità di aggiornamento del **Recordset** oggetto e se si passa il *Fieldlist* e *valori*argomenti.  
  
 In *modalità di aggiornamento immediato* (in cui il provider scrive le modifiche all'origine dati sottostante non appena viene chiamato il **aggiornare** metodo), la chiamata di **AddNew** metodo senza set di argomenti di [EditMode](../../../ado/reference/ado-api/editmode-property.md) proprietà **adEditAdd** (un' [EditModeEnum](../../../ado/reference/ado-api/editmodeenum.md) valore). Il provider di memorizza nella cache qualsiasi valore di campo modificato in locale. Chiama il **Update** metodo invia il nuovo record nel database e reimposta il **EditMode** proprietà **adEditNone** (un **EditModeEnum**valore). Se si passa il *Fieldlist* e *valori* argomenti, ADO genera immediatamente il nuovo record nel database (nessun **Update** è necessario chiamare); il **EditMode**  non modifica il valore di proprietà (**adEditNone**).  
  
 In *modalità di aggiornamento batch* (in cui il provider vengono memorizzati nella cache più modifiche e li scrive all'origine dati sottostante solo quando si chiama il [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) metodo), la chiamata di **AddNew** metodo senza argomenti imposta le **EditMode** proprietà **adEditAdd**. Il provider di memorizza nella cache qualsiasi valore di campo modificato in locale. Chiama il **Update** metodo aggiunge il nuovo record corrente **Recordset**, ma il provider non inviare le modifiche al database sottostante o reimpostare il **EditMode** per **adEditNone**, fino a quando si chiama il **UpdateBatch** (metodo). Se si passa il *Fieldlist* e *valori* argomenti, ADO invia il nuovo record per il provider per l'archiviazione in una cache e imposta il **EditMode** a **adEditAdd** ; è necessario chiamare il **UpdateBatch** metodo per registrare il nuovo record nel database sottostante.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come usare il metodo AddNew con l'elenco dei campi e un elenco di valori incluso, per informazioni su come includere l'elenco dei campi e un elenco di valori come matrici.  
  
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
 [Requery (metodo)](../../../ado/reference/ado-api/requery-method.md)   
 [Metodo Supports](../../../ado/reference/ado-api/supports-method.md)   
 [Metodo di aggiornamento](../../../ado/reference/ado-api/update-method.md)   
 [Metodo UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md)
