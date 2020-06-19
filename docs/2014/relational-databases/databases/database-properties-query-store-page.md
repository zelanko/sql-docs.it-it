---
title: Proprietà database (pagina Archivio query) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql13.swb.databaseproperties.querystore.f1
ms.assetid: da47d75e-291a-4305-acef-4b0aaf5215da
author: stevestein
ms.author: sstein
ms.openlocfilehash: bab0d9b697e9ad9ec4b27f320d26b9b9edb5944e
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84970121"
---
# <a name="database-properties-query-store-page"></a>Proprietà database (pagina Archivio query)
  Accedere a questa pagina dal database principale e usarla per configurare e modificare le proprietà dell'archivio query del database. È anche possibile configurare queste opzioni con le [opzioni ALTER DATABASE SET](/sql/t-sql/statements/alter-database-transact-sql-set-options). Per informazioni sull'archivio query, vedere [Monitoring Performance By Using the Query Store](../performance/monitoring-performance-by-using-the-query-store.md).  
  
||  
|-|  
|**Si applica a**: [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].|  
  
## <a name="options"></a>Opzioni  
 Abilitare  
 Abilita e disabilita l'archivio query.  
  
 Modalità operativa  
 I valori validi sono READ_ONLY e READ_WRITE. In modalità READ_WRITE l'archivio query raccoglie e mantiene le informazioni di statistiche sull'esecuzione di runtime e piani di query. In modalità READ_ONLY le informazioni possono essere lette dall'archivio query, ma non vengono aggiunte nuove informazioni. Se lo spazio massimo allocato dell'archivio query è esaurito, la modalità operativa dell'archivio query passa a READ_ONLY.  
  
 Modalità operativa (effettiva)  
 Ottiene la modalità operativa effettiva dell'archivio query.  
  
 Modalità operativa (richiesta)  
 Ottiene e imposta la modalità operativa desiderata dell'archivio query.  
  
 Intervallo di scaricamento dati (minuti)  
 Determina la frequenza con cui i dati scritti nell'archivio query vengono mantenuti su disco. Per ottimizzare le prestazioni, i dati raccolti dall'archivio query vengono scritti in modo asincrono sul disco. La frequenza con cui si verifica questo trasferimento asincrono è configurabile.  
  
 Intervallo di raccolta statistiche  
 Ottiene e imposta il valore dell'intervallo di raccolta delle statistiche.  
  
 Dimensioni massime (MB)  
 Ottiene e imposta lo spazio totale allocato all'archivio query.  
  
 Soglia per query non aggiornate (giorni)  
 Ottiene e imposta la soglia per query non aggiornate. Configurare l'argomento STALE_QUERY_THRESHOLD_DAYS per specificare il numero di giorni per la conservazione dei dati nell'archivio query.  
  
 Elimina dati query  
 Rimuove il contenuto dell'archivio query.  
  
 Grafici a torta  
 Il grafico a sinistra illustra l'utilizzo totale del file di database sul disco e la parte del file occupata dai dati dell'archivio query.  
  
 Il grafico a destra illustra la parte della quota dell'archivio query attualmente utilizzata. Si noti che la quota non è visualizzata nel grafico a sinistra e può superare le dimensioni correnti del database.  
  
## <a name="remarks"></a>Commenti  
 La funzionalità dell'archivio query mette a disposizione degli amministratori di database informazioni dettagliate sulle prestazioni e sulla scelta del piano di query. Semplifica la risoluzione dei problemi in quanto consente di individuare rapidamente le variazioni delle prestazioni causate da modifiche nei piani di query. La funzionalità acquisisce automaticamente una cronologia delle query, dei piani e delle statistiche di runtime e li conserva in modo che sia possibile esaminarli successivamente. I dati vengono separati dagli intervalli di tempo, consentendo di visualizzare i modelli di utilizzo del database e capire quando sono state apportate modifiche al piano di query nel server. Per configurare l'archivio query, si può usare questa pagina delle proprietà del database dell'archivio query oppure l'opzione [ALTER DATABASE SET](/sql/t-sql/statements/alter-database-transact-sql-set-options) . Per presentare le informazioni, nell'archivio query viene usata una finestra di dialogo di [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] . Per altre informazioni sull'archivio query, vedere [Monitoring Performance By Using the Query Store](../performance/monitoring-performance-by-using-the-query-store.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure di Query Store &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/query-store-stored-procedures-transact-sql)   
 [Viste del catalogo di Archivio query &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/query-store-catalog-views-transact-sql)  
  
  
