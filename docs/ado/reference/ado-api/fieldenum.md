---
title: FieldEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- FieldEnum
helpviewer_keywords:
- FieldEnum enumeration [ADO]
ms.assetid: be4eda13-d4e4-4d6b-bb0d-3310b0a96fc2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5fe89d90510e95468e18b0d744ff566f69654320
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67932688"
---
# <a name="fieldenum"></a>FieldEnum
Specifica i campi speciali a cui fa riferimento una [Record](../../../ado/reference/ado-api/record-object-ado.md) dell'oggetto [campi](../../../ado/reference/ado-api/fields-collection-ado.md) raccolta.  
  
## <a name="remarks"></a>Note  
 Queste costanti rappresentano un "collegamento" per l'accesso a speciali campi associati a un **Record**. Recuperare il [campo](../../../ado/reference/ado-api/field-object.md) dell'oggetto dal **campi** insieme e quindi ottenere il contenuto con il **campo** dell'oggetto [valore](../../../ado/reference/ado-api/value-property-ado.md) proprietà.  
  
|Costante|Value|Descrizione|  
|--------------|-----------|-----------------|  
|**adDefaultStream**|-1|Fa riferimento al campo che contiene il valore predefinito [Stream](../../../ado/reference/ado-api/stream-object-ado.md) oggetto associato a un **Record**.|  
|**adRecordURL**|-2|Fa riferimento al campo che contiene la stringa URL assoluta per l'oggetto corrente **Record**.|
