---
description: InheritTypeEnum
title: InheritTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: d1fed614d90bbf53fdb2198e3ddd657a1e44acd1
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88770120"
---
# <a name="inherittypeenum"></a>InheritTypeEnum
Specifica il modo in cui gli oggetti erediteranno le autorizzazioni impostate con [le autorizzazioni.](./setpermissions-method-adox.md)  
  
|Costante|valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adInheritBoth**|3|Entrambi gli oggetti e altri contenitori contenuti nell'oggetto primario ereditano la voce.|  
|**adInheritContainers**|2|Gli altri contenitori contenuti nell'oggetto primario ereditano la voce.|  
|**adInheritNone**|0|Valore predefinito. Non si verifica alcuna ereditarietà.|  
|**adInheritNoPropagate**|4|I flag **adInheritObjects** e **adInheritContainers** non vengono propagati a una voce ereditata.|  
|**adInheritObjects**|1|Gli oggetti non contenitore nel contenitore ereditano le autorizzazioni.|  
  
## <a name="applies-to"></a>Si applica a  
 [Metodo SetPermissions (ADOX)](./setpermissions-method-adox.md)