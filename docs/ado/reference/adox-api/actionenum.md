---
description: ActionEnum
title: ActionEnum indicante | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
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
ms.openlocfilehash: 2c9032dfdb3394e582541f60afce7b930751a5c0
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/24/2020
ms.locfileid: "88777780"
---
# <a name="actionenum"></a>ActionEnum
Specifica il tipo di azione da eseguire quando viene chiamata l' [autorizzazione](./setpermissions-method-adox.md) .  
  
|Costante|valore|Descrizione|  
|--------------|-----------|-----------------|  
|**adAccessDeny**|3|Al gruppo o all'utente verranno negate le autorizzazioni specificate.|  
|**adAccessGrant**|1|Il gruppo o l'utente avrà almeno le autorizzazioni richieste.|  
|**adAccessRevoke**|4|Eventuali diritti di accesso espliciti al gruppo o all'utente verranno revocati.|  
|**adAccessSet**|2|Il gruppo o l'utente avrà esattamente le autorizzazioni richieste.|