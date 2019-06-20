---
title: RuleEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RuleEnum
helpviewer_keywords:
- RuleEnum enumeration [ADOX]
ms.assetid: 738fd3ff-3daf-483d-a0b9-88bef1be54c1
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 77d488bd128f4f5cfa905586f2130cd90be6354c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "66705835"
---
# <a name="ruleenum"></a>RuleEnum
Specifica la regola per seguire quando un [chiave](../../../ado/reference/adox-api/key-object-adox.md) viene eliminato.  
  
|Costante|Value|Descrizione|  
|--------------|-----------|-----------------|  
|**adRICascade**|1|Consente di propagare le modifiche.|  
|**adRINone**|0|Valore predefinito. Non viene eseguita alcuna azione.|  
|**adRISetDefault**|3|Valore di chiave esterna è impostata sul valore predefinito.|  
|**adRISetNull**|2|Valore di chiave esterna è impostato su null.|  
  
## <a name="applies-to"></a>Si applica a  
 [Proprietà DeleteRule (ADOX)](../../../ado/reference/adox-api/deleterule-property-adox.md)
