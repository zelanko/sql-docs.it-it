---
title: Metodo Requery | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Requery
- Recordset15::raw_Requery
helpviewer_keywords:
- Requery method [ADO]
ms.assetid: d81ab76f-1aa8-4ccf-92ec-b65254dc3ea1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c3626f91018714fa4d67304c92ce464d82fb5c8e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67917219"
---
# <a name="requery-method"></a>Metodo Requery
Aggiorna i dati in un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto eseguendo nuovamente la query in cui si basa l'oggetto.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
recordset.Requery Options  
```  
  
#### <a name="parameters"></a>Parametri  
 *Opzioni*  
 Facoltativo. Maschera di bit che contiene [ExecuteOptionEnum](../../../ado/reference/ado-api/executeoptionenum.md) e [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) valori che influenzano l'operazione.  
  
> [!NOTE]
>  Se *le opzioni* è impostata su **adAsyncExecute**, l'operazione verrà eseguita in modo asincrono e un [RecordsetChangeComplete](../../../ado/reference/ado-api/willchangerecordset-and-recordsetchangecomplete-events-ado.md) evento verrà generato quando termina. Il **ExecuteOpenEnum** i valori di **adExecuteStream** oppure **adExecuteStream** non devono essere usati con **Requery**.  
  
## <a name="remarks"></a>Note  
 Usare il **Requery** metodo per aggiornare l'intero contenuto di un **Recordset** oggetto dall'origine dati rieseguendo il comando originale e recuperando i dati una seconda volta. Chiamare questo metodo è equivalente alla chiamata di [Close](../../../ado/reference/ado-api/close-method-ado.md) e [Open](../../../ado/reference/ado-api/open-method-ado-recordset.md) metodi in successione. Se si modifica il record corrente o aggiungere un nuovo record, si verifica un errore.  
  
 Mentre il **Recordset** oggetto è aperto, le proprietà che definiscono la natura del cursore ([CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md), [LockType](../../../ado/reference/ado-api/locktype-property-ado.md), [MaxRecords](../../../ado/reference/ado-api/maxrecords-property-ado.md) e così via) sono di sola lettura. Di conseguenza, il **Requery** metodo può aggiornare solo il cursore corrente. Per modificare le proprietà del cursore e visualizzare i risultati, è necessario usare il [Chiudi](../../../ado/reference/ado-api/close-method-ado.md) metodo in modo che le proprietà di lettura/scrittura tornato. È possibile modificare le impostazioni delle proprietà e chiamare il [aperto](../../../ado/reference/ado-api/open-method-ado-recordset.md) metodo riapertura del cursore.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire, rieseguire una query ed eliminare i metodi esempio (VB)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vb.md)   
 [Eseguire, rieseguire una query ed eliminare i metodi esempio (VBScript)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vbscript.md)   
 [Eseguire, rieseguire una query ed eliminare i metodi esempio (VC + +)](../../../ado/reference/ado-api/execute-requery-and-clear-methods-example-vc.md)   
 [Proprietà CommandText (ADO)](../../../ado/reference/ado-api/commandtext-property-ado.md)
