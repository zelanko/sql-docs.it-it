---
title: Metodo AppendChunk (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Parameter::AppendChunk
- Field20::AppendChunk
helpviewer_keywords:
- AppendChunk method [ADO]
ms.assetid: c648b5a8-d4f1-4d16-836e-3957feb03617
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f9d575460daf0f801f6d6dd2e80b0c67f4886dc7
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67920569"
---
# <a name="appendchunk-method-ado"></a>Metodo AppendChunk (ADO)
Accoda i dati a un [campo](../../../ado/reference/ado-api/field-object.md)di dati di testo o binario di grandi dimensioni o a un oggetto [Parameter](../../../ado/reference/ado-api/parameter-object.md) .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
object.AppendChunk Data  
```  
  
#### <a name="parameters"></a>Parametri  
 *oggetto*  
 Oggetto **campo** o **parametro** .  
  
 *Dati*  
 **Variante** che contiene i dati da accodare all'oggetto.  
  
## <a name="remarks"></a>Osservazioni  
 Usare il metodo **AppendChunk** su un oggetto **Field** o **Parameter** per inserire dati di tipo binary o character lunghi. Nelle situazioni in cui la memoria di sistema è limitata, è possibile usare il metodo **AppendChunk** per modificare i valori Long in parti piuttosto che interamente.  
  
## <a name="field"></a>Campo  
 Se il bit **adFldLong** nella proprietà [Attributes](../../../ado/reference/ado-api/attributes-property-ado.md) di un oggetto **Field** è impostato su **true**, è possibile usare il metodo **AppendChunk** per quel campo.  
  
 La prima chiamata di **AppendChunk** su un oggetto **campo** scrive i dati nel campo, sovrascrivendo eventuali dati esistenti. Le chiamate successive a **AppendChunk** vengono aggiunte ai dati esistenti. Se si aggiungono dati a un campo e si imposta o si legge il valore di un altro campo nel record corrente, ADO presuppone che sia stata completata l'aggiunta dei dati al primo campo. Se si chiama nuovamente il metodo **AppendChunk** sul primo campo, ADO interpreta la chiamata come nuova operazione **AppendChunk** e sovrascrive i dati esistenti. L'accesso ai campi di altri oggetti [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) che non sono cloni del primo oggetto **Recordset** non interferisce con le operazioni **AppendChunk** .  
  
 Se non è presente alcun record corrente quando si chiama **AppendChunk** su un oggetto **campo** , si verifica un errore.  
  
> [!NOTE]
>  Il metodo **AppendChunk** non opera su oggetti **Field** di un oggetto [record (ADO)](../../../ado/reference/ado-api/record-object-ado.md) . Non esegue alcuna operazione e produrrà un errore di run-time.  
  
## <a name="parameter"></a>Parametro  
 Se il bit **adParamLong** nella proprietà **Attributes** di un oggetto **Parameter** è impostato su **true**, è possibile usare il metodo **AppendChunk** per il parametro.  
  
 La prima chiamata di **AppendChunk** su un oggetto **Parameter** scrive i dati nel parametro, sovrascrivendo eventuali dati esistenti. Le chiamate **AppendChunk** successive su un oggetto **Parameter** aggiungono ai dati dei parametri esistenti. Una chiamata **AppendChunk** che passa un valore null Elimina tutti i dati dei parametri.  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Oggetto Field](../../../ado/reference/ado-api/field-object.md)|[Oggetto Parameter](../../../ado/reference/ado-api/parameter-object.md)|  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodi AppendChunk e GetChunk (VB)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vb.md)   
 [Esempio di metodi AppendChunk e GetChunk (VC + +)](../../../ado/reference/ado-api/appendchunk-and-getchunk-methods-example-vc.md)   
 [Proprietà Attributes (ADO)](../../../ado/reference/ado-api/attributes-property-ado.md)   
 [Metodo GetChunk (ADO)](../../../ado/reference/ado-api/getchunk-method-ado.md)
