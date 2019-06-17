---
title: HelpContext, HelpFile proprietà | Microsoft Docs
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
manager: jroth
ms.openlocfilehash: c9c980e293b06e7fa9642ace7d425b7ffd3c0197
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66694810"
---
# <a name="helpcontext-helpfile-properties"></a>Proprietà HelpContext e HelpFile
Indica il file della Guida e l'argomento associato a un [errore](../../../ado/reference/ado-api/error-object.md) oggetto.  
  
## <a name="return-values"></a>Valori restituiti  
  
-   **ID argomento Guida** restituisce un ID di contesto, come un **lungo** valore, per un argomento in un file della Guida.  
  
-   **HelpFile** restituisce un **stringa** valore che restituisce un percorso completamente risolto in un file della Guida.  
  
## <a name="remarks"></a>Note  
 Se viene specificato un file della Guida nel **HelpFile** proprietà, il **HelpContext** proprietà viene utilizzata per visualizzare automaticamente l'argomento della Guida vengono identificati. Se nessun argomento rilevante è disponibile, il **HelpContext** proprietà restituisce zero e il **HelpFile** proprietà restituisce una stringa di lunghezza zero ("").  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Error](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Description, HelpContext, HelpFile, NativeError, numero, origine e SQLState proprietà esempio (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description, HelpContext, HelpFile, NativeError, numero, origine e SQLState esempio di proprietà (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
 [Proprietà Description](../../../ado/reference/ado-api/description-property.md)   
 [Proprietà Number (ADO)](../../../ado/reference/ado-api/number-property-ado.md)   
 [Proprietà Source (errore ADO)](../../../ado/reference/ado-api/source-property-ado-error.md)
