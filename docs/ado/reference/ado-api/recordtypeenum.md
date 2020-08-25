---
description: RecordTypeEnum
title: RecordTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- RecordTypeEnum
helpviewer_keywords:
- RecordTypeEnum enumeration [ADO]
ms.assetid: f557e537-015d-4ba7-8a41-a6f00b366a91
author: rothja
ms.author: jroth
ms.openlocfilehash: a1e5a43d2b53a76a21d79ce671004e139dab5e20
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88771990"
---
# <a name="recordtypeenum"></a>RecordTypeEnum
Specifica il tipo di oggetto [record](./record-object-ado.md) .  
  
|Costante|valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adSimpleRecord**|0|Indica un record *semplice* (non contiene nodi figlio).|  
|**adCollectionRecord**|1|Indica un record di *raccolta* (contiene i nodi figlio).|  
|**adRecordUnknown**|-1|Indica che il tipo di questo **record** è sconosciuto.|  
|**adStructDoc**|2|Indica un tipo speciale di record di *raccolta* che rappresenta i documenti strutturati com.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Queste costanti non dispongono di equivalenti ADO/WFC.  
  
## <a name="applies-to"></a>Si applica a  
 [Proprietà RecordType (ADO)](./recordtype-property-ado.md)