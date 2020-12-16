---
title: Definire una base di riferimento delle prestazioni | Microsoft Docs
description: Misurare le prestazioni a intervalli di tempo regolari, anche quando non si è verificato alcun problema, in modo da definire una baseline per le prestazioni del server in SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- database performance [SQL Server], baselines
- monitoring performance [SQL Server], baselines
- tuning databases [SQL Server], baselines
- server performance [SQL Server], baselines
- performance [SQL Server], baselines
- baseline performance [SQL Server]
- measurements for baseline statistics [SQL Server]
- monitoring server performance [SQL Server], establishing baseline
- database monitoring [SQL Server], baselines
ms.assetid: dc5aa8d6-2507-448f-ad86-4196443915fc
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ebe94b0a4d678b888d99e51b7bda4c0addd0f17b
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97461922"
---
# <a name="establish-a-performance-baseline"></a>Definire una base di riferimento delle prestazioni
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Per stabilire se le prestazioni del sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono ottimali, misurare le prestazioni a intervalli di tempo regolari, anche quando non si è verificato alcun problema, in modo da definire una base di riferimento per le prestazioni del server. Confrontare ogni set di misurazioni con i set precedenti.  
  
 Le aree seguenti influiscono sulle prestazioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Risorse di sistema (hardware)  
  
-   Architettura di rete  
  
-   Sistema operativo  
  
-   Applicazioni di database  
  
-   Applicazioni client  
  
 Le misurazioni di riferimento devono essere utilizzate almeno per determinare gli elementi seguenti:  
  
-   Orari di punta e di minore attività.  
  
-   Tempi di risposta di query o batch di comandi.  
  
-   Tempi necessari per il completamento di operazioni di backup e ripristino dei database.  
  
 Dopo aver definito una base di riferimento attendibile, confrontare i dati statistici di riferimento con le prestazioni correnti del server. I valori notevolmente superiori o inferiori a quelli di riferimento sono possibili candidati per analisi più approfondite. Tali scostamenti possono indicare aree per cui sono necessari interventi di ottimizzazione o riconfigurazione. In presenza di un aumento dei tempi di esecuzione di un set di query, ad esempio, esaminare le query per verificare se è possibile riscriverle oppure se è necessario aggiungere statistiche di colonna o nuovi indici.  
  
## <a name="see-also"></a>Vedere anche  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
  
