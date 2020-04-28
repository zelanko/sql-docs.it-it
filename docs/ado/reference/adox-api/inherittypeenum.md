---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: aef8f768dd991e4e6ed740cc56600a6f1a8020e0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "67965957"
---
# <a name="inherittypeenum"></a>InheritTypeEnum
Specifica il modo in cui gli oggetti erediteranno le autorizzazioni impostate con [le autorizzazioni.](../../../ado/reference/adox-api/setpermissions-method-adox.md)  
  
|Costante|valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adInheritBoth**|3|Entrambi gli oggetti e altri contenitori contenuti nell'oggetto primario ereditano la voce.|  
|**adInheritContainers**|2|Gli altri contenitori contenuti nell'oggetto primario ereditano la voce.|  
|**adInheritNone**|0|Valore predefinito. Non si verifica alcuna ereditarietà.|  
|**adInheritNoPropagate**|4|I flag **adInheritObjects** e **adInheritContainers** non vengono propagati a una voce ereditata.|  
|**adInheritObjects**|1|Gli oggetti non contenitore nel contenitore ereditano le autorizzazioni.|  
  
## <a name="applies-to"></a>Si applica a  
 [Metodo SetPermissions (ADOX)](../../../ado/reference/adox-api/setpermissions-method-adox.md)
