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
ms.openlocfilehash: 2e8c969c8e611c8e2bff76dc045a28a9c6d6ab96
ms.sourcegitcommit: c4d564435c008e2c92035efd2658172f20f07b2b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88759941"
---
# <a name="activecommand-property-ado"></a>Proprietà ActiveCommand (ADO)
Indica l'oggetto [comando](./command-object-ado.md) che ha creato l'oggetto [Recordset](./recordset-object-ado.md) associato.  
  
## <a name="return-value"></a>Valore restituito  
 Restituisce una **variante** che contiene un oggetto **comando** . Il valore predefinito è un riferimento a un oggetto null.  
  
## <a name="remarks"></a>Commenti  
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