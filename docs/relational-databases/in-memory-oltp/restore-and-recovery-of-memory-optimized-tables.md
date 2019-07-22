---
title: Ripristino e recupero di tabelle ottimizzate per la memoria | Microsoft Docs
ms.custom: ''
ms.date: 12/31/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 294975b7-e7d1-491b-b66a-fdb1100d2acc
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 10a54ea4326c3fb3c1a9400568ac9aa7e904aa2d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68111796"
---
# <a name="restore-and-recovery-of-memory-optimized-tables"></a>Ripristino e recupero di tabelle ottimizzate per la memoria
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Il meccanismo di base per recuperare o ripristinare un database che usa tabelle ottimizzate per la memoria è simile a quello per un database che usa solo tabelle basate su disco. Ma a differenza delle tabelle basate su disco, per rendere disponibile il database per l'accesso dell'utente, le tabelle ottimizzate per la memoria devono essere prima caricate in memoria. Questo requisito aggiunge un nuovo passaggio nel processo di recupero del database.  
  
Se la memoria disponibile nel server non è sufficiente, il recupero del database ha esito negativo e il database viene contrassegnato come sospetto. Per risolvere questo problema, vedere [Risolvere i problemi di memoria insufficiente](resolve-out-of-memory-issues.md). 
  
## <a name="factors-that-affect-load-time"></a>Fattori che influiscono sul tempo di caricamento
Durante le operazioni di recupero o ripristino, il motore di OLTP in memoria legge i file di dati e differenziali per il caricamento nella memoria fisica. Il tempo di caricamento viene determinato dai seguenti fattori:  
  
-   Quantità di dati da caricare.  
  
-   Larghezza di banda per operazioni di I/O sequenziali.  
  
-   Grado di parallelismo, determinato dal numero di contenitori di file e core del processore.  
  
-   Numero di record di log nella parte attiva del log di cui è necessario eseguire il rollforward.  

## <a name="phases-of-recovery"></a>Fasi di recupero
Al riavvio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ogni database viene sottoposto a un processo di recupero costituito da tre fasi:  
  
1.  **Analisi**. In questa fase viene eseguito un passaggio nei log delle transazioni attivi per rilevare le transazioni di cui è stato eseguito il commit e di cui non è stato eseguito il commit. Il motore OLTP in memoria identifica il checkpoint per caricare e precaricare le voci di log della tabella di sistema. Elabora inoltre alcuni record di log delle allocazioni di file.  
  
2.  **Rollforward**. Questa fase viene eseguita contemporaneamente sia nelle tabelle basate su disco sia in quelle ottimizzate per la memoria.  
  
    - Per le tabelle basate su disco, il database viene spostato al momento corrente e acquisisce i blocchi utilizzati dalle transazioni di cui non è stato eseguito il commit.  
  
    - Per le tabelle ottimizzate per la memoria, i dati delle coppie di file di dati e differenziali vengono caricati in memoria. I dati vengono quindi aggiornati con il log delle transazioni attivo in base all'ultimo checkpoint durevole.  
  
    Al termine delle operazioni appena descritte sulle tabelle basate su disco e su quelle ottimizzate per la memoria, il database è disponibile per l'accesso.  
  
3.  **Rollback**. In questa fase, viene effettuato il rollback delle transazioni di cui non è stato eseguito il commit.  

[!INCLUDE[freshInclude](../../includes/paragraph-content/fresh-note-steps-feedback.md)]

## <a name="process-for-improving-load-time"></a>Processo per migliorare il tempo di caricamento
Il caricamento delle tabelle ottimizzate per la memoria può influire sul tempo necessario per il pieno recupero dell'operatività (RTO, Recovery Time Objective). Per migliorare il tempo di caricamento dei dati ottimizzati per la memoria dai file di dati e differenziali, il motore OLTP in memoria carica i file di dati e differenziali in parallelo nel modo seguente:  
  
-   **Creazione di un filtro mappa differenziale**. I file differenziali archiviano i riferimenti alle righe eliminate. Un thread per contenitore legge i file differenziali e crea un filtro mappa differenziale. In un filegroup di dati ottimizzato per la memoria possono essere presenti più contenitori.  
  
-   **Flusso dei file di dati**. Dopo la creazione del filtro mappa differenziale, i file di dati vengono letti da un numero di thread equivalente al numero di CPU logiche. Ogni thread legge le righe di dati, controlla la mappa differenziale associata e inserisce una riga nella tabella solo se la riga non è stata contrassegnata come eliminata. In alcuni casi questa parte del recupero può essere basata sulla CPU, come illustrato in questo diagramma:  
  
    ![Flusso dei dati alle tabelle ottimizzate per la memoria](../../relational-databases/in-memory-oltp/media/memory-optimized-tables.gif "Flusso dei dati alle tabelle ottimizzate per la memoria")  
  
## <a name="specific-cases-of-slow-load-times"></a>Casi specifici di tempi di caricamento lenti
Le tabelle ottimizzate per la memoria possono in genere essere caricate in memoria alla velocità di I/O, ma il caricamento delle righe di dati in memoria è talvolta più lento. Alcuni casi specifici sono i seguenti:  
  
-   Un numero di bucket ridotto per un indice hash può determinare una collisione eccessiva rallentando gli inserimenti delle righe di dati. Ciò comporta in genere un uso elevato della CPU per l'intero processo, in particolare verso la fine del recupero. Se l'indice hash è stato configurato correttamente, non dovrebbe influire sul tempo di recupero.  
  
-   Tabelle ottimizzate per la memoria di grandi dimensioni con uno o più indici non cluster possono determinare un uso elevato della CPU. A differenza di un indice hash, il cui numero di bucket viene stabilito al momento della creazione, le dimensioni degli indici non cluster aumentano in modo dinamico.  
  
## <a name="see-also"></a>Vedere anche  
 [Eseguire il backup, ripristinare e recuperare tabelle con ottimizzazione per la memoria](https://msdn.microsoft.com/library/3f083347-0fbb-4b19-a6fb-1818d545e281)  
  
  
