---
title: Il log shipping non viene eseguito dopo l'aggiornamento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server]
ms.assetid: 6727cb7d-ac01-4972-a730-dbb7cdc29705
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 952a47eaa2028819908ef7e93326c31a289a0cc2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66093976"
---
# <a name="log-shipping-will-not-run-after-upgrading"></a>Il log shipping non verrà eseguito dopo l'aggiornamento
  È in uso il log shipping. Il log shipping di [!INCLUDE[ssVersion2000](../../includes/ssversion2000-md.md)] non è compatibile con quello di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] e non può essere direttamente aggiornato. Dopo l'aggiornamento a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], riconfigurare il log shipping utilizzando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o le stored procedure.  
  
## <a name="see-also"></a>Vedi anche  
 [SQL Server Agent log shipping categoria di processi causa l'esito negativo dell'aggiornamento](../../../2014/sql-server/install/sql-server-agent-log-shipping-job-category-causes-upgrade-to-fail.md)   
 [L'aggiornamento modificherà l'account proxy utente SQL Server Agent al UpgradedProxyAccount temporaneo](../../../2014/sql-server/install/upgrading-changes-sql-server-agent-user-proxy-account-to-temporary-account.md)   
 [Problemi di aggiornamento motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)   
 [SQL Server 2014 preparazione aggiornamento &#91;nuova&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
