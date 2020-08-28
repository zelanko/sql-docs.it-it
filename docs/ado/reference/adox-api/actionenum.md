---
description: ActionEnum
title: ActionEnum indicante | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: ado
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- ActionEnum
helpviewer_keywords:
- ActionEnum enumeration [ADOX]
ms.assetid: f948febd-c885-4621-823b-421e116fec4e
author: rothja
ms.author: jroth
ms.openlocfilehash: 02422de45f3e0ec28901678528468dc72f021549
ms.sourcegitcommit: 18a98ea6a30d448aa6195e10ea2413be7e837e94
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/27/2020
ms.locfileid: "88985922"
---
# <a name="actionenum"></a>ActionEnum
Specifica il tipo di azione da eseguire quando viene chiamata l' [autorizzazione](./setpermissions-method-adox.md) .  
  
|Costante|Valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adAccessDeny**|3|Al gruppo o all'utente verranno negate le autorizzazioni specificate.|  
|**adAccessGrant**|1|Il gruppo o l'utente avrà almeno le autorizzazioni richieste.|  
|**adAccessRevoke**|4|Eventuali diritti di accesso espliciti al gruppo o all'utente verranno revocati.|  
|**adAccessSet**|2|Il gruppo o l'utente avrà esattamente le autorizzazioni richieste.|