---
title: Stima della cardinalità (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 11/24/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- cardinality estimator
- CE (cardinality estimator)
- estimating cardinality
ms.assetid: baa8a304-5713-4cfe-a699-345e819ce6df
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: f7c3f609bd2b25fcb3e3553497ead2baad476f2f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63151038"
---
# <a name="cardinality-estimation-sql-server"></a>Stima della cardinalità (SQL Server)
  La logica di stima della cardinalità, denominata strumento di stima della cardinalità, è stata riprogettata in [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] per migliorare la qualità dei piani di query e, di conseguenza, per ottimizzare le prestazioni delle query. Nel nuovo strumento di stima della cardinalità sono incorporati presupposti e algoritmi maggiormente adatti ai i carichi di lavoro di data warehouse e alle soluzioni OLTP più recenti. Lo strumento è basato sulla ricerca approfondita della stima della cardinalità sui carichi di lavoro più recenti e sulle conoscenze relative al miglioramento della stima della cardinalità di SQL Server acquisite nel corso degli ultimi 15 anni. I commenti e i suggerimenti dei clienti indicano che sebbene la maggior parte delle query registrerà un miglioramento o rimarrà invariata a seguito della modifica, una percentuale minima potrebbe registrare una regressione rispetto allo strumento di stima della cardinalità precedente.  
  
> [!NOTE]  
>  Le stime della cardinalità sono una stima del numero di righe nel risultato della query. Query Optimizer usa queste stime per scegliere un piano per l'esecuzione della query. La qualità del piano di query influisce direttamente sul miglioramento delle prestazioni della query.  
  
## <a name="performance-testing-and-tuning-recommendations"></a>Indicazioni per il test e l'ottimizzazione delle prestazioni  
 Il nuovo strumento di stima della cardinalità è abilitato per tutti i nuovi database creati in [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]. Tuttavia, l'aggiornamento a [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] non abilita il nuovo strumento di stima della cardinalità sui database esistenti.  
  
 Per garantire le prestazioni ottimali per le query, fare riferimento alle indicazioni riportate di seguito per testare il carico di lavoro con il nuovo strumento di stima della cardinalità prima di abilitarlo nel sistema di produzione.  
  
1.  Aggiornare tutti i database esistenti per l'uso del nuovo strumento di stima della cardinalità. A questo scopo, usare [livello di compatibilità ALTER DATABASE &#40;Transact-SQL&#41; ](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level) per impostare il livello di compatibilità del database su 120.  
  
2.  Eseguire il carico di lavoro di prova con il nuovo strumento di stima della cardinalità e quindi risolvere gli eventuali nuovi problemi relativi alle prestazioni adottando le attuali procedure per la risoluzione dei problemi.  
  
3.  Quando il carico di lavoro è in esecuzione con il nuovo strumento di stima della cardinalità (con livello di compatibilità del database impostato su 120 in SQL Server 2014) e le prestazioni di una query specifica registrano una regressione, è possibile eseguire la query con il flag di traccia 9481 per usare la versione dello strumento di stima della cardinalità usato in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e versioni precedenti. Per eseguire una query con un flag di traccia, vedere l'articolo della Knowledge Base relativo all' [abilitazione del comportamento di SQL Server Query Optimizer con effetto sul piano che può essere controllato da flag di traccia diversi al livello della query specifica](https://support.microsoft.com/kb/2801413).  
  
4.  Se non è possibile modificare tutti i database in una sola volta per usare la nuova stima di cardinalità, è possibile usare lo strumento di stima della cardinalità precedente per tutti i database usando [livello di compatibilità ALTER DATABASE &#40;Transact-SQL&#41; ](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level) a impostare il livello di compatibilità del database su 110.  
  
5.  Se il carico di lavoro è in esecuzione con il livello di compatibilità del database impostato su 110 e si vuole verificare o eseguire una query specifica con il nuovo strumento di stima della cardinalità, è possibile eseguire la query con il flag di traccia 2312 per usare la versione di tale strumento inclusa in SQL Server 2014.  Per eseguire una query con un flag di traccia, vedere l'articolo della Knowledge Base relativo all' [abilitazione del comportamento di SQL Server Query Optimizer con effetto sul piano che può essere controllato da flag di traccia diversi al livello della query specifica](https://support.microsoft.com/kb/2801413).  
  
## <a name="new-xevents"></a>Nuovi XEvent  
 Sono disponibili due nuovi XEvent query_optimizer_estimate_cardinality per supportare i nuovi piani di query.  
  
-   *query_optimizer_estimate_cardinality* si verifica quando Query Optimizer stima la cardinalità in un'espressione relazionale.  
  
-   *query_optimizer_force_both_cardinality_estimation*_behaviors si verifica quando entrambi i flag di traccia 2312 e 9481 sono abilitati e tentano di forzare contemporaneamente sia il comportamento precedente della stima della cardinalità sia quello nuovo.  
  
## <a name="examples"></a>Esempi  
 Negli esempi seguenti sono illustrate alcune delle modifiche introdotte nelle nuove stime della cardinalità. Il codice per la stima della cardinalità è stato riscritto. La logica è complessa e non è possibile fornire un elenco completo di tutte le modifiche.  
  
> [!NOTE]  
>  Questi esempi sono forniti a titolo di informazioni concettuali. All'utente non è richiesta alcuna modifica rispetto alla modalità di progettazione di database e query.  
  
### <a name="example-a-new-cardinality-estimates-use-an-average-cardinality-for-recently-added-ascending-data"></a>Esempio A. Le nuove stime della cardinalità usano una cardinalità media per i dati in ordine crescente aggiunti di recente.  
 Questo esempio illustra come il nuovo strumento di stima della cardinalità può migliorare le stime della cardinalità per i dati in ordine crescente che superano il valore massimo nella tabella durante l'aggiornamento delle statistiche più recente.  
  
```  
SELECT item, category, amount FROM dbo.Sales AS s WHERE Date = '2013-12-19';  
```  
  
 In questo esempio, le nuove righe vengono aggiunte alla tabella Sales ogni giorno, la query richiede le vendite eseguite in data 19/12/2013 e l'ultimo aggiornamento delle statistiche è stato effettuato in data 18/12/2013. Lo strumento di stima della cardinalità precedente presuppone che i valori relativi al 19/12/2013 non esistano poiché la data supera la data massima e le statistiche non sono state aggiornate per includere i valori del 19/12/2013. Questa situazione, nota come problema della chiave crescente, si verificherà se si caricano dati durante il giorno e quindi si eseguono query sui dati prima che le statistiche vengano aggiornate.  
  
 Questo comportamento è stato modificato. Ora, anche se le statistiche non sono state aggiornate per i dati crescenti più recenti aggiunti dall'ultimo aggiornamento delle statistiche, il nuovo strumento di stima della cardinalità presuppone che i valori esistano e usa la cardinalità media per ogni valore nella colonna come stima della cardinalità.  
  
### <a name="example-b-new-cardinality-estimates-assume-filtered-predicates-on-the-same-table-have-some-correlation"></a>Esempio B. Le nuove stime della cardinalità presuppongono che i predicati filtrati nella stessa tabella presentino una correlazione.  
 Per questo esempio, si supponga che nella tabella Cars siano presenti 1000 righe, che in Make siano presenti 200 corrispondenze per "Honda", che in Model siano presenti 50 corrispondenze per "Civic" e che tutte le Civic siano Honda. Di conseguenza, il 20% dei valori nella colonna Make sono "Honda", il 5% dei valori nella colonna del modello sono "Civic" e il numero effettivo di Honda Civic è 50. Le stime della cardinalità precedenti presuppongono che i valori nelle colonne Make e Model siano indipendenti gli uni dagli altri. Query optimizer precedente stima che sono presenti 10 Honda Civic (.05 *.20 \* 1000 righe = 10 righe).  
  
```  
SELECT year, purchase_price FROM dbo.Cars WHERE Make = 'Honda' AND Model = 'Civic';  
```  
  
 Questo comportamento è stato modificato. Ora, le nuove stime della cardinalità presuppongono che le colonne Make e Model presentino una *certa* correlazione. Query Optimizer stima una cardinalità più elevata mediante l'aggiunta di un componente esponenziale all'equazione di stima. Query optimizer ora stima che 22,36 righe (.05 * SQRT(.20) \* 1000 righe = 22,36 righe) corrispondono al predicato. Per questo scenario e per la distribuzione di dati specifica, 22,36 righe è un risultato più vicino alle 50 righe che saranno restituite dalla query.  
  
 Si noti che la nuova logica di stima della cardinalità ordina le selettività del predicato e aumenta l'esponente. Ad esempio, se le selettività del predicato.05.20 e.25, la stima della cardinalità sarebbe (.05 * SQRT(.20) \* SQRT(SQRT(.25))).  
  
### <a name="example-c-new-cardinality-estimates-assume-filtered-predicates-on-different-tables-are-independent"></a>Esempio C. Le nuove stime della cardinalità presuppongono che i predicati filtrati in tabelle diverse siano indipendenti.  
 Per questo esempio, lo strumento di stima della cardinalità precedente presuppone che i filtri s.type e r.date del predicato siano correlati. Tuttavia, i risultati di prova sui carichi di lavoro più recenti mostrano che i filtri del predicato sulle colonne in tabelle diverse non sono in genere correlati tra loro.  
  
```  
SELECT s.ticket, s.customer, r.store FROM dbo.Sales AS s CROSS JOIN dbo.Returns AS r  
WHERE s.ticket = r.ticket AND s.type = 'toy' AND r.date = '2013-12-19';  
```  
  
 Questo comportamento è stato modificato. Ora, la nuova logica di stima della cardinalità presuppone che s.type non sia correlato a r.date. In pratica, si presuppone che i giocattoli siano restituiti ogni giorno e non solo in un giorno specifico. In questo caso, le nuove stime della cardinalità restituiranno un numero inferiore rispetto alle stime della cardinalità precedenti.  
  
## <a name="see-also"></a>Vedere anche  
 [Monitoraggio e ottimizzazione delle prestazioni](monitor-and-tune-for-performance.md)  
  
  
