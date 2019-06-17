---
title: Ripristinare e recuperare tabelle con ottimizzazione per la memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 294975b7-e7d1-491b-b66a-fdb1100d2acc
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 9560249e07cbd360914b5dab21eb68dc8e7f013f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62467245"
---
# <a name="restore-and-recovery-of-memory-optimized-tables"></a>Ripristinare e recuperare tabelle con ottimizzazione per la memoria
  Il meccanismo di base per recuperare o ripristinare un database con tabelle ottimizzate per la memoria è simile a quello per i database che hanno solo tabelle basate su disco. A differenza delle tabelle basate su disco, le tabelle ottimizzate per la memoria devono essere caricate in memoria prima di rendere disponibile il database per l'accesso utente. Si tratta di un nuovo passaggio nel processo di recupero del database. I passaggi modificati per il recupero del database sono cambiati come indicato di seguito:  
  
 Al riavvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ogni database attraversa una fase di recupero suddivisa in tre parti:  
  
1.  Fase di analisi. Durante questa fase, viene eseguito un passaggio nei log delle transazioni attivi per rilevare le transazioni di cui è stato eseguito il commit e di cui non è stato eseguito il commit. Il motore OLTP in memoria identifica il checkpoint per caricare e precaricare le voci di log della tabella di sistema. Elabora inoltre alcuni record di log delle allocazioni di file.  
  
2.  Fase di rollforward. Questa fase viene eseguita contemporaneamente sia nelle tabelle basate su disco sia in quelle ottimizzate per la memoria.  
  
     Per le tabelle basate su disco, il database viene spostato al momento corrente e acquisisce i blocchi utilizzati dalle transazioni di cui non è stato eseguito il commit.  
  
     Per le tabelle ottimizzate per la memoria, i dati dalle coppie di file di dati e differenziali vengono caricati in memoria e aggiornati con il log delle transazioni attivo basato sull'ultimo checkpoint durevole.  
  
     Quando vengono completate le operazioni riportate sopra per le tabelle basate su disco e le tabelle ottimizzate per la memoria, il database è disponibile per l'accesso.  
  
3.  Fase di rollback. In questa fase, viene effettuato il rollback delle transazioni di cui non è stato eseguito il commit.  
  
 Il caricamento delle tabelle ottimizzate per la memoria può influire sul tempo necessario per il pieno recupero dell'operatività (RTO, Recovery Time Objective). Per migliorare il tempo di caricamento dei dati ottimizzati per la memoria dai file di dati e differenziali, il motore OLTP in memoria carica i file di dati e differenziali in parallelo nel modo seguente:  
  
-   Creazione di un filtro mappa differenziale. I file differenziali archiviano i riferimenti alle righe eliminate. Un thread per contenitore legge i file differenziali e crea un filtro mappa differenziale. In un filegroup di dati con ottimizzazione per la memoria possono essere presenti più contenitori.  
  
-   Flusso dei file di dati.  Alla creazione del filtro mappa differenziale, i file di dati vengono letti utilizzando un numero di thread equivalente al numero di CPU logiche. Ogni thread che legge il file di dati legge le righe di dati, controlla la mappa differenziale associata e inserisce la riga nella tabella solo se tale riga non è stata contrassegnata come eliminata. Questa parte del recupero può essere associata alla CPU in alcuni casi riportati di seguito.  
  
 ![Tabelle con ottimizzazione per la memoria.](../../database-engine/media/memory-optimized-tables.gif "Tabelle con ottimizzazione per la memoria.")  
  
 Le tabelle con ottimizzazione per la memoria possono in genere essere caricate in memoria alla velocità di I/O, ma in alcuni casi il caricamento delle righe di dati in memoria è più lento. Alcuni casi specifici sono i seguenti:  
  
-   Un numero di bucket basso per l'indice hash può portare a conflitti eccessivi rallentando gli inserimenti delle righe di dati. Ciò comporta in genere un utilizzo elevato della CPU per l'intero processo, in particolare verso la fine del recupero. Se l'indice hash è stato configurato correttamente, non dovrebbe influire sul tempo di recupero.  
  
-   L'utilizzo della CPU può risultare elevato per le tabelle ottimizzate per la memoria di grandi dimensioni con uno o più indici non cluster in quanto, a differenza di un indice hash in cui il numero di bucket è stabilito al momento della creazione, gli indici non cluster aumentano in modo dinamico.  
  
## <a name="restoring-a-database-with-memory-optimized-tables"></a>Ripristino di un database con tabelle con ottimizzazione per la memoria  
 Si sa che è disponibile memoria sufficiente nel server per ripristinare un database, ma è necessario che la memoria richiesta dal database venga calcolata come parte di un pool di risorse esistente.  Si sa che non è possibile creare l'associazione al pool di risorse prima che il database sia disponibile, quindi si esegue il ripristino con l'opzione RESTORE WITH RECOVERY.  In questo modo, l'immagine disco del database viene ripristinata e il database viene creato, ma non viene usata memoria OLTP in memoria in quanto il database non viene portato online.  
  
 A questo punto, è possibile creare il pool di risorse per l'associazione del database e quindi usare RESTORE WITH RECOVERY per portare online il database ripristinato.  Poiché l'associazione è disponibile prima che il database venga portato online, l'utilizzo della memoria OLTP in memoria viene calcolato correttamente. Ciò richiede che il database venga ripristinato una sola volta. Il primo comando RESTORE è un comando informativo che legge solo l'intestazione del backup, mentre l'ultimo comando attiva semplicemente il ripristino senza effettivamente ripristinare alcun bit.  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire il backup, ripristinare e recuperare tabelle con ottimizzazione per la memoria](memory-optimized-tables.md)  
  
  
