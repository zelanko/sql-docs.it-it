---
description: FieldEnum
title: FieldEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
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
ms.openlocfilehash: 2bdcec83c211f71803ea64b7b78f3e6f8c76dee6
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88973132"
---
# <a name="fieldenum"></a>FieldEnum
Specifica i campi speciali a cui viene fatto riferimento nella raccolta di [campi](./fields-collection-ado.md) di un oggetto [record](./record-object-ado.md) .  
  
## <a name="remarks"></a>Osservazioni  
 Queste costanti forniscono un "collegamento" per accedere ai campi speciali associati a un **record**. Recuperare l'oggetto [campo](./field-object.md) dalla raccolta **Fields** e quindi ottenere il relativo contenuto con la proprietà [value](./value-property-ado.md) dell'oggetto **campo** .  
  
|Costante|Valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adDefaultStream**|-1|Fa riferimento al campo contenente l'oggetto [flusso](./stream-object-ado.md) predefinito associato a un **record**.|  
|**adRecordURL**|-2|Fa riferimento al campo contenente la stringa URL assoluta per il **record**corrente.|