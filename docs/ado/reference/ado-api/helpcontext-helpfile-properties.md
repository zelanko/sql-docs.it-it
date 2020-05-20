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
author: rothja
ms.author: jroth
ms.openlocfilehash: 13fb3f0b5bf55ac9acb525183eba6d8645f4de62
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82758717"
---
# <a name="helpcontext-helpfile-properties"></a>Proprietà HelpContext e HelpFile
Indica il file della guida e l'argomento associato a un oggetto [Error](../../../ado/reference/ado-api/error-object.md) .  
  
## <a name="return-values"></a>Valori restituiti  
  
-   **HelpContextID** Restituisce un ID di contesto, come valore **Long** , per un argomento in un file della guida.  
  
-   **HelpFile** Fileguida Restituisce un valore **stringa** che restituisce un percorso completamente risolto a un file della guida.  
  
## <a name="remarks"></a>Osservazioni  
 Se nella proprietà FileGuida viene specificato un **file della Guida** , la proprietà **HelpContext** viene utilizzata per visualizzare automaticamente l'argomento della Guida identificato. Se non è disponibile alcun argomento della Guida pertinente, la proprietà **HelpContext** restituisce zero **e la proprietà** fileguida restituisce una stringa di lunghezza zero ("").  
  
## <a name="applies-to"></a>Si applica a  
 [Error (oggetto)](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà Description, HelpContext, filelima, NativeError, Number, source e SQLState (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Esempio di proprietà Description, HelpContext, filelima, NativeError, Number, source e SQLState (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Description (proprietà)](../../../ado/reference/ado-api/description-property.md)   
 [Proprietà Number (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Proprietà Source (errore ADO)](../../../ado/reference/ado-api/source-property-ado-error.md)
