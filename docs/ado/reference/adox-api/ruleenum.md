---
description: RuleEnum
title: RuleEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 66367d872e27629f1bf437961b99908d0c42e9f2
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88983372"
---
# <a name="ruleenum"></a>RuleEnum
Specifica la regola da seguire quando viene eliminato un [tasto](./key-object-adox.md) .  
  
|Costante|Valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adRICascade**|1|Modifiche a cascata.|  
|**adRINone**|0|Valore predefinito. Non viene eseguita alcuna azione.|  
|**adRISetDefault**|3|Il valore della chiave esterna è impostato sul valore predefinito.|  
|**adRISetNull**|2|Il valore della chiave esterna è impostato su null.|  
  
## <a name="applies-to"></a>Si applica a  
 [Proprietà DeleteRule (ADOX)](./deleterule-property-adox.md)