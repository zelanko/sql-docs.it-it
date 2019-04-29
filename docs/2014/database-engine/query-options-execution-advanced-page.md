---
title: Opzioni di query esecuzione (pagina avanzata) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.query.advanced.f1
ms.assetid: 661595ce-99b9-4316-ad80-ed04002d04d5
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 7c598ca2dc2e1fd79e221c0c3d3fc1a5c3592dcb
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62844172"
---
# <a name="query-options-execution-advanced-page"></a>Esecuzione di Opzioni query (pagina Avanzate)
  L'uso dell'istruzione **SET** rende disponibili numerose opzioni. Usare questa pagina per specificare un'opzione **set** per l'esecuzione di query di Microsoft SQL Server. Per informazioni dettagliate su ogni opzione, vedere la documentazione online di SQL Server.  
  
 **SET NOCOUNT**  
 Non restituisce il conteggio del numero di righe sotto forma di messaggio con il set di risultati. Questa opzione è deselezionata per impostazione predefinita.  
  
 **SET NOEXEC**  
 La query non viene eseguita. Questa opzione è deselezionata per impostazione predefinita.  
  
 **SET PARSEONLY**  
 Consente di verificare la sintassi di ogni query senza eseguire le query. Questa opzione è deselezionata per impostazione predefinita.  
  
 **SET CONCAT_NULL_YIELDS_NULL**  
 Se questa casella di controllo è selezionata, le query che eseguono la concatenazione di un valore esistente con un valore `NULL` restituiscono sempre `NULL` come risultato. Se questa casella di controllo è deselezionata, un valore esistente concatenato con un valore `NULL` restituisce il valore esistente. Questa opzione è selezionata per impostazione predefinita.  
  
 **SET ARITHABORT**  
 Se questa casella di controllo è selezionata, quando un'istruzione `INSERT`, `DELETE` o `UPDATE` incontra un errore aritmetico (overflow, divisione per zero o errore di dominio) durante la valutazione dell'espressione, la query o il batch viene terminato. Se questa casella di controllo è deselezionata, viene fornito un valore `NULL` per quel valore, se possibile, l'esecuzione della query continua e nel risultato viene incluso un messaggio. Per ulteriori informazioni sull'argomento, vedere la documentazione online. Questa opzione è selezionata per impostazione predefinita.  
  
 **SET SHOWPLAN_TEXT**  
 Quando questa casella di controllo è selezionata, il piano di query viene restituito in formato testo per ogni query. Questa opzione è deselezionata per impostazione predefinita.  
  
 **SET STATISTICS TIME**  
 Se questa casella di controllo è selezionata, le statistiche temporali vengono restituite con ogni query. Questa opzione è deselezionata per impostazione predefinita.  
  
 **SET STATISTICS IO**  
 Se questa casella di controllo è selezionata, le statistiche di input/output (I/O) vengono restituite con ogni query. Questa opzione è deselezionata per impostazione predefinita.  
  
 **SET TRANSACTION ISOLATION LEVEL**  
 Il livello di isolamento delle transazioni READ COMMITTED è impostato per impostazione predefinita. Per altre informazioni, vedere [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql). Il livello di isolamento SNAPSHOT non è disponibile. Per utilizzare l'isolamento SNAPSHOT, aggiungere l'istruzione [!INCLUDE[tsql](../includes/tsql-md.md)] seguente:  
  
```  
SET TRANSACTION ISOLATION LEVEL SNAPSHOT;  
GO  
```  
  
 **IMPOSTARE LA PRIORITÀ DI DEADLOCK**  
 Il valore predefinito **Normale** consente a ogni query di avere la stessa priorità quando si verifica un deadlock. Selezionare la priorità Bassa nell'elenco a discesa se si desidera che la query specifica ignori gli eventuali conflitti con deadlock e che sia possibile selezionarla come query da terminare.  
  
 **IMPOSTARE IL TIMEOUT DEL BLOCCO**  
 Il valore predefinito -1 indica che i blocchi vengono mantenuti fino al completamento delle transazioni. Un valore uguale a 0 significa nessuna attesa e che non appena viene incontrato un blocco viene visualizzato un messaggio. Specificare un valore maggiore di 0 millisecondi per terminare una transazione se i blocchi delle transazioni devono essere mantenuti per un periodo di tempo superiore rispetto al tempo specificato.  
  
 **SET QUERY_GOVERNOR_COST_LIMIT**  
 L'opzione **Limite di costo di Query Governor** consente di specificare un limite di tempo massimo per l'esecuzione di una query. Il costo della query equivale al tempo trascorso (in secondi) stimato per l'esecuzione di una query in una configurazione hardware specifica. Il valore predefinito 0 indica che non esistono limiti all'estensione di tempo per l'esecuzione di una query.  
  
 **Non visualizzare intestazioni messaggi provider**  
 Se questa casella di controllo è selezionata, i messaggi di stato provenienti dal provider, ad esempio il provider OLE DB, non vengono visualizzati. Questa casella di controllo è selezionata per impostazione predefinita. Deselezionare questa casella di controllo per visualizzare i messaggi del provider durante la risoluzione dei problemi relativi alle query che potrebbero essersi verificati a livello del provider.  
  
 **Disconnetti al termine dell'esecuzione della query**  
 Quando questa casella di controllo è selezionata, la connessione a SQL Server viene terminata dopo il completamento della query. Questa opzione è deselezionata per impostazione predefinita.  
  
 **Ripristina predefiniti**  
 Reimposta le impostazioni predefinite originali per tutti i valori nella pagina.  
  
  
