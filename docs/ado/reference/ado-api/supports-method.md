---
title: Supporta metodo | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: 1d1df1d780cf9e1e631f6b146e45cc0a34da9438
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66710687"
---
# <a name="supports-method"></a>Metodo Supports
Determina se un oggetto specificato [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) oggetto supporta un determinato tipo di funzionalità.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
boolean = recordset.Supports(CursorOptions )  
```  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un **booleana** valore che indica se tutte le funzionalità identificati dal *CursorOptions* argomento sono supportati dal provider.  
  
#### <a name="parameters"></a>Parametri  
 *CursorOptions*  
 Oggetto **lungo** espressione costituita da uno o più [CursorOptionEnum](../../../ado/reference/ado-api/cursoroptionenum.md) valori.  
  
## <a name="remarks"></a>Note  
 Usare la **supporta** metodo per determinare quali tipi di funzionalità di un **Recordset** supporta dell'oggetto. Se il **Recordset** oggetto supporta le funzionalità di cui costanti corrispondente sono *CursorOptions*, il **supporta** restituzione del metodo **True**. In caso contrario, restituisce **False**.  
  
> [!NOTE]
>  Anche se il **supporta** metodo può restituire **True** per una determinata funzionalità, ma questa soluzione non garantisce che il provider può rendere la funzionalità disponibile in tutte le circostanze. Il **supporta** metodo restituisce semplicemente se il provider supporta la funzionalità specificata, presupponendo che vengano soddisfatte determinate condizioni. Ad esempio, il **supporta** metodo potrebbe indicare che un **Recordset** oggetto supporti gli aggiornamenti anche se il cursore è basato su un join tra più tabelle, alcune colonne di cui non sono aggiornabili.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Supporta l'esempio di metodo (VB)](../../../ado/reference/ado-api/supports-method-example-vb.md)   
 [Supporta l'esempio di metodo (VC + +)](../../../ado/reference/ado-api/supports-method-example-vc.md)   
 [Proprietà CursorType (ADO)](../../../ado/reference/ado-api/cursortype-property-ado.md)
