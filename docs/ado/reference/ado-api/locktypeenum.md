---
description: LockTypeEnum
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
author: rothja
ms.author: jroth
ms.openlocfilehash: 7ba912f082cbd621d2d2205c6505e8c2be309bec
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88774550"
---
# <a name="locktypeenum"></a>LockTypeEnum
Specifica il tipo di blocco inserito nei record durante la modifica.  
  
|Costante|valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adLockBatchOptimistic**|4|Indica gli aggiornamenti in batch ottimistici. Obbligatorio per la modalità di aggiornamento batch.|  
|**adLockOptimistic**|3|Indica il blocco ottimistico, record per record. Il provider utilizza il blocco ottimistico, bloccando i record solo quando si chiama il metodo [Update](./update-method.md) .|  
|**adLockPessimistic**|2|Indica il blocco pessimistico, record per record. Il provider esegue le operazioni necessarie per garantire la corretta modifica dei record, in genere bloccando i record nell'origine dati immediatamente dopo la modifica.|  
|**adLockReadOnly**|1|Indica i record di sola lettura. Non è possibile modificare i dati.|  
|**adLockUnspecified**|-1|Non specifica un tipo di blocco. Per i cloni, il clone viene creato con lo stesso tipo di blocco dell'originale.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Pacchetto: **com. ms. wfc. Data**  
  
|Costante|  
|--------------|  
|AdoEnums.LockType.BATCHOPTIMISTIC|  
|AdoEnums. LockType. OTTIMISTIca|  
|AdoEnums. LockType. PESSIMISTica|  
|AdoEnums. LockType. READONLY|  
|AdoEnums. LockType. Unspecified|  
  
## <a name="applies-to"></a>Si applica a  

:::row:::
    :::column:::
        [Metodo Clone (ADO)](./clone-method-ado.md)  
        [Proprietà LockType (ADO)](./locktype-property-ado.md)  
    :::column-end:::
    :::column:::
        [Metodo Open (Recordset - ADO)](./open-method-ado-recordset.md)  
        [Evento WillExecute (ADO)](./willexecute-event-ado.md)  
    :::column-end:::
:::row-end:::