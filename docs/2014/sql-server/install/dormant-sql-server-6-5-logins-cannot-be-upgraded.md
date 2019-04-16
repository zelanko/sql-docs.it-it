---
title: Non è possibile aggiornare l'account di accesso di SQL Server 6.5 inattivi | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- passwords [SQL Server], dormant logins
- dormant logins
- logins [SQL Server], upgrading dormant logins
- identifying dormant logins
- password hashes [SQL Server]
ms.assetid: ebe18a74-0375-4df4-b894-239f8fdabb64
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 0381e04ae1df53e5502c49eb17d0823fcf611e89
ms.sourcegitcommit: 46a2c0ffd0a6d996a3afd19a58d2a8f4b55f93de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/15/2019
ms.locfileid: "59582177"
---
# <a name="dormant-sql-server-65-logins-cannot-be-upgraded"></a>Impossibile aggiornare gli account di accesso di SQL Server 6.5 inattivi
  Preparazione aggiornamento ha rilevato un account di accesso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la cui password non può essere direttamente aggiornata a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Per attivare questo account di accesso, è necessario reimpostarne la password. Utilizzare ALTER LOGIN per reimpostare la password.  
  
```  
ALTER LOGIN <login name> WITH PASSWORD = '<new password>' MUST_CHANGE  
```  
  
 La nuova password verrà convalidata in base ai criteri di complessità delle password del sistema, a meno che il controllo dei criteri non sia disabilitato. È consigliabile utilizzare password complesse e non disabilitare il controllo dei criteri. L'opzione MUST_CHANGE impone all'utente la selezione di una nuova password. Tale procedura non è necessaria ma è consigliabile.  
  
 Per identificare gli account di accesso inattivi utilizzare la query seguente:  
  
```  
SELECT * FROM sysxlogins WHERE (xstatus & 2048) = 2048;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Problemi di aggiornamento del motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [Preparazione aggiornamento a SQL Server 2014 &#91;new&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
