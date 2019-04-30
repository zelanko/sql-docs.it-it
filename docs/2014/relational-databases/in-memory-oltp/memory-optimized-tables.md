---
title: Tabelle con ottimizzazione per la memoria | Microsoft Docs
ms.custom: ''
ms.date: 10/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 14dddf81-b502-49dc-a6b6-d18b1ae32d2b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9123bf89f75fce68a6edd8ba1becd141821fe326
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63158759"
---
# <a name="memory-optimized-tables"></a>Tabelle con ottimizzazione per la memoria
  Con la funzionalità OLTP in memoria di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] è possibile migliorare le prestazioni delle applicazioni OLTP tramite l'accesso ai dati efficiente e ottimizzato per la memoria, la compilazione nativa della logica di business e gli algoritmi senza blocchi e latch. La funzionalità include tabelle ottimizzate per la memoria e tipi di tabella, nonché la compilazione nativa delle stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] per l'accesso efficiente a queste tabelle.  
  
 Per ulteriori informazioni sulle tabelle ottimizzate per la memoria, vedere:  
  
-   [Introduzione alle tabelle con ottimizzazione per la memoria](memory-optimized-tables.md)  
  
     Descrive le tabelle ottimizzate per la memoria e fornisce informazioni sulla durabilità dei dati, sull'accesso ai dati nelle tabelle ottimizzate per la memoria e sulle prestazioni e la scalabilità.  
  
-   [Compilazione nativa di tabelle e stored procedure](../in-memory-oltp/natively-compiled-stored-procedures.md)  
  
     Descrive come vengono compilate in DLL le tabelle ottimizzate per la memoria e le stored procedure compilate in modo nativo e fornisce considerazioni correlate alla sicurezza.  
  
-   [Modifica di tabelle con ottimizzazione per la memoria](altering-memory-optimized-tables.md)  
  
     Linee guida per l'aggiornamento delle tabelle ottimizzate per la memoria, compresa la modifica di colonne di tabella, indici e bucket_count.  
  
-   [Informazioni sulle transazioni in tabelle con ottimizzazione per la memoria](../../database-engine/understanding-transactions-on-memory-optimized-tables.md)  
  
     Questa sezione fornisce diversi argomenti relativi all'esecuzione di transazioni in tabelle ottimizzate per la memoria compresi i livelli di isolamento delle transazioni e le transazioni tra contenitori.  
  
-   [Modello di applicazione per il partizionamento di tabelle con ottimizzazione per la memoria](application-pattern-for-partitioning-memory-optimized-tables.md)  
  
     Esempio di codice dettagliato che mostra come emulare le tabelle partizionate quando vengono usate le tabelle ottimizzate per la memoria.  
  
-   [Statistiche per tabelle con ottimizzazione per la memoria](statistics-for-memory-optimized-tables.md)  
  
     Descrive come vengono compilate le statistiche per le tabelle ottimizzate per la memoria e come gestire e aggiornare manualmente le statistiche per le tabelle ottimizzate per la memoria.  
  
-   [Tabelle codici e regole di confronto](../../database-engine/collations-and-code-pages.md)  
  
     Descrive le restrizioni sulle tabelle codici e le regole di confronto supportate per le tabelle ottimizzate per la memoria.  
  
-   [Dimensioni di tabelle e righe per le tabelle con ottimizzazione per la memoria](table-and-row-size-in-memory-optimized-tables.md)  
  
     Descrive il limite di 8.060 byte per le righe delle tabelle ottimizzate per la memoria e fornisce un esempio per calcolare le dimensioni di righe e tabelle.  
  
-   [Guida all'elaborazione delle query per le tabelle con ottimizzazione per la memoria](a-guide-to-query-processing-for-memory-optimized-tables.md)  
  
     Fornisce una panoramica sull'elaborazione delle query per le tabelle ottimizzate per la memoria e le stored procedure compilate in modo nativo.  
  
## <a name="see-also"></a>Vedere anche  
 [OLTP in memoria &#40;ottimizzazione per la memoria&#41;](in-memory-oltp-in-memory-optimization.md)  
  
  
