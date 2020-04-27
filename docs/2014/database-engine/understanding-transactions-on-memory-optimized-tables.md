---
title: Informazioni sulle transazioni nelle tabelle ottimizzate per la memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 06075248-705e-4563-9371-b64cd609793c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4ceedcedae64bf2ec8f8ede0ccbb99350b979fd7
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62773379"
---
# <a name="understanding-transactions-on-memory-optimized-tables"></a>Informazioni sulle transazioni in tabelle con ottimizzazione per la memoria
  Le transazioni accedono a tabelle ottimizzate per la memoria tramite una forma di controllo della concorrenza ottimistica con più versioni. Ciò significa che sono presenti versioni diverse dei dati. Ogni transazione viene eseguita nella propria versione del database coerente a livello di transazione, indipendentemente da altre transazioni in esecuzione simultanea. Le transazioni vengono inoltre eseguite nel presupposto ottimistico che non saranno presenti conflitti con altre transazioni simultanee, evitando in tal modo la necessità di utilizzare blocchi, ma richiedendo il rilevamento automatico di conflitti e l'interruzione di una delle transazioni in conflitto. I conflitti possono verificarsi solo per le transazioni di scrittura-scrittura e per le transazioni di lettura e scrittura. Se si verifica un conflitto di scrittura-scrittura, una transazione di scrittura viene terminata.  
  
 Esistono analogie tra il controllo della concorrenza per le tabelle ottimizzate per la memoria e il controllo della concorrenza per le tabelle basate su disco per i livelli di isolamento delle transazioni READ_COMMITTED_SNAPSHOT e SNAPSHOT. Per ulteriori informazioni sulle tabelle basate su disco, vedere [livelli di isolamento basati sul controllo delle versioni delle righe nella motore di database](https://msdn.microsoft.com/library/ms177404\(v=sql.100\).aspx).  
  
## <a name="topics-in-this-section"></a>Contenuto della sezione  
 In questa sezione sulle transazioni in tabelle ottimizzate per la memoria sono inclusi gli argomenti seguenti:  
  
-   [Linee guida per i livelli di isolamento delle transazioni con tabelle con ottimizzazione per la memoria](../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
-   [Linee guida per la logica di riesecuzione per le transazioni in tabelle con ottimizzazione per la memoria](guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md)  
  
-   [Transazioni in tabelle con ottimizzazione per la memoria](transactions-in-memory-optimized-tables.md)  
  
-   [Livelli di isolamento delle transazioni](transaction-isolation-levels.md)  
  
-   [Transazioni tra contenitori](cross-container-transactions.md)  
  
 Per altre informazioni, vedere [Controllo della durabilità delle transazioni](../relational-databases/logs/control-transaction-durability.md).  
  
## <a name="see-also"></a>Vedi anche  
 [Tabelle con ottimizzazione per la memoria](../relational-databases/in-memory-oltp/memory-optimized-tables.md)  
  
  
