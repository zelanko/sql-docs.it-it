---
title: MSSQLSERVER_10532 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10532 (Database Engine error)
ms.assetid: 01da29ee-bf67-433f-8148-587a7e8d1d76
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 050f1c4e1c47458e513e02d16eb3ea6dc7e842a8
ms.sourcegitcommit: 454270de64347db917ebe41c081128bd17194d73
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005992"
---
# <a name="mssqlserver_10532"></a>MSSQLSERVER_10532
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>Dettagli  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|10532|  
|Origine evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbolico|PG_NO_ELIGIBLE_STMT|  
|Testo del messaggio|Impossibile creare la guida di piano '%.\*ls' perché il batch o il modulo specificato da **\@plan_handle** non contiene un'istruzione idonea per una guida di piano. Specificare un valore diverso per **\@plan_handle**.|  
  
## <a name="explanation"></a>Spiegazione  
Il batch o il modulo specificato da **\@plan_handle** non contiene un'istruzione idonea per una guida di piano.  
  
## <a name="user-action"></a>Azione dell'utente  
Specificare un valore diverso per **\@plan_handle**.  
  
## <a name="see-also"></a>Vedere anche  
[Guide di piano](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle &#40;Transact-SQL&#41;](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
