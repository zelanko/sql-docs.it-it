---
title: MSSQLSERVER_10502 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10502 (Database Engine error)
ms.assetid: 26d9b64d-4299-4b55-92d0-0a32a3688c0a
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3b6120a7f5c0479bb23894d1368c903a27f1de65
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85781525"
---
# <a name="mssqlserver_10502"></a>MSSQLSERVER_10502
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
|Nome prodotto|SQL Server|  
|ID evento|10502|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|PG_DUP_FOUND|  
|Testo del messaggio|Impossibile creare la guida di piano '%.*ls' perché l'istruzione specificata da @stmt e @module_or_batch o da @plan_handle e @statement_start_offset corrisponde alla guida di piano '%.\*ls' esistente nel database. Eliminare la guida di piano esistente prima di creare quella nuova.|  
  
## <a name="explanation"></a>Spiegazione  
Per l'istruzione specificata esiste già una guida di piano.  
  
## <a name="user-action"></a>Azione dell'utente  
Eliminare la guida di piano esistente prima di creare quella nuova.  
  
## <a name="see-also"></a>Vedere anche  
[Guide di piano](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
