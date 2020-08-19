---
description: Proprietà ActiveCommand (ADO)
title: Proprietà ActiveCommand (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset20::ActiveCommand
helpviewer_keywords:
- ActiveCommand property [ADO]
ms.assetid: fb4088d5-5968-42d6-aeaa-3955046bb4da
author: rothja
ms.author: jroth
ms.openlocfilehash: 38c0a0955e934b4f303937d978f739e00ac6c120
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88451743"
---
# <a name="activecommand-property-ado"></a>Proprietà ActiveCommand (ADO)
Indica l'oggetto [comando](../../../ado/reference/ado-api/command-object-ado.md) che ha creato l'oggetto [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) associato.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce una **variante** che contiene un oggetto **comando** . Il valore predefinito è un riferimento a un oggetto null.  
  
## <a name="remarks"></a>Osservazioni  
 La proprietà **ActiveCommand** è di sola lettura.  
  
 Se non è stato utilizzato un oggetto **comando** per creare il **Recordset**corrente, viene restituito un riferimento a un oggetto **null** .  
  
 Utilizzare questa proprietà per trovare l'oggetto **comando** associato quando viene fornito solo l'oggetto **Recordset** risultante.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà ActiveCommand (VB)](../../../ado/reference/ado-api/activecommand-property-example-vb.md)   
 [Esempio di proprietà ActiveCommand (JScript)](../../../ado/reference/ado-api/activecommand-property-example-jscript.md)   
 [Esempio di proprietà ActiveCommand (VC + +)](../../../ado/reference/ado-api/activecommand-property-example-vc.md)   
 [Oggetto Command (ADO)](../../../ado/reference/ado-api/command-object-ado.md)
