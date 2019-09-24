---
title: Esecuzione di opzioni query (pagina Avanzate) | Microsoft Docs
ms.prod: sql-server-2014
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.query.advanced.f1
ms.assetid: 661595ce-99b9-4316-ad80-ed04002d04d5
author: markingmyname
ms.author: maghan
manager: jroth
ms.reviewer: ''
ms.custom: ''
ms.date: 09/03/2019
ms.openlocfilehash: 39a43adeb82b154a076fc7bfc24cc56b54cc8640
ms.sourcegitcommit: 9221a693d4ab7ae0a7e2ddeb03bd0cf740628fd0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/23/2019
ms.locfileid: "71199321"
---
# <a name="query-options-execution-advanced-page"></a>Esecuzione di Opzioni query (pagina Avanzate)

  L'uso dell'istruzione **SET** rende disponibili numerose opzioni. Utilizzare questa pagina per specificare un'opzione **set** per l'esecuzione di Microsoft SQL Server query. Per informazioni dettagliate su ogni opzione, vedere la documentazione online di SQL Server.
  
**set NOcount** Non restituisce il conteggio del numero di righe, come messaggio con il set di risultati. Questa opzione è deselezionata per impostazione predefinita.

**set NOexec** Non esegue la query. Questa opzione è deselezionata per impostazione predefinita.

**imposta PARSEONLY** Controlla la sintassi di ogni query senza eseguire le query. Questa opzione è deselezionata per impostazione predefinita.  

**imposta CONCAT_NULL_YIELDS_NULL** Se questa casella di controllo è selezionata, le query che concatenano un valore `NULL`esistente con un oggetto `NULL` restituiscono sempre come risultato. Se questa casella di controllo è deselezionata, un valore esistente concatenato con un valore `NULL` restituisce il valore esistente. Questa opzione è selezionata per impostazione predefinita.

**imposta ARITHABORT** Se questa casella di controllo è selezionata, quando `INSERT`un' `DELETE` istruzione `UPDATE` , o rileva un errore aritmetico (overflow, divisione per zero o errore di dominio) durante la valutazione dell'espressione, la query o il batch viene terminato. Se questa casella di controllo è deselezionata, viene fornito un valore `NULL` per quel valore, se possibile, l'esecuzione della query continua e nel risultato viene incluso un messaggio. Per ulteriori informazioni sull'argomento, vedere la documentazione online. Questa opzione è selezionata per impostazione predefinita.
  
**imposta SHOWPLAN_TEXT** Se questa casella di controllo è selezionata, il piano di query viene restituito in formato testo a ogni query. Questa opzione è deselezionata per impostazione predefinita.
  
**Imposta ora statistiche** Se questa casella di controllo è selezionata, con ogni query vengono restituite le statistiche temporali. Questa opzione è deselezionata per impostazione predefinita.
  
**set Statistics io** Se questa casella di controllo è selezionata, con ogni query vengono restituite statistiche relative all'input/output (I/O). Questa opzione è deselezionata per impostazione predefinita.
  
**imposta il livello di isolamento delle transazioni** Il livello di isolamento delle transazioni READ COMMITTED è impostato per impostazione predefinita. Per altre informazioni, vedere [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-transaction-isolation-level-transact-sql). Il livello di isolamento SNAPSHOT Transaction non è disponibile. Per utilizzare l'isolamento SNAPSHOT, aggiungere l'istruzione [!INCLUDE[tsql](../includes/tsql-md.md)] seguente:
  
  ```sql
  SET TRANSACTION ISOLATION LEVEL SNAPSHOT;
  GO
  ```

**Imposta priorità deadlock** Il valore predefinito **normale** consente a ogni query di avere la stessa priorità quando si verifica un deadlock. Selezionare la priorità Bassa nell'elenco a discesa se si desidera che la query specifica ignori gli eventuali conflitti con deadlock e che sia possibile selezionarla come query da terminare.

**Imposta timeout blocco** Il valore predefinito-1 indica che i blocchi vengono mantenuti fino al completamento delle transazioni. Un valore uguale a 0 significa nessuna attesa e che non appena viene incontrato un blocco viene visualizzato un messaggio. Specificare un valore maggiore di 0 millisecondi per terminare una transazione se i blocchi delle transazioni devono essere mantenuti per un periodo di tempo superiore rispetto al tempo specificato.

**imposta QUERY_GOVERNOR_COST_LIMIT** Utilizzare l'opzione **limite di costo Query Governor** per specificare un limite massimo per il periodo di tempo in cui è possibile eseguire una query. Il costo della query equivale al tempo trascorso (in secondi) stimato per l'esecuzione di una query in una configurazione hardware specifica. Il valore predefinito 0 indica che non esistono limiti all'estensione di tempo per l'esecuzione di una query.

Non **visualizzare le intestazioni del messaggio del provider** Se questa casella di controllo è selezionata, non vengono visualizzati i messaggi di stato provenienti dal provider, ad esempio il provider di OLE DB. Questa casella di controllo è selezionata per impostazione predefinita. Deselezionare questa casella di controllo per visualizzare i messaggi del provider durante la risoluzione dei problemi relativi alle query che potrebbero essersi verificati a livello del provider.

**Disconnetti dopo l'esecuzione della query** Se questa casella di controllo è selezionata, la connessione a SQL Server viene terminata dopo il completamento della query. Questa opzione è deselezionata per impostazione predefinita.

**Mostra ora di completamento** Consente di stampare l'ora in cui l'esecuzione della query è stata completata dopo i risultati della query o nella scheda messaggi.

**Protocollo di attestazione per le enclavi vbs per Always Encrypted** Consente di impostare un protocollo di attestazione per gli enclave di sicurezza basata sulla virtualizzazione (VBS) usati da Always Encrypted con le enclave sicure.

I protocolli di attestazione supportati correnti sono:

* Servizio sorveglianza host: protocollo di attestazione che utilizza il servizio sorveglianza host di Windows (HGS).

Per altre informazioni, vedere [Always Encrypted con le enclave sicure](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-enclaves?view=sqlallproducts-allversions) e l' [attestazione protetta dell'enclave](https://docs.microsoft.com/sql/relational-databases/security/encryption/always-encrypted-enclaves?view=sqlallproducts-allversions#secure-enclave-attestation).

**Ripristina predefiniti** Reimposta le impostazioni predefinite originali per tutti i valori nella pagina.
