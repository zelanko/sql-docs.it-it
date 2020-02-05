---
title: Autorizzazioni Guest nei database utente | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 540f1c6d-df51-497e-958a-3a0f429d2920
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: cbe3efe2337b8e967ea7b5ced9fc6b3890d989e5
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68087287"
---
# <a name="guest-permissions-on-user-databases"></a>Autorizzazioni Guest nei database utente
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Questa regola consente di determinare se l'utente guest dispone dell'autorizzazione necessaria per accedere al database. Questa regola si applica solo ai database utente.  
  
## <a name="best-practices-recommendations"></a>Procedure consigliate  
 Se non è necessaria, revocare l'autorizzazione di accesso al database dell'utente guest.  
  
 L'utente guest non può essere rimosso. È tuttavia possibile disabilitarlo revocandone l'autorizzazione CONNECT tramite l'esecuzione di REVOKE CONNECT FROM GUEST all'interno di un database diverso da master, tempdb o msdb.  
  
## <a name="for-more-information"></a>Ulteriori informazioni  
 [Sicurezza di SQL Server](../../relational-databases/security/securing-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare e applicare le procedure consigliate tramite la gestione basata su criteri](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
