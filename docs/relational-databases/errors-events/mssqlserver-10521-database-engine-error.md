---
title: MSSQLSERVER_10521 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10521 (Database Engine error)
ms.assetid: ba2d7e44-207c-4428-b5f0-c975ac122c0d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 3daa4f6dcfc9be9f34da2be3c1344dd694b811ae
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85781478"
---
# <a name="mssqlserver_10521"></a>MSSQLSERVER_10521
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Dettagli  
  
| Attributo | valore |  
| :-------- | :---- |  
|Nome prodotto|SQL Server|  
|ID evento|10521|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|PG_PARAM_NEEDED|  
|Testo del messaggio|Impossibile creare la guida di piano '%.\*ls' perché **\@type** è stato specificato come '%ls' e il parametro '%ls' è NULL. Questo tipo richiede un valore non NULL per il parametro. Specificare un valore non NULL per il parametro oppure impostare un tipo che consenta un valore NULL per il parametro.|  
  
## <a name="explanation"></a>Spiegazione  
Il tipo indicato in **\@type** richiede un valore NULL per il parametro specificato, ma è stato fornito un valore NULL.  
  
## <a name="user-action"></a>Azione dell'utente  
Specificare un valore non NULL per il parametro oppure impostare un tipo che consenta un valore NULL per il parametro.  
  
## <a name="see-also"></a>Vedere anche  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[Guide di piano](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
