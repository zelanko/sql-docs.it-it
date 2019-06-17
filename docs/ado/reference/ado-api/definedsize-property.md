---
title: Proprietà DefinedSize | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::DefinedSize
helpviewer_keywords:
- DefinedSize property [ADO]
ms.assetid: 3ee27314-a305-4fbc-8433-9ee9a909afd6
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: b80838ce47bdb74878efb2918fd79b057abce216
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66718478"
---
# <a name="definedsize-property"></a>Proprietà DefinedSize
Indica la capacità dei dati di un [campo](../../../ado/reference/ado-api/field-object.md) oggetto.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un **lungo** valore che corrisponde alle dimensioni definite per un campo, che dipende dal tipo dell'oggetto campo dati, vedere [tipo](../../../ado/reference/ado-api/type-property-ado.md) per altre informazioni. Per un campo che utilizza un tipo di dati a lunghezza fissa, il valore restituito è la dimensione del tipo di dati in byte. Per un campo che utilizza un tipo di dati a lunghezza variabile, questa è una delle operazioni seguenti:  
  
1.  La lunghezza massima del campo nei caratteri (per **adVarChar** e **adVarWChar**) o in byte (per **adVarBinary**, e **adVarNumeric**) se il campo ha una lunghezza definita. Ad esempio, **adVarChar(5)** campo ha una lunghezza massima pari a 5.  
  
2.  La lunghezza massima del tipo di dati in caratteri (per **famiglia** e **adWChar**) o in byte (per **adBinary** e **adNumeric**) se la campo non è una lunghezza definita.  
  
3.  ~ 0 (OR bit per bit, il valore non è 0; tutti i bit sono impostati su 1) se il campo né il tipo di dati ha una lunghezza massima definita.  
  
4.  Per i tipi di dati che non hanno una lunghezza, è impostato su ~ 0 (OR bit per bit, il valore non è 0; tutti i bit sono impostati su 1).  
  
## <a name="remarks"></a>Note  
 Usare la **DefinedSize** proprietà per determinare la capacità di dati di un **campo** oggetto.  
  
 Il **DefinedSize** e [ActualSize](../../../ado/reference/ado-api/actualsize-property-ado.md) le proprietà sono diverse. Si consideri, ad esempio, un **campo** oggetto con un tipo dichiarato del **adVarChar** e un **DefinedSize** valore della proprietà di 50, che contiene un singolo carattere. Il **ActualSize** valore restituito della proprietà è la lunghezza in byte del carattere singolo.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di ActualSize e DefinedSize (esempio di proprietà (VB)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [Esempio di ActualSize e l'esempio di proprietà DefinedSize (VC + +)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [Proprietà ActualSize (ADO)](../../../ado/reference/ado-api/actualsize-property-ado.md)
