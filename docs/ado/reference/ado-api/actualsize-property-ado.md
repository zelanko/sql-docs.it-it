---
title: Proprietà ActualSize (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 03/20/2018
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Field20::ActualSize
helpviewer_keywords:
- ActualSize property [ADO]
ms.assetid: 722803d0-cef5-4d4c-b79d-3f2f58052229
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6d405113044d10244d8c4fc3483c6220bf630dc5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67921425"
---
# <a name="actualsize-property-ado"></a>Proprietà ActualSize (ADO)
Indica la lunghezza effettiva del valore del campo espressa in byte.  
  
## <a name="settings-and-return-values"></a>Le impostazioni e valori restituiti  
 Restituisce un **lungo** valore.  
  
## <a name="remarks"></a>Note  
 Usare la **ActualSize** proprietà per restituire la lunghezza effettiva di un [campo](../../../ado/reference/ado-api/field-object.md) valore dell'oggetto. Per tutti i campi, il **ActualSize** proprietà è di sola lettura. Se ADO non è possibile determinare la lunghezza del **campo** valore dell'oggetto, il **ActualSize** restituisce proprietà **adUnknown**.  
  
 Il **ActualSize** e [DefinedSize](../../../ado/reference/ado-api/definedsize-property.md) le proprietà sono diverse, come illustrato nell'esempio seguente. Oggetto **campo** oggetto con un tipo dichiarato della **adVarChar** e una lunghezza massima di 50 caratteri restituisce un **DefinedSize** valore della proprietà di 50, ma il  **Esempio di ActualSize** valore restituito della proprietà è la lunghezza dei dati archiviati nel campo del record corrente. **I campi** con un **DefinedSize** maggiori di 255 byte vengono gestite come colonne a lunghezza variabile.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di ActualSize e DefinedSize (esempio di proprietà (VB)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [Esempio di ActualSize e l'esempio di proprietà DefinedSize (VC + +)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [Proprietà DefinedSize](../../../ado/reference/ado-api/definedsize-property.md)
