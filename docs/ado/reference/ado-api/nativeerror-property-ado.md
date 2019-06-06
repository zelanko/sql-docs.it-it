---
title: Proprietà NativeError (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Error::GetNativeError
- Error::get_NativeError
- Error::NativeError
helpviewer_keywords:
- NativeError property [ADO]
ms.assetid: b9b47e57-18a4-4186-aef5-5bd18d7b1d74
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 17f279af526a9e1f5b2c8deff4b4092e7949c5ea
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/05/2019
ms.locfileid: "66707268"
---
# <a name="nativeerror-property-ado"></a>Proprietà NativeError (ADO)
Indica il codice di errore specifico del provider per un determinato [errore](../../../ado/reference/ado-api/error-object.md) oggetto.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce un **lungo** valore che indica il codice di errore.  
  
## <a name="remarks"></a>Note  
 Usare la **NativeError** proprietà di cui recuperare le informazioni di errore specifiche del database per un particolare **errore** oggetto. Ad esempio, quando si usa il Provider ODBC di Microsoft per OLE DB con un database Microsoft SQL Server, i codici di errore nativi che hanno origine da SQL Server passano tramite ODBC e il Provider ODBC per l'oggetto ADO **NativeError** proprietà.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Error](../../../ado/reference/ado-api/error-object.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Description, HelpContext, HelpFile, NativeError, numero, origine e SQLState proprietà esempio (VB)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vb.md)   
 [Description, HelpContext, HelpFile, NativeError, numero, origine e SQLState esempio di proprietà (VC + +)](../../../ado/reference/ado-api/description-helpcontext-helpfile-nativeerror-number-source-example-vc.md)   
