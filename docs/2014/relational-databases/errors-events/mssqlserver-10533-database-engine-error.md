---
title: MSSQLSERVER_10533 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10533 (Database Engine error)
ms.assetid: cc2fbdab-7b90-415f-a1f9-066824344283
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 82b771c639681a1064cbde3ddee3c344b29c2990
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554136"
---
# <a name="mssqlserver_10533"></a>MSSQLSERVER_10533
    
## <a name="details"></a>Dettagli  
  
|Attributo|valore|  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|10533|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|PG_NAME_TOO_BIG|  
|Testo del messaggio|Impossibile creare la guida di piano '%.*ls' perché il nome della guida di piano supera la lunghezza massima consentita di 124 caratteri. Specificare un nome che contiene meno di 125 caratteri.|  
  
## <a name="explanation"></a>Spiegazione  
 Il nome della guida di piano supera la lunghezza massima consentita di 124 caratteri.  
  
## <a name="user-action"></a>Azione dell'utente  
 Specificare un nome che contiene meno di 125 caratteri.  
  
## <a name="see-also"></a>Vedere anche  
 [Guide di piano](../performance/plan-guides.md)   
 [sp_create_plan_guide &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
