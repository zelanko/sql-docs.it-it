---
title: Impostare l'opzione di database AUTO_SHRINK su OFF | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 16403850-d745-4754-b84f-5f01aaecd24e
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 2b202f2856e066047c5458ef8ed1f40b2422b391
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68021696"
---
# <a name="set-the-autoshrink-database-option-to-off"></a>Impostazione dell'opzione di database AUTO_SHRINK su OFF
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Questa regola consente di controllare se l'opzione di database AUTO_SHRINK è impostata su OFF. La compattazione e l'espansione di un database comportano spesso la frammentazione fisica.  
  
## <a name="best-practices-recommendations"></a>Procedure consigliate  
 Impostare l'opzione di database AUTO_SHRINK su OFF. Se si prevede che lo spazio recuperato non sarà necessario in futuro, è possibile liberare spazio compattando manualmente il database.  
  
## <a name="for-more-information"></a>Ulteriori informazioni  
 Articolo [315512](https://go.microsoft.com/fwlink/?linkid=117750)della Microsoft Knowledge Base  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare e applicare le procedure consigliate tramite la gestione basata su criteri](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
