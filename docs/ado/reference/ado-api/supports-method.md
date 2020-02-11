---
title: Metodo Supports | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::raw_Supports
- Recordset15::Supports
helpviewer_keywords:
- Supports method [ADO]
ms.assetid: 298fc41c-0b55-42fc-b373-c5133b4da6a5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: cce5ab3b735d3c641da4a6234e860d0528f107c2
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67936708"
---
# <a name="supports-method"></a>Metodo Supports
Determina se un oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) specificato supporta un particolare tipo di funzionalità.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un valore **booleano** che indica se tutte le funzionalità identificate dall'argomento *CursorOptions* sono supportate dal provider.  
  
#### <a name="parameters"></a>Parametri  
 *CursorOptions*  
 Espressione **Long** costituita da uno o più valori [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md) .  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare il metodo **Supports** per determinare i tipi di funzionalità supportati da un oggetto **Recordset** . Se l'oggetto **Recordset** supporta le funzionalità le cui costanti corrispondenti si trovano in *CursorOptions*, il metodo **Supports** restituisce **true**. In caso contrario, restituisce **false**.  
  
> [!NOTE]
>  Sebbene il metodo **Supports** possa restituire **true** per una determinata funzionalità, non garantisce che il provider possa rendere la funzionalità disponibile in tutte le circostanze. Il metodo **Supports** restituisce semplicemente un valore che indica se il provider può supportare la funzionalità specificata, supponendo che vengano soddisfatte determinate condizioni. Il metodo **Supports** , ad esempio, può indicare che un oggetto **Recordset** supporta gli aggiornamenti anche se il cursore è basato su un join a più tabelle, alcune colonne di che non sono aggiornabili.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di metodo Supports (VB)](../../../ado/reference/ado-api/supports-method-example-vb.md)   
 [Esempio di metodo Supports (VC + +)](../../../ado/reference/ado-api/supports-method-example-vc.md)   
 [Proprietà CursorType (ADO)](../../../ado/reference/ado-api/cursortype-property-ado.md)
