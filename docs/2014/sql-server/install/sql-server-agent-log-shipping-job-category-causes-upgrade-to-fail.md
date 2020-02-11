---
title: SQL Server Agent log shipping categoria di processi causa l'esito negativo dell'aggiornamento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- log shipping [SQL Server Agent]
- job categories [SQL Server Agent]
ms.assetid: ef05ce53-c6ce-42ec-9df8-46c951626424
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7145d846657613b50706ebe75c9832f40f49383e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "66092035"
---
# <a name="sql-server-agent-log-shipping-job-category-causes-upgrade-to-fail"></a>La categoria di processi per il log shipping di SQL Server Agent impedisce il completamento dell'aggiornamento
  Il processo di aggiornamento non verrà completato se esiste una categoria di processi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent denominata Log shipping.  
  
## <a name="component"></a>Componente  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Agente  
  
## <a name="description"></a>Descrizione  
 Esiste una categoria di processi di sistema denominata Log shipping. Se una delle installazioni da aggiornare contiene già una categoria di processi creata dall'utente denominata Log shipping, sarà necessario rinominarla prima dell'aggiornamento. In caso contrario, l'aggiornamento non verrà completato.  
  
## <a name="see-also"></a>Vedere anche  
 [Il log shipping non viene eseguito dopo l'aggiornamento](../../../2014/sql-server/install/log-shipping-will-not-run-after-upgrading.md)   
 [L'aggiornamento modificherà l'account proxy utente SQL Server Agent al UpgradedProxyAccount temporaneo](../../../2014/sql-server/install/upgrading-changes-sql-server-agent-user-proxy-account-to-temporary-account.md)   
 [Problemi di aggiornamento di SQL Server Agent](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
  
