---
title: LockTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- LockTypeEnum
helpviewer_keywords:
- LockTypeEnum enumeration [ADO]
ms.assetid: d2894eaf-4450-4ace-aa51-c8b875fd3010
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bcd2e4d2a3b84ef913954c1a1a2d7fa76393040c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62864074"
---
# <a name="locktypeenum"></a>LockTypeEnum
Specifica il tipo di blocco inserito nei record durante la modifica.  
  
|Costante|Value|Descrizione|  
|--------------|-----------|-----------------|  
|**adLockBatchOptimistic**|4|Indica gli aggiornamenti in blocco ottimistico. Obbligatorio per la modalità di aggiornamento batch.|  
|**adLockOptimistic**|3|Indica il blocco ottimistico, dal record. Il provider utilizza il blocco ottimistico, blocco dei record solo quando si chiama il [Update](../../../ado/reference/ado-api/update-method.md) (metodo).|  
|**adLockPessimistic**|2|Indica il blocco pessimistico, un record. Il provider non sia necessaria per garantire la corretta modifica dei record, in genere dal blocco dei record nell'origine dati immediatamente dopo la modifica.|  
|**adLockReadOnly**|1|Indica i record di sola lettura. Non è possibile modificare i dati.|  
|**adLockUnspecified**|-1|Non specifica un tipo di blocco. Per la clonazione, il clone viene creato con lo stesso tipo di blocco dell'originale.|  
  
## <a name="adowfc-equivalent"></a>Equivalente di ADO o WFC  
 Package: **com.ms.wfc.data**  
  
|Costante|  
|--------------|  
|AdoEnums.LockType.BATCHOPTIMISTIC|  
|AdoEnums.LockType.OPTIMISTIC|  
|AdoEnums.LockType.PESSIMISTIC|  
|AdoEnums.LockType.READONLY|  
|AdoEnums.LockType.UNSPECIFIED|  
  
## <a name="applies-to"></a>Si applica a  
  
|||  
|-|-|  
|[Metodo Clone (ADO)](../../../ado/reference/ado-api/clone-method-ado.md)|[Proprietà LockType (ADO)](../../../ado/reference/ado-api/locktype-property-ado.md)|  
|[Metodo Open (Recordset ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|[Evento WillExecute (ADO)](../../../ado/reference/ado-api/willexecute-event-ado.md)|
