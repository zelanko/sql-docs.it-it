---
title: Associare gli hint per le query a una guida di piano | Microsoft Docs
description: In una guida di piano è possibile utilizzare qualsiasi combinazione di hint per la query validi. Informazioni sull'associazione degli hint a una guida di piano in SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
ms.assetid: 2131f796-6359-4f9e-9047-da0b3d4dedaf
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 6a428f0cf913c4076e431314efc12bb52030d4c8
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/17/2020
ms.locfileid: "86458584"
---
# <a name="attach-query-hints-to-a-plan-guide"></a>Associazione degli hint per le query a una guida di piano
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  In una guida di piano è possibile utilizzare qualsiasi combinazione di hint per la query validi. Quando una guida di piano corrisponde a una query, la clausola OPTION specificata nella clausola dell'hint di una guida di piano viene aggiunta alla query prima che questa venga compilata e ottimizzata. Se una query che corrisponde a una guida di piano contiene già una clausola OPTION, gli hint per la query specificati nella guida di piano sostituiscono quelli della query. Perché una guida di piano possa corrispondere a una query che già contiene una clausola OPTION è tuttavia necessario includere la clausola OPTION della query quando si specifica il testo della query da far corrispondere nell'istruzione sp_create_plan_guide. Se si desidera che gli hint specificati nella guida di piano vengano aggiunti agli hint già esistenti nella query, invece di sostituirli è necessario specificare sia gli hint originali che gli hint aggiuntivi nella clausola OPTION della guida di piano.  
  
> [!CAUTION]  
>  L'utilizzo non corretto degli hint per la query da parte delle guide di piano può provocare problemi di compilazione, esecuzione o prestazioni. È consigliabile che le guide di piano vengano utilizzate solo da sviluppatori e amministratori esperti di database.  
  
## <a name="common-query-hints-used-in-plan-guides"></a>Hint per le query comuni utilizzate nelle guide di piano  
 Le query che possono trarre vantaggio dall'utilizzo di guide di piano sono in genere basate su parametri ed è possibile che le prestazioni siano insufficienti a causa dell'utilizzo di piani di query memorizzati nella cache nei quali i valori dei parametri non rappresentano il caso peggiore o lo scenario più rappresentativo. Per la risoluzione di questo problema è possibile utilizzare gli hint per le query OPTIMIZE FOR e RECOMPILE. OPTIMIZE FOR indica a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] di utilizzare un valore particolare per un parametro quando la query viene ottimizzata. RECOMPILE indica al server di eliminare un piano di query dopo l'esecuzione, forzando Query Optimizer alla compilazione di un nuovo piano di query alla successiva esecuzione della stessa query. Per un esempio, vedere [Guide di piano](../../relational-databases/performance/plan-guides.md).  
  
 Inoltre, è possibile specificare gli hint di tabella INDEX, FORCESCAN e FORCESEEK come hint per le query. Se specificati come hint per le query, tali hint si comportano come un hint di vista o di una tabella inline. L'hint INDEX impone a Query Optimizer di utilizzare soltanto gli indici specificati per accedere ai dati nella tabella o nella vista. L’hint FORCESEEK impone a Optimizer di utilizzare soltanto un’operazione Index Seek per accedere ai dati nella tabella o nella vista a cui si fa riferimento. Tali hint forniscono funzionalità della guida di piano aggiuntive e consentono di avere maggiore influenza sull'ottimizzazione di query che utilizzano la guida di piano.  
  
  
