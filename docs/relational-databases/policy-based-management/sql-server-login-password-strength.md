---
title: Livello di complessità delle password di accesso di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: b0862c3a-926b-490c-a37f-382e50146a3e
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: 8a392547d4e8b43430c2608f36790944eb88287f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 02/01/2020
ms.locfileid: "68043313"
---
# <a name="sql-server-login-password-strength"></a>Livello di complessità delle password di accesso di SQL Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Questa regola consente di controllare se è abilitata la funzionalità "Applica criteri password" di ogni account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Se è abilitata l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e la versione del sistema operativo è precedente a [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)], un utente malintenzionato potrebbe sfruttare ripetutamente una password di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nota.  
  
## <a name="best-practices-recommendations"></a>Procedure consigliate  
 È consigliabile aggiornare il sistema operativo a [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)].  
  
 Se nell'ambiente non è necessaria l'autenticazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , utilizzare l'autenticazione di Windows.  
  
 Abilitare "Applica criteri password" per tutti gli account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Per configurare i criteri password per gli account di accesso di [, utilizzare](../../t-sql/statements/alter-login-transact-sql.md) ALTER LOGIN [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="for-more-information"></a>Ulteriori informazioni  
 [Criteri password](../../relational-databases/security/password-policy.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare e applicare le procedure consigliate tramite la gestione basata su criteri](../../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
