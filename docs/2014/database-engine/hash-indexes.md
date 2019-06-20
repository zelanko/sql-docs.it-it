---
title: Indici hash | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f4bdc9c1-7922-4fac-8183-d11ec58fec4e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 263fdcd4b09c4acc6c2bba4d67629f867d64c6b3
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62779489"
---
# <a name="hash-indexes"></a>Indici hash
  Gli indici vengono utilizzati come punti di ingresso per le tabelle ottimizzate per la memoria. Per la lettura delle righe da una tabella è necessario un indice di individuare i dati in memoria.  
  
 Un indice hash è costituito da una raccolta di bucket organizzati in una matrice. Una funzione hash esegue il mapping delle chiavi di indice ai bucket dell'indice hash. Nella figura seguente sono illustrate tre chiavi di indice di cui viene eseguito il mapping a tre bucket diversi nell'indice hash. A scopo illustrativo il nome della funzione hash è f(x).  
  
 ![Chiavi di indice eseguito il mapping a bucket diversi. ](../../2014/database-engine/media/hekaton-tables-2.gif "Eseguito il mapping a bucket diversi di chiavi di indice.")  
  
 La funzione di hashing utilizzata per gli indici hash presenta le caratteristiche seguenti:  
  
-   In [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] è disponibile una funzione hash utilizzata per tutti gli indici hash.  
  
-   La funzione hash è deterministica. Per la stessa chiave di indice viene sempre eseguito il mapping allo stesso bucket nell'indice hash.  
  
-   È possibile che venga eseguito il mapping di più chiavi di indice allo stesso bucket di hash.  
  
-   La funzione hash viene bilanciata, pertanto la distribuzione dei valori di chiave di indice in bucket di hash segue in genere una distribuzione di probabilità di Poisson.  
  
     La distribuzione di probabilità di Poisson non è uniforme. I valori delle chiavi di indice non vengono distribuiti in modo uniforme nei bucket di hash. Ad esempio, una distribuzione di Poisson di *n* chiavi di indice distinct failover *n* i risultati in circa un terzo di bucket vuoti, un terzo di bucket contenenti una chiave di un indice e l'altro terzo di bucket di hash contenente due chiavi dell'indice. Un piccolo numero di bucket conterrà più di due chiavi.  
  
 Se viene eseguito il mapping di due chiavi dell'indice allo stesso bucket di hash, si verifica una collisione hash. Un numero elevato di collisioni hash può influire negativamente sulle prestazioni nelle operazioni di lettura.  
  
 La struttura dell'indice hash in memoria è costituita da una matrice di puntatori alla memoria. Per ogni bucket viene eseguito il mapping a un offset nella matrice. Ogni bucket nella matrice punta alla prima riga in tale bucket di hash. Ogni riga del bucket punta alla riga successiva, generando in tal modo una catena di righe per ogni bucket di hash, come illustrato nella figura seguente.  
  
 ![La struttura dell'indice hash in memoria. ](../../2014/database-engine/media/hekaton-tables-3.gif "La struttura dell'indice hash in memoria.")  
  
 Nella figura sono illustrati tre bucket con righe. Il secondo bucket dall'alto contiene le tre righe rosse. Il quarto bucket contiene una singola riga blu. Il bucket inferiore contiene due linee verdi. Queste possono essere diverse versioni della stessa riga.  
  
 Per altre informazioni sugli indici per tabelle ottimizzate per la memoria, vedere [linee guida per Using Indexes on Memory-Optimized Tables](../relational-databases/in-memory-oltp/memory-optimized-tables.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Indici in tabelle con ottimizzazione per la memoria](../../2014/database-engine/indexes-on-memory-optimized-tables.md)  
  
  
