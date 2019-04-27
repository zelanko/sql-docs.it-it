---
title: Risoluzione dei problemi di aggiornamento | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- installing Upgrade Advisor
- Upgrade Advisor [SQL Server], reference
- component issue resolution [Upgrade Advisor]
- resolving upgrade issues
- upgrade blocks [Upgrade Advisor]
- detecting upgrade issues
- finding upgrade issues
- Upgrade Advisor [SQL Server], blocking issues
- configurations preventing upgrading [Upgrade Advisor]
- locating upgrade issues
- blocking issues [Upgrade Advisor]
- issues preventing upgrading [Upgrade Advisor]
- Setup [Upgrade Advisor]
- SQL Server Upgrade Advisor, reference
- analyzing system [Upgrade Advisor], resolving issues
- settings preventing upgrading [Upgrade Advisor]
- upgrade issue reference [Upgrade Advisor]
- identifying upgrade issues
- fixing upgrade issues [Upgrade Advisor]
ms.assetid: 113eb435-8d36-4ed6-9790-b5e4c14809c8
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bad975eb6b2b2645cb31b075089c02be735b1d88
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62753323"
---
# <a name="resolving-upgrade-issues"></a>Risoluzione dei problemi di aggiornamento
  Negli argomenti di questa sezione vengono descritti i problemi relativi all'aggiornamento rilevabili e quelli non rilevabili che possono tuttavia influire sull'esecuzione dell'aggiornamento o del post-aggiornamento. I problemi sono organizzati per componente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="in-this-section"></a>In questa sezione  
  
-   [Problemi di aggiornamento più recenti](../../../2014/sql-server/install/late-breaking-upgrade-issues.md)  
  
-   [Problemi di aggiornamento del motore di database](../../../2014/sql-server/install/database-engine-upgrade-issues.md)  
  
-   [Problemi di aggiornamento della ricerca full-text](../../../2014/sql-server/install/full-text-search-upgrade-issues.md)  
  
-   [Problemi di aggiornamento della replica](../../../2014/sql-server/install/replication-upgrade-issues.md)  
  
-   [Problemi di aggiornamento di Reporting Services &#40;Preparazione aggiornamento&#41;](../../../2014/sql-server/install/reporting-services-upgrade-issues-upgrade-advisor.md)  
  
-   [Problemi di aggiornamento di SQL Server Agent](../../../2014/sql-server/install/sql-server-agent-upgrade-issues.md)  
  
## <a name="issues-that-prevent-upgrading"></a>Problemi che impediscono l'aggiornamento  
 Alcune configurazioni o impostazioni di una versione precedente di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] possono impedire l'esecuzione dell'aggiornamento a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Se il programma di installazione rileva questi problemi durante l'installazione di [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], il processo di aggiornamento viene arrestato e all'utente viene richiesto di eseguire Preparazione di aggiornamento e di risolvere i problemi che bloccano l'installazione.  
  
### [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
 Se le attività seguenti sono elencate nel report di aggiornamento del [!INCLUDE[ssDE](../../includes/ssde-md.md)], è necessario eseguire le azioni richieste prima dell'aggiornamento a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]:  
  
-   [Scollegare il database con ID 32767](../../../2014/sql-server/install/detach-database-id-32767.md)  
  
-   [Rinominare gli account di accesso con nomi uguali a quelli dei ruoli predefiniti del server](../../../2014/sql-server/install/rename-logins-matching-fixed-server-role-names.md)  
  
-   [Rinominare l'utente sys](../../../2014/sql-server/install/rename-user-sys.md)  
  
-   [Usare sp_rename per rinominare gli indici duplicati](../../../2014/sql-server/install/use-sp-rename-to-rename-duplicate-index-name.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Preparazione aggiornamento a SQL Server 2014 &#91;new&#93;](sql-server-2014-upgrade-advisor.md)  
  
  
