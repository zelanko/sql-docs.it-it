---
description: MemberTypeEnum
title: MemberTypeEnum | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- MemberTypeEnum
helpviewer_keywords:
- MemberTypeEnum enumeration [ADO MD]
ms.assetid: 5d8132c0-7ca2-4f86-8336-1b34213869ad
author: rothja
ms.author: jroth
ms.openlocfilehash: 186ef16dfaafac2151436a3cd63e944de2468457
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777960"
---
# <a name="membertypeenum"></a>MemberTypeEnum
Specifica l'impostazione per la proprietà [Type](./type-property-ado-md.md) di un oggetto [membro](./member-object-ado-md.md) .  
  
|Costante|valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adMemberAll**|4|Indica che l'oggetto **membro** rappresenta tutti i membri del livello.|  
|**adMemberFormula**|3|Indica che l'oggetto **membro** viene calcolato utilizzando un'espressione di formula.|  
|**adMemberMeasure**|2|Indica che l'oggetto **membro** appartiene alla dimensione Measures e rappresenta un attributo quantitativo.|  
|**adMemberRegular**|1|Valore predefinito. Indica che l'oggetto **membro** rappresenta un'istanza di un'entità business.|  
|**adMemberUnknown**|0|Impossibile determinare il tipo del membro.|