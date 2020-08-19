---
description: Proprietà Number (ADO)
title: Proprietà Number (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::Number
- Error::GetNumber
- Error::get_Number
helpviewer_keywords:
- number property [ADO]
ms.assetid: f92323c5-dd11-4a63-a505-d9014a0f067f
author: rothja
ms.author: jroth
ms.openlocfilehash: 448842387c524326e51b104a0850f9ff503d35e7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88443073"
---
# <a name="number-property-ado"></a>Proprietà Number (ADO)
Indica il numero che identifica in modo univoco un oggetto [Error](../../../ado/reference/ado-api/error-object.md) .  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un valore **Long** che può corrispondere a una delle costanti [ErrorValueEnum](../../../ado/reference/ado-api/errorvalueenum.md) .  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare la proprietà **Number** per determinare l'errore che si è verificato. Il valore della proprietà è un numero univoco che corrisponde alla condizione di errore.  
  
 La raccolta [Errors](../../../ado/reference/ado-api/errors-collection-ado.md) restituisce un valore HRESULT in formato esadecimale, ad esempio 0x80004005, o valore Long (ad esempio, 2147467259). Questi valori HRESULT possono essere generati dai componenti sottostanti, ad esempio OLE DB o persino OLE. Per ulteriori informazioni su questi numeri, vedere la pagina relativa agli [errori (OLE DB)](https://msdn.microsoft.com/ed74e62d-4948-4eeb-a7c9-fd7ad46af7fd) nella Guida [di riferimento per programmatori OLE DB](https://msdn.microsoft.com/3c5e2dd5-35e5-4a93-ac3a-3818bb43bbf8)*.*  
  
## <a name="applies-to"></a>Si applica a  
 [Error (oggetto)](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Description, HelpContext, filelima, NativeError, Number, source e SQLState (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Esempio di proprietà Description, HelpContext, filelima, NativeError, Number, source e SQLState (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description (proprietà)](../../../ado/reference/ado-api/description-property.md)   
 [HelpContext, proprietà di filelima](../../../ado/reference/ado-api/helpcontext-helpfile-properties.md)   
 [Proprietà Source (errore ADO)](../../../ado/reference/ado-api/source-property-ado-error.md)
