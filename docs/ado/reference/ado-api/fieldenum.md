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
author: rothja
ms.author: jroth
ms.openlocfilehash: 24d69ac1406363458c8dbd3168e6d25309cfa2c4
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/04/2020
ms.locfileid: "82762572"
---
# <a name="fieldenum"></a>FieldEnum
Specifica i campi speciali a cui viene fatto riferimento nella raccolta di [campi](../../../ado/reference/ado-api/fields-collection-ado.md) di un oggetto [record](../../../ado/reference/ado-api/record-object-ado.md) .  
  
## <a name="remarks"></a>Osservazioni  
 Queste costanti forniscono un "collegamento" per accedere ai campi speciali associati a un **record**. Recuperare l'oggetto [campo](../../../ado/reference/ado-api/field-object.md) dalla raccolta **Fields** e quindi ottenere il relativo contenuto con la proprietà [value](../../../ado/reference/ado-api/value-property-ado.md) dell'oggetto **campo** .  
  
|Costante|Valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adDefaultStream**|-1|Fa riferimento al campo contenente l'oggetto [flusso](../../../ado/reference/ado-api/stream-object-ado.md) predefinito associato a un **record**.|  
|**adRecordURL**|-2|Fa riferimento al campo contenente la stringa URL assoluta per il **record**corrente.|
