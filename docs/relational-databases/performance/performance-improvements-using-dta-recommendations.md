---
title: Indicazioni di Ottimizzazione guidata motore di database per il miglioramento delle prestazioni
description: Informazioni su come Ottimizzazione guidata motore di database può proporre una combinazione di indici rowstore e columnstore grazie all'analisi di un carico di lavoro del database in SQL Server.
ms.custom: seo-dt-2019
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Database Engine Tuning Advisor, performance improvements
ms.assetid: 2e51ea06-81cb-4454-b111-da02808468e6
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: e6d392cedebec98c00ca6dac84dcc1d2fee21258
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505105"
---
# <a name="performance-improvements-using-database-engine-tuning-advisor-dta-recommendations"></a>Miglioramenti delle prestazioni mediante le indicazioni di Ottimizzazione guidata motore di database
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]


---
Le prestazioni dei carichi di lavoro di data warehousing e analisi possono trarre vantaggio dagli indici **columnstore**, in particolare per le query che devono eseguire l'analisi di tabelle di grandi dimensioni. Gli indici **Rowstore** (albero B+-) sono particolarmente utili per le query che accedono a quantità relativamente piccole di dati durante la ricerca di un determinato valore o intervallo di valori. Poiché possono restituire righe ordinate, gli indici rowstore consentono anche di ridurre il costo dell'ordinamento nei piani di esecuzione delle query. Pertanto, la scelta della combinazione di indici rowstore e columnstore da compilare dipende dal carico di lavoro dell'applicazione.

A partire da SQL Server 2016, Ottimizzazione guidata motore di database può proporre una **combinazione di indici rowstore e columnstore** appropriata grazie all'analisi di uno specifico carico di lavoro del database. 

Per illustrare i vantaggi delle indicazioni di Ottimizzazione guidata motore di database relative alle prestazioni del carico di lavoro, abbiamo provato diversi carichi di lavoro reali dei clienti. Per ogni carico di lavoro dei clienti, Ottimizzazione guidata motore di database analizza le singole query e il carico di lavoro completo delle query. Consideriamo tre alternative:
  
  1. **Solo indici columnstore**: compilare solo gli indici columnstore per tutte le tabelle senza usare Ottimizzazione guidata motore di database. 
  2. **Ottimizzazione guidata motore di database (solo indici rowstore)** : eseguire Ottimizzazione guidata motore di database con l'opzione di specificare indicazioni solo per gli indici rowstore.
  3. **Ottimizzazione guidata motore di database (indici rowstore + columnstore)** : eseguire Ottimizzazione guidata motore di database con l'opzione per specificare indicazioni sia per gli indici rowstore che per gli indici columnstore.  
   
In ogni caso abbiamo implementato gli indici consigliati. Viene evidenziato il tempo di CPU (in millisecondi) come valore medio di più esecuzioni della query o del carico di lavoro. Nella figura seguente è riportato il tempo di CPU in millisecondi per i carichi di lavoro tra due diversi database dei clienti. Si noti che l'asse y (tempo di CPU) usa una scala logaritmica.   


![Screenshot di un grafico a barre che mostra le prestazioni rowstore columnstore DTA.](../../relational-databases/performance/media/dta-columnstore-rowstore-performance.gif)



**Necessità di progettazioni fisiche miste**: primo set di barre corrispondente a Cliente 1 Query 1. L'indicazione di Ottimizzazione guidata motore di database (rowstore + columnstore) che prevede un set di quattro indici columnstore e sei indici rowstore ha come risultato un tempo di CPU da 2,5 a 4 volte inferiore rispetto all'uso del solo indice columnstore e di Ottimizzazione guidata motore di database (solo rowstore). Questo esempio dimostra i vantaggi delle progettazioni fisiche miste costituite da indici rowstore e columnstore *anche per una singola query*. 

**Efficacia delle indicazioni relative agli indici rowstore**: il secondo e terzo set di barre, corrispondenti a Cliente 1 Query 2 e a Cliente 2 Query 1, sono casi in cui le query includono predicati del filtro selettivo che traggono vantaggio dagli indici rowstore adatti. Per entrambe queste query, Ottimizzazione guidata motore di database (solo rowstore) e Ottimizzazione guidata motore di database (rowstore + columnstore) consigliano l'uso solo degli indici rowstore. Questi esempi illustrano inoltre che, anche se Ottimizzazione guidata motore di database viene chiamato con l'opzione per consigliare gli indici columnstore, il relativo approccio basato sui costi fa sì che venga proposto un indice columnstore solo se effettivamente il carico di lavoro può trarne vantaggio.

**Efficacia delle indicazioni relative agli indici columnstore**: il quarto set di barre corrispondente a Cliente 2 Query 2 rappresenta un caso in cui la query esegue l'analisi di tabelle di grandi dimensioni e può trarre beneficio dagli indici columnstore. Ottimizzazione guidata motore di database (solo rowstore) genera un'indicazione il cui tempo di CPU è superiore rispetto a quando sono presenti gli indici columnstore. Ottimizzazione guidata motore di database (rowstore + columnstore) consiglia gli indici columnstore adatti, ottenendo prestazioni di esecuzione delle query corrispondenti a quelle in cui viene usata l'opzione basata solo su indici columnstore.

**Efficacia delle indicazioni per il carico di lavoro con più query**: il set finale di barre corrispondente al carico di lavoro completo per Cliente 2 illustra la capacità di Ottimizzazione guidata motore di database di analizzare più query nel carico di lavoro per consigliare un set appropriato di indici rowstore e columnstore al fine di migliorare il costo di esecuzione complessivo del carico di lavoro. Ottimizzazione guidata motore di database (rowstore + columnstore) consiglia quattro indici columnstore e decine di indici rowstore, ottenendo come risultato un rilevante miglioramento delle prestazioni per il carico di lavoro, se confrontato con l'opzione che prevede la compilazione solo di indici columnstore, nonché un miglioramento da 4 a 5 volte superiore se confrontato con Ottimizzazione guidata motore di database (solo rowstore).

In sintesi, gli esempi precedenti illustrano la capacità di Ottimizzazione guidata motore di database di sfruttare gli indici sia rowstore che columnstore supportati nel motore di database di SQL Server e di consigliare una combinazione appropriata di indici in grado di ridurre in modo significativo il tempo di CPU per il carico di lavoro. 

<a name="see-also"></a>Vedere anche
---
[Database Engine Tuning Advisor](../../relational-databases/performance/database-engine-tuning-advisor.md)

[Indicazioni relative agli indici columnstore in Ottimizzazione guidata motore di database](../../relational-databases/performance/columnstore-index-recommendations-in-database-engine-tuning-advisor-dta.md)

[Guida agli indici columnstore](~/relational-databases/indexes/columnstore-indexes-overview.md)

[Indici columnstore per il data warehousing](~/relational-databases/indexes/columnstore-indexes-data-warehouse.md)

[CREATE COLUMNSTORE INDEX (Transact-SQL)](../../t-sql/statements/create-columnstore-index-transact-sql.md)

[CREATE INDEX (Transact-SQL)](../../t-sql/statements/create-index-transact-sql.md)



