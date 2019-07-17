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
ms.openlocfilehash: 87c61baa93cb1dbca58bbe86ffc254a92d2b9d5b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67965242"
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
