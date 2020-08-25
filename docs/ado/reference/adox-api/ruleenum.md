---
description: RuleEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: da49bbacf8ba59ba12f59fb072e9b5ec8c2ec2ea
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88769460"
---
# <a name="ruleenum"></a>RuleEnum
Specifica la regola da seguire quando viene eliminato un [tasto](./key-object-adox.md) .  
  
|Costante|valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adRICascade**|1|Modifiche a cascata.|  
|**adRINone**|0|Valore predefinito. Non viene eseguita alcuna azione.|  
|**adRISetDefault**|3|Il valore della chiave esterna è impostato sul valore predefinito.|  
|**adRISetNull**|2|Il valore della chiave esterna è impostato su null.|  
  
## <a name="applies-to"></a>Si applica a  
 [Proprietà DeleteRule (ADOX)](./deleterule-property-adox.md)