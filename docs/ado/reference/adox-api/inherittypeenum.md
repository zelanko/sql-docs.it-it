---
description: InheritTypeEnum
title: InheritTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- InheritTypeEnum
helpviewer_keywords:
- InheritTypeEnum enumeration [ADOX]
ms.assetid: c2f6ce79-c4b3-4d40-ac95-21025208f991
author: rothja
ms.author: jroth
ms.openlocfilehash: 37c6eba57eb7efb05d2b718e294e33b9616cac77
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88984102"
---
# <a name="inherittypeenum"></a>InheritTypeEnum
Specifica il modo in cui gli oggetti erediteranno le autorizzazioni impostate con [le autorizzazioni.](./setpermissions-method-adox.md)  
  
|Costante|Valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adInheritBoth**|3|Entrambi gli oggetti e altri contenitori contenuti nell'oggetto primario ereditano la voce.|  
|**adInheritContainers**|2|Gli altri contenitori contenuti nell'oggetto primario ereditano la voce.|  
|**adInheritNone**|0|Valore predefinito. Non si verifica alcuna ereditarietà.|  
|**adInheritNoPropagate**|4|I flag **adInheritObjects** e **adInheritContainers** non vengono propagati a una voce ereditata.|  
|**adInheritObjects**|1|Gli oggetti non contenitore nel contenitore ereditano le autorizzazioni.|  
  
## <a name="applies-to"></a>Si applica a  
 [Metodo SetPermissions (ADOX)](./setpermissions-method-adox.md)