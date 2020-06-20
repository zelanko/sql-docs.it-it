---
title: Definizione di durabilità per gli oggetti con ottimizzazione per la memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 0fe85fbf-8e8d-4983-96fd-d04b3c7d6d65
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: caae904bc1e25288e81d3baba21719be28c05d31
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85050234"
---
# <a name="defining-durability-for-memory-optimized-objects"></a>Definizione di durabilità per gli oggetti con ottimizzazione per la memoria
  Con OLTP in memoria viene garantita la disponibilità completa di tutte le proprietà di atomicità, coerenza, isolamento e durabilità (ACID, Atomicity, Consistency, Isolation, Durability). La durabilità, nel contesto di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e delle tabelle ottimizzate per la memoria, offre le seguenti garanzie:  
  
 Durabilità delle transazioni  
 Quando si esegue il commit di una transazione completamente durevole che ha apportato modifiche (DML o DDL) a una tabella ottimizzata per la memoria, le modifiche apportate a una tabella durevole ottimizzata per la memoria vengono rese permanenti.  
  
 Quando si esegue il commit di una transazione durevole posticipata a una tabella ottimizzata per la memoria, la transazione diventa durevole solo dopo che il log delle transazioni in memoria viene salvato su disco.  
  
 Durabilità al riavvio  
 Quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene riavviato dopo un arresto anomalo o pianificato, viene ricreata un'istanza delle tabelle durevoli ottimizzate per la memoria per ripristinarne lo stato precedente all'arresto anomalo o pianificato.  
  
 Durabilità in caso di errori dei supporti  
 Se in un disco guasto o danneggiato sono presenti una o più copie persistenti di oggetti durevoli ottimizzati per la memoria, la funzionalità di backup e ripristino di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] consente di ripristinare le tabelle ottimizzate per la memoria sul nuovo supporto.  
  
 Per le tabelle ottimizzate per la memoria sono disponibili due opzioni di durabilità:  
  
 SCHEMA_ONLY (tabella non durevole)  
 Questa opzione assicura la durabilità dello schema della tabella, inclusi gli indici. Quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene riavviato, la tabella non durevole viene ricreata, ma inizialmente senza dati. Si tratta di un comportamento diverso da una tabella in tempdb, in cui sia la tabella che i dati vengono persi al riavvio. Uno scenario tipico per creare una tabella non durevole consiste nell'archiviare dati temporanei, ad esempio una tabella di staging per un processo ETL. Una durabilità SCHEMA_ONLY evita la registrazione delle transazioni e i checkpoint, con una possibile riduzione significativa delle operazioni di I/O.  
  
 SCHEMA_AND_DATA (tabella durevole)  
 Questa opzione offre durabilità dello schema e dei dati. Il livello di durabilità dei dati dipende dall'eventuale scelta di eseguire il commit di una transazione come completamente durevole o con durabilità posticipata. Le transazioni completamente durevoli offrono la stessa garanzia di durabilità dei dati e dello schema, in modo analogo a una tabella basata su disco. La durabilità posticipata migliora le prestazioni ma può causare la perdita di dati in caso di un arresto anomalo del server o di failover. Per altre informazioni sulla durabilità ritardata, vedere [Controllo della durabilità delle transazioni](../logs/control-transaction-durability.md).  
  
 Lo schema della tabella ottimizzata per la memoria viene reso persistente, in modo analogo alle tabelle basate su disco, nel filegroup primario di un database.  
  
 I dati delle tabelle ottimizzate per la memoria vengono salvati in coppie di file di dati e differenziali.  
  
 Gli indici definiti nelle tabelle ottimizzate per la memoria sono persistenti solo nei metadati, non nell'archiviazione. Le strutture degli indici vengono generate nell'ambito del caricamento di tabelle ottimizzate per la memoria.  
  
 Le righe vengono eliminate in modo esplicito tramite un'istruzione DELETE o indirettamente tramite un'istruzione UPDATE. Un'operazione UPDATE viene eseguita come un'eliminazione seguita da un inserimento. Quando viene eliminata una riga, non viene apportata alcuna modifica a un file di dati, ma al file differenziale corrispondente viene accodata una nuova riga che identifica quella eliminata.  
  
 Durante le operazioni di recupero o ripristino, il motore di OLTP in memoria legge i file di dati e differenziali per il caricamento nella memoria fisica. Il tempo di caricamento viene determinato dai seguenti fattori:  
  
-   Quantità di dati da caricare.  
  
-   Larghezza di banda per operazioni di I/O sequenziali.  
  
-   Grado di parallelismo, determinato dal numero di file contenitori e di core del processore.  
  
-   Quantità di record di log nella parte attiva del log che devono essere ripetuti.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione e gestione dell'archiviazione per gli oggetti con ottimizzazione per la memoria](creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
