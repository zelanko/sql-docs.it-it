---
title: Autorizzazioni Guest nei database utente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 540f1c6d-df51-497e-958a-3a0f429d2920
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 344c5fd0639876998f1585c32fac5f7599f664e7
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85061662"
---
# <a name="guest-permissions-on-user-databases"></a>Autorizzazioni Guest nei database utente
  Questa regola consente di determinare se l'utente guest dispone dell'autorizzazione necessaria per accedere al database. Questa regola si applica solo ai database utente.  
  
## <a name="best-practices-recommendations"></a>Procedure consigliate  
 Se non è necessaria, revocare l'autorizzazione di accesso al database dell'utente guest.  
  
 L'utente guest non può essere rimosso. È tuttavia possibile disabilitarlo revocandone l'autorizzazione CONNECT tramite l'esecuzione di REVOKE CONNECT FROM GUEST all'interno di un database diverso da master, tempdb o msdb.  
  
## <a name="for-more-information"></a>Ulteriori informazioni  
 [Sicurezza di SQL Server](../security/securing-sql-server.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare e applicare le procedure consigliate tramite la gestione basata su criteri](monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
