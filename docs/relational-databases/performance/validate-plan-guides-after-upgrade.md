---
title: Convalidare le guide di piano dopo l'aggiornamento | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- plan guides [SQL Server], validating after upgrade
ms.assetid: a55ebd88-6f58-454d-b1c4-991b88add522
author: julieMSFT
ms.author: jrasnick
manager: craigg
ms.openlocfilehash: d325ac1d922956c92bd27eb099c655f72e5b2631
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/13/2018
ms.locfileid: "53366413"
---
# <a name="validate-plan-guides-after-upgrade"></a>Convalidare le guide di piano dopo l'aggiornamento
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Quando si aggiorna l'applicazione a una nuova versione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è consigliabile valutare nuovamente e testare le definizioni delle guide di piano. I requisiti di ottimizzazione delle prestazioni e la funzionalità di individuazione delle corrispondenze delle guide di piano possono cambiare. Anche se una guida di piano non valida non farà in modo che una query non riesca, il piano è compilato senza utilizzare la guida di piano e potrebbe non essere la migliore scelta. Dopo aver aggiornato un database a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], si consiglia di eseguire le seguenti attività:  
  
-   Eseguire la convalida delle guide di piano esistenti usando la funzione [sys.fn_validate_plan_guide](../../relational-databases/system-functions/sys-fn-validate-plan-guide-transact-sql.md) .  
  
-   Usare gli eventi estesi per eseguire il monitoraggio di piani fuorviati per determinati periodo di tempo usando l'evento [Plan Guide Unsuccessful](../../relational-databases/event-classes/plan-guide-unsuccessful-event-class.md) .  
  
  
