---
description: Proprietà ActualSize (ADO)
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 53384838d53003f0c4f81ec3b629e987ce2649a8
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451633"
---
# <a name="actualsize-property-ado"></a>Proprietà ActualSize (ADO)
Indica la lunghezza effettiva del valore di un campo in byte.  
  
## <a name="settings-and-return-values"></a>Impostazioni e valori restituiti  
 Restituisce un valore **Long** .  
  
## <a name="remarks"></a>Osservazioni  
 Utilizzare la proprietà **ActualSize** per restituire la lunghezza effettiva del valore di un oggetto [campo](../../../ado/reference/ado-api/field-object.md) . Per tutti i campi, la proprietà **ActualSize** è di sola lettura. Se ADO non è in grado di determinare la lunghezza del valore dell'oggetto **campo** , la proprietà **ActualSize** restituisce **adUnknown**.  
  
 Le proprietà **ActualSize** e [DefinedSize](../../../ado/reference/ado-api/definedsize-property.md) sono diverse, come illustrato nell'esempio seguente. Un oggetto **campo** con un tipo dichiarato di **adVarChar** e una lunghezza massima di 50 caratteri restituisce un valore di proprietà **DefinedSize** pari a 50, ma il valore della proprietà **ActualSize** restituito è la lunghezza dei dati archiviati nel campo per il record corrente. I **campi** con un **DefinedSize** maggiore di 255 byte vengono trattati come colonne a lunghezza variabile.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Field](../../../ado/reference/ado-api/field-object.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà ActualSize e DefinedSize (VB)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vb.md)   
 [Esempio di proprietà ActualSize e DefinedSize (VC + +)](../../../ado/reference/ado-api/actualsize-and-definedsize-properties-example-vc.md)   
 [Proprietà DefinedSize](../../../ado/reference/ado-api/definedsize-property.md)
