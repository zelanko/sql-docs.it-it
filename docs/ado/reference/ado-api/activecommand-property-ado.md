---
description: Proprietà ActiveCommand (ADO)
title: Proprietà ActiveCommand (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: df737543e8cc09735c7da413b89406b6f2385079
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88977154"
---
# <a name="activecommand-property-ado"></a>Proprietà ActiveCommand (ADO)
Indica l'oggetto [comando](./command-object-ado.md) che ha creato l'oggetto [Recordset](./recordset-object-ado.md) associato.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce una **variante** che contiene un oggetto **comando** . Il valore predefinito è un riferimento a un oggetto null.  
  
## <a name="remarks"></a>Osservazioni  
 La proprietà **ActiveCommand** è di sola lettura.  
  
 Se non è stato utilizzato un oggetto **comando** per creare il **Recordset**corrente, viene restituito un riferimento a un oggetto **null** .  
  
 Utilizzare questa proprietà per trovare l'oggetto **comando** associato quando viene fornito solo l'oggetto **Recordset** risultante.  
  
## <a name="applies-to"></a>Si applica a  
 [Oggetto Recordset (ADO)](./recordset-object-ado.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Esempio di proprietà ActiveCommand (VB)](./activecommand-property-example-vb.md)   
 [Esempio di proprietà ActiveCommand (JScript)](./activecommand-property-example-jscript.md)   
 [Esempio di proprietà ActiveCommand (VC + +)](./activecommand-property-example-vc.md)   
 [Oggetto Command (ADO)](./command-object-ado.md)