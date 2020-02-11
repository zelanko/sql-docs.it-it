---
title: HelpContext, proprietà di filelima | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::GetHelpContext
- Error::GetHelpFile
- Error::get_HelpFile
- Error::get_HelpContext
- Error::HelpContext
- Error::HelpFile
helpviewer_keywords:
- HelpContext property [ADO]
- HelpFile property [ADO]
ms.assetid: 2b9ef441-993c-44d4-8f87-fac0979dac1d
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ba441a52958e423308e648f15dd36e14d6d1d895
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67918475"
---
# <a name="helpcontext-helpfile-properties"></a>Proprietà HelpContext e HelpFile
Indica il file della guida e l'argomento associato a un oggetto [Error](../../../ado/reference/ado-api/error-object.md) .  
  
## <a name="return-values"></a>Valori restituiti  
  
-   **HelpContextID** Restituisce un ID di contesto, come valore **Long** , per un argomento in un file della guida.  
  
-   **** Fileguida Restituisce un valore **stringa** che restituisce un percorso completamente risolto a un file della guida.  
  
## <a name="remarks"></a>Osservazioni  
 Se nella proprietà FileGuida viene specificato un **file della Guida** , la proprietà **HelpContext** viene utilizzata per visualizzare automaticamente l'argomento della Guida identificato. Se non è disponibile alcun argomento della Guida pertinente, la proprietà **HelpContext** restituisce zero **e la proprietà** fileguida restituisce una stringa di lunghezza zero ("").  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Error](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Description, HelpContext, filelima, NativeError, Number, source e SQLState (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Esempio di proprietà Description, HelpContext, filelima, NativeError, Number, source e SQLState (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description (proprietà)](../../../ado/reference/ado-api/description-property.md)   
 [Proprietà Number (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Proprietà Source (Error - ADO)](../../../ado/reference/ado-api/source-property-ado-error.md)
