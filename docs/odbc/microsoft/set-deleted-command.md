---
title: IMPOSTA comando eliminato | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET DELETED command [ODBC]
ms.assetid: 6b5e0086-156d-471d-8e7f-6c5fa9686cd5
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 54900f00e03e1f236baf0b6eef152081b1f384a1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67997741"
---
# <a name="set-deleted-command"></a>SET DELETED (comando)
Specifica se i record contrassegnati per l'eliminazione vengono elaborati e se sono disponibili per l'utilizzo in altri comandi.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SET DELETED ON | OFF  
```  
  
## <a name="arguments"></a>Argomenti  
 ATTIVA  
 (Impostazione predefinita per il driver; l'impostazione predefinita per Visual FoxPro è OFF). Specifica che i comandi che operano sui record (inclusi i record nelle tabelle correlate) che utilizzano un ambito ignorano i record contrassegnati per l'eliminazione.  
  
 OFF  
 Specifica che i record contrassegnati per l'eliminazione possono essere accessibili tramite comandi che operano sui record (inclusi i record nelle tabelle correlate) utilizzando un ambito.  
  
## <a name="remarks"></a>Osservazioni  
 Le query che usano DELETED () per testare lo stato dei record possono essere ottimizzate usando la tecnologia Visual FoxPro Rushmore se la tabella è indicizzata in DELETED ().  
  
> [!IMPORTANT]  
>  SET DELETED viene ignorato se l'ambito predefinito del comando è il record corrente o se si include un ambito di un singolo record. INDEX ignora sempre SET DELETED e indicizza tutti i record nella tabella.  
  
## <a name="see-also"></a>Vedere anche  
 [DELETE (comando SQL)](../../odbc/microsoft/delete-sql-command.md)
