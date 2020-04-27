---
title: 'Opzioni (esecuzione query: SQL Server: pagina Avanzate) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryExecution.SqlServer.SqlExecutionAdvanced
ms.assetid: 3ec788c7-22c3-4216-9ad0-81a168d17074
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 5323054b77ed26a3ada816f44c1bf6764ded931d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "66089367"
---
# <a name="options-query-executionsql-serveradvanced-page"></a>Opzioni (Esecuzione query/SQL Server/pagina Avanzate)
  Utilizzando il comando SET sono disponibili numerose opzioni. Usare questa pagina per specificare un'opzione **set** per l'esecuzione di query di [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] nell'editor di query di SQL Server. Le opzioni non hanno avranno alcun effetto su altri editor del codice. Le modifiche apportate a queste opzioni si applicano soltanto alle nuove query di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Per modificare le opzioni delle query correnti scegliere **Opzioni query** dal menu **Query** o il menu di scelta rapida della finestra Query di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Fare clic su **Avanzate** in **Esecuzione**. Per ulteriori informazioni su ognuna di queste opzioni, vedere la documentazione online di [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
## <a name="options"></a>Opzioni  
 **SET NOCOUNT**  
 Non restituisce il conteggio del numero di righe sotto forma di messaggio con il set di risultati. Questa casella di controllo è deselezionata per impostazione predefinita.  
  
 **SET NOEXEC**  
 La query non viene eseguita. Questa casella di controllo è deselezionata per impostazione predefinita.  
  
 **SET PARSEONLY**  
 Consente di verificare la sintassi di ogni query senza eseguire le query. Questa casella di controllo è deselezionata per impostazione predefinita.  
  
 **SET CONCAT_NULL_YIELDS_NULL**  
 Se questa casella di controllo è selezionata, le query che eseguono la concatenazione di un valore esistente con un valore NULL restituiscono sempre NULL come risultato. Se questa casella di controllo è deselezionata, un valore esistente concatenato con un valore NULL restituisce il valore esistente. Questa casella di controllo è selezionata per impostazione predefinita.  
  
 **SET ARITHABORT**  
 Se questa casella di controllo è selezionata, quando un'istruzione INSERT, DELETE o UPDATE incontra un errore aritmetico (overflow, divisione per zero o errore di dominio) durante la valutazione dell'espressione, la query o il batch viene terminato. Se questa casella di controllo è deselezionata, viene fornito un valore NULL per quel valore, se possibile, l'esecuzione della query continua e nel risultato viene incluso un messaggio. Per altre informazioni, vedere [SET ARITHABORT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-arithabort-transact-sql). Questa casella di controllo è selezionata per impostazione predefinita.  
  
 **SET SHOWPLAN_TEXT**  
 Se questa casella di controllo è selezionata, il piano di query viene restituito in formato testo per ogni query. Questa casella di controllo è deselezionata per impostazione predefinita.  
  
 **SET STATISTICS TIME**  
 Se questa casella di controllo è selezionata, le statistiche temporali vengono restituite con ogni query. Questa casella di controllo è deselezionata per impostazione predefinita.  
  
 **SET STATISTICS IO**  
 Se questa casella di controllo è selezionata, con ogni query vengono restituite statistiche relative all'input e all'output. Questa casella di controllo è deselezionata per impostazione predefinita.  
  
 **SET TRANSACTION ISOLATION LEVEL**  
 Il livello di isolamento delle transazioni READ COMMITTED è impostato per impostazione predefinita. Per altre informazioni, vedere [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql). Il livello di isolamento SNAPSHOT non è disponibile. Per utilizzare l'isolamento SNAPSHOT, aggiungere l'istruzione [!INCLUDE[tsql](../includes/tsql-md.md)] seguente:  
  
```  
SET TRANSACTION ISOLATION LEVEL SNAPSHOT;  
GO  
```  
  
 **SET DEADLOCK PRIORITY**  
 Il valore predefinito Normale consente a ogni query di avere la stessa priorità quando si verifica un deadlock. Selezionare la priorità Bassa se si desidera che la query perda in eventuali conflitti di deadlock e venga selezionata come query da interrompere.  
  
 **SET LOCK TIMEOUT**  
 Il valore predefinito -1 indica che i blocchi vengono mantenuti fino al completamento delle transazioni. Un valore uguale a 0 significa nessuna attesa e che non appena viene incontrato un blocco viene visualizzato un messaggio. Specificare un valore maggiore di 0 millisecondi per terminare una transazione se i blocchi delle transazioni devono essere mantenuti per un periodo di tempo superiore rispetto al tempo specificato.  
  
 **SET QUERY_GOVERNOR_COST_LIMIT**  
 Usare l'opzione **QUERY_GOVERNOR_COST_LIMIT** per specificare un limite di tempo massimo per l'esecuzione di una query. Il costo della query equivale al tempo trascorso (in secondi) stimato per l'esecuzione di una query in una configurazione hardware specifica. Il valore predefinito 0 indica che non esistono limiti di tempo per l'esecuzione di una query.  
  
 **Non visualizzare intestazioni messaggi provider**  
 Se questa casella di controllo è selezionata, non vengono visualizzati i messaggi di stato provenienti dal provider, ad esempio il provider SQLClient. Questa casella di controllo è selezionata per impostazione predefinita. Deselezionare questa casella di controllo per visualizzare i messaggi del provider durante la risoluzione dei problemi relativi alle query che potrebbero essersi verificati a livello del provider.  
  
 **Disconnetti al termine della query**  
 Se questa casella di controllo è selezionata, la connessione a [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] viene terminata dopo il completamento della query. Questa casella di controllo è deselezionata per impostazione predefinita.  
  
 **Ripristina predefiniti**  
 Reimposta le impostazioni predefinite originali per tutti i valori nella pagina.  
  
  
