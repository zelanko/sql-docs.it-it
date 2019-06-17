---
title: Confronto dell'archiviazione delle tabelle basate su disco con quella delle tabelle con ottimizzazione per la memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: eacf443c-001a-445f-ad1c-5f5a45eca6f4
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: be224cdd8c3221f1e7796e15c9c0132aeb99bcd7
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62990665"
---
# <a name="comparing-disk-based-table-storage-to-memory-optimized-table-storage"></a>Confronto dell'archiviazione delle tabelle basate su disco con quella delle tabelle con ottimizzazione per la memoria
  
  
|Categories|Tabella basata su disco|Tabella durevole con ottimizzazione per la memoria|  
|----------------|-----------------------|-------------------------------------|  
|DDL|Le informazioni sui metadati vengono archiviate in tabelle di sistema nel filegroup primario del database e sono accessibili tramite le viste del catalogo.|Le informazioni sui metadati vengono archiviate in tabelle di sistema nel filegroup primario del database e sono accessibili tramite le viste del catalogo.|  
|Struttura|Le righe vengono archiviate in pagine da 8 KB. Una pagina contiene solo righe della stessa tabella.|Le righe vengono archiviate come singole righe. Non è presente alcuna struttura della pagina. Due righe consecutive in un file di dati possono appartenere a tabelle ottimizzate per la memoria diverse.|  
|Indici|Gli indici vengono archiviati in una struttura della pagina simile alle righe di dati.|Solo la definizione dell'indice è persistente (non le righe di indice). Gli indici vengono gestiti in memoria e generati di nuovo quando la tabella ottimizzata per la memoria viene caricata in memoria come parte del riavvio di un database. Poiché le righe di indice non sono persistenti, non viene effettuata alcuna registrazione per le modifiche dell'indice.|  
|Operazione DML|Il primo passaggio consiste nell'individuare la pagina, quindi nel caricarla nel pool di buffer.<br /><br /> Insert<br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la riga viene inserita nella pagina prendendo in considerazione l'ordinamento delle righe in caso di indice cluster.<br /><br /> DELETE<br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene individuata la riga da eliminare nella pagina e viene contrassegnata come eliminata.<br /><br /> Update<br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] viene individuata la riga nella pagina. L'aggiornamento viene eseguito sul posto per le colonne non chiave. L'aggiornamento delle colonne chiave viene eseguito tramite un'operazione di eliminazione e inserimento.<br /><br /> Una volta completata l'operazione DML, le pagine modificate vengono scaricate su disco come parte dei criteri del pool di buffer, del checkpoint o del commit della transazione per le operazioni con registrazione minima. Sia le operazioni di lettura sia quelle di scrittura nelle pagine comportano attività di I/O non necessaria.|Per le tabelle ottimizzate per la memoria, poiché i dati risiedono in memoria, le operazioni DML vengono eseguite direttamente in memoria. È disponibile un thread in background che legge i record del log per le tabelle ottimizzate per la memoria e li salva in modo persistente nei file di dati e differenziali. Un aggiornamento genera una nuova versione di riga, tuttavia viene registrato come un'eliminazione seguita da un inserimento.|  
|Frammentazione dei dati|La manipolazione dei dati ne comporta la frammentazione che produce pagine riempite parzialmente e pagine logicamente consecutive che non sono contigue su disco. Ciò comporta una riduzione delle prestazioni di accesso ai dati e ne richiede la deframmentazione.|I dati con ottimizzazione per la memoria non vengono archiviati in pagine, pertanto non vengono frammentati. Poiché tuttavia le righe vengono aggiornate ed eliminate, i file di dati e differenziali devono essere compressi. Questa operazione viene eseguita da un thread MERGE in background in base ai criteri di unione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione e gestione dell'archiviazione per gli oggetti con ottimizzazione per la memoria](creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
