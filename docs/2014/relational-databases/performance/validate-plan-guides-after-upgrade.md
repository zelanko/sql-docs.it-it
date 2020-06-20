---
title: Convalidare le guide di piano dopo l'aggiornamento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- plan guides [SQL Server], validating after upgrade
ms.assetid: a55ebd88-6f58-454d-b1c4-991b88add522
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 18cc0f93ddec46025f659bcb9489bfff3ca846ef
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85066747"
---
# <a name="validate-plan-guides-after-upgrade"></a>Convalidare le guide di piano dopo l'aggiornamento
  Quando si aggiorna l'applicazione a una nuova versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è consigliabile valutare nuovamente e testare le definizioni delle guide di piano. I requisiti di ottimizzazione delle prestazioni e la funzionalità di individuazione delle corrispondenze delle guide di piano possono cambiare. Anche se una guida di piano non valida non farà in modo che una query non riesca, il piano è compilato senza utilizzare la guida di piano e potrebbe non essere la migliore scelta. Dopo aver aggiornato un database a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], si consiglia di eseguire le seguenti attività:  
  
-   Eseguire la convalida delle guide di piano esistenti usando la funzione [sys.fn_validate_plan_guide](/sql/relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql) .  
  
-   Usare gli eventi estesi per eseguire il monitoraggio di piani fuorviati per determinati periodo di tempo usando l'evento [Plan Guide Unsuccessful](../event-classes/plan-guide-unsuccessful-event-class.md) .  
  
  
