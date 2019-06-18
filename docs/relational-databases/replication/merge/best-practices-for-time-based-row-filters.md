---
title: Procedure consigliate per i filtri di riga basati sul tempo
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- best practices
ms.assetid: 773c5c62-fd44-44ab-9c6b-4257dbf8ffdb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 3a2b86b5f9b08e9915adae27132b6beb5647394f
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62639313"
---
# <a name="best-practices-for-time-based-row-filters"></a>Procedure consigliate per i filtri di riga basati sul tempo
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Gli utenti delle applicazioni hanno spesso la necessità di recuperare da diverse tabelle determinati subset di dati basati sul tempo. Un venditore potrebbe ad esempio richiedere i dati relativi agli ordini dell'ultima settimana, così come un responsabile della pianificazione di eventi potrebbe aver bisogno di recuperare i dati relativi agli eventi della settimana in arrivo. Per soddisfare queste richieste, le applicazioni utilizzano, in numerosi casi, query contenenti la funzione **GETDATE()** . Si consideri l'istruzione di filtro di riga seguente:  
  
```  
WHERE SalesPersonID = CONVERT(INT,HOST_NAME()) AND OrderDate >= (GETDATE()-6)  
```  
  
 Con un filtro di questo tipo, l'esecuzione dell'agente di merge ha in genere due risultati: le righe che soddisfano il filtro vengono replicate nei Sottoscrittori, mentre le righe che non soddisfano più il filtro vengono rimosse dai Sottoscrittori. Per altre informazioni sulle opzioni di filtro con **HOST_NAME()** , vedere [Filtri di riga con parametri](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md). La replica di tipo merge, tuttavia, consente di replicare e pulire esclusivamente i dati che sono stati modificati dopo l'ultima sincronizzazione, indipendentemente dalla modalità di definizione di un filtro di riga per tali dati.  
  
 Affinché la replica di tipo merge elabori una riga, è necessario che i dati contenuti in tale riga soddisfino il filtro di riga e che siano stati modificati dopo l'ultima sincronizzazione. Nel caso della tabella **SalesOrderHeader** , **OrderDate** viene immesso quando si inserisce una riga. Le righe vengono quindi replicate nel Sottoscrittore come previsto poiché l'inserimento rappresenta una modifica ai dati. Se tuttavia nel Sottoscrittore sono presenti righe che non soddisfano più il filtro, ovvero sono relative a ordini immessi da più di sette giorni, queste verranno rimosse dal Sottoscrittore a meno che non siano state aggiornate per altri motivi.  
  
 L'esempio del responsabile della pianificazione di eventi evidenzia ulteriormente il problema legato a questo tipo di filtro. Si consideri di utilizzare il filtro seguente per una tabella **Events** :  
  
```  
WHERE EventCoordID = CONVERT(INT,HOST_NAME()) AND EventDate <= (GETDATE()+6)  
```  
  
 Per una tabella contenente eventi, gli inserimenti potrebbero essere eseguiti molto prima della data dell'evento. Se un mese prima è stato eseguito un inserimento per un evento della settimana successiva a quella corrente, senza che sia stata aggiornata la riga, quest'ultima non verrà replicata nel Sottoscrittore, anche se soddisfa il filtro di riga.  
  
 A seconda inoltre della configurazione della pubblicazione, la replica di tipo merge valuta i filtri in momenti diversi:  
  
-   Se una pubblicazione utilizza partizioni pre-calcolate, in base all'impostazione predefinita, i filtri vengono valutati ad ogni inserimento o aggiornamento di una riga.  
  
-   Se la pubblicazione non utilizza partizioni pre-calcolate, i filtri vengono valutati durante l'esecuzione dell'agente di merge.  
  
 Per altre informazioni sulle partizioni pre-calcolate, vedere [Ottimizzare le prestazioni dei filtri con parametri con le partizioni pre-calcolate](../../../relational-databases/replication/merge/parameterized-filters-optimize-for-precomputed-partitions.md). A seconda del momento in cui viene valutato il filtro, il tipo di dati che lo soddisfa sarà diverso. Se ad esempio una pubblicazione utilizza partizioni pre-calcolate e i dati vengono sincronizzati ogni due giorni, il subset di dati per il venditore potrebbe includere righe che risalgono fino a due giorni prima del previsto.  
  
## <a name="recommendations-for-using-time-based-row-filters"></a>Indicazioni sull'utilizzo dei filtri di riga basati sul tempo  
 Il metodo seguente offre un approccio semplice ed efficace per il filtraggio basato sul tempo:  
  
-   Aggiungere alla tabella una colonna del tipo di dati **bit**. Questa colonna indica se è necessario replicare una riga.  
  
-   Utilizzare un filtro di riga che fa riferimento alla nuova colonna, anziché a una colonna basata sul tempo.  
  
-   Creare un processo di SQL Server Agent, o un processo pianificato tramite un altro meccanismo, per aggiornare la colonna prima dell'avvio pianificato dell'agente di merge.  
  
 Questo approccio consente di superare i limiti del metodo **GETDATE()** o di altri metodi basati sul tempo e di evitare il problema di determinare il momento della valutazione dei filtri per le partizioni. Si consideri la tabella **Events** seguente:  
  
|**EventID**|**EventName**|**EventCoordID**|**EventDate**|**Replica**|  
|-----------------|-------------------|----------------------|-------------------|-------------------|  
|1|Reception|112|2006-10-04|1|  
|2|Pranzo|112|2006-10-10|0|  
|3|Party|112|2006-10-11|0|  
|4|Matrimonio|112|2006-10-12|0|  
  
 Il filtro di riga di questa tabella avrebbe quindi l'aspetto seguente:  
  
```  
WHERE EventCoordID = CONVERT(INT,HOST_NAME()) AND Replicate = 1  
```  
  
 Il processo di SQL Server Agent può eseguire istruzioni [!INCLUDE[tsql](../../../includes/tsql-md.md)] simili alle seguenti prima dell'esecuzione di ogni agente di merge:  
  
```  
UPDATE Events SET Replicate = 0 WHERE Replicate = 1  
GO  
UPDATE Events SET Replicate = 1 WHERE EventDate <= GETDATE()+6  
GO  
```  
  
 La prima riga reimposta la colonna **Replicate** su **0**, mentre la seconda riga imposta la colonna su **1** per gli eventi che avranno luogo nei sette giorni successivi. Se questa istruzione [!INCLUDE[tsql](../../../includes/tsql-md.md)] viene eseguita il 07/10/2006, la tabella verrà aggiornata nel modo seguente:  
  
|**EventID**|**EventName**|**EventCoordID**|**EventDate**|**Replica**|  
|-----------------|-------------------|----------------------|-------------------|-------------------|  
|1|Reception|112|2006-10-04|0|  
|2|Pranzo|112|2006-10-10|1|  
|3|Party|112|2006-10-11|1|  
|4|Matrimonio|112|2006-10-12|1|  
  
 Gli eventi della settimana successiva sono ora contrassegnati come pronti per la replica. Alla successiva esecuzione dell'agente di merge per la sottoscrizione utilizzata dal coordinatore di eventi 112, le righe 2, 3 e 4 verranno scaricate nel Sottoscrittore e la riga 1 verrà rimossa dal Sottoscrittore.  
  
## <a name="see-also"></a>Vedere anche  
 [GETDATE &#40;Transact-SQL&#41;](../../../t-sql/functions/getdate-transact-sql.md)   
 [Implementare processi](../../../ssms/agent/implement-jobs.md)   
 [Filtri di riga con parametri](../../../relational-databases/replication/merge/parameterized-filters-parameterized-row-filters.md)  
  
  
