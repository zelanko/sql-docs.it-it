---
title: Livelli di isolamento delle transazioni per le tabelle ottimizzate per la memoria | Microsoft Docs
ms.custom: seo-dt-2019
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 8a6a82bf-273c-40ab-a101-46bd3615db8a
author: stevestein
ms.author: sstein
ms.openlocfilehash: 5ee0ba17dc999c9076ca4622d47db28b8200b851
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84928172"
---
# <a name="transaction-isolation-levels-in-memory-optimized-tables"></a>Livelli di isolamento delle transazioni nelle tabelle con ottimizzazione per la memoria

  Di seguito sono indicati i livelli di isolamento supportati per le transazioni che accedono a tabelle ottimizzate per la memoria.  
  
-   SNAPSHOT  
  
-   REPEATABLE READ  
  
-   SERIALIZABLE  
  
-   READ COMMITTED  
  
 Il livello di isolamento della transazione può essere specificato come parte del blocco atomico di una stored procedure compilata in modo nativo. Per altre informazioni, vedere [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql). Quando si accede a tabelle ottimizzate per la memoria da codice [!INCLUDE[tsql](../includes/tsql-md.md)] interpretato, è possibile specificare il livello di isolamento tramite hint a livello di tabella.  
  
 È necessario specificare il livello di isolamento delle transazioni quando si definisce una stored procedure compilata in modo nativo. È necessario specificare il livello di isolamento in hint di tabella quando si accede alle tabelle ottimizzate per la memoria da transazioni utente in codice [!INCLUDE[tsql](../includes/tsql-md.md)] interpretato. Per ulteriori informazioni, vedere [linee guida per i livelli di isolamento delle transazioni con tabelle ottimizzate per la memoria](../relational-databases/in-memory-oltp/memory-optimized-tables.md).  
  
 Il livello di isolamento READ COMMITTED è supportato per le tabelle ottimizzate per la memoria con transazioni in modalità autocommit. READ COMMITTED non è valido nelle transazioni utente o in un blocco atomico. READ COMMITTED non è invece supportato con le transazioni utente implicite o esplicite. Il livello di isolamento READ_COMMITTED_SNAPSHOT è supportato per le tabelle ottimizzate per la memoria con transazioni in modalità autocommit e solo se la query non accede alle tabelle basate su disco. Alle transazioni avviate tramite codice [!INCLUDE[tsql](../includes/tsql-md.md)] interpretato con isolamento SNAPSHOT non è inoltre consentito accedere alle tabelle ottimizzate per la memoria. Le transazioni che utilizzano codice [!INCLUDE[tsql](../includes/tsql-md.md)] interpretato con isolamento REPEATABLE READ o SERIALIZABLE devono accedere alle tabelle ottimizzate per la memoria utilizzando il livello di isolamento SNAPSHOT. Per altre informazioni su questo scenario, vedere [transazioni tra contenitori](cross-container-transactions.md).  
  
 READ COMMITTED è il livello di isolamento predefinito in [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Quando il livello di isolamento della sessione è READ COMMITTED o inferiore, è possibile effettuare una delle operazioni seguenti:  
  
-   Utilizzare in modo esplicito un hint superiore del livello di isolamento per accedere alla tabella ottimizzata per la memoria, ad esempio WITH (SNAPSHOT).  
  
-   Specificare l'opzione del set `MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT`, tramite cui verrà impostato il livello di isolamento per le tabelle ottimizzate per la memoria su SNAPSHOT (come se si includessero hint WITH(SNAPSHOT) in ogni tabella ottimizzata per la memoria). Per ulteriori informazioni su `MEMORY_OPTIMIZED_ELEVATE_TO_SNAPSHOT` , vedere [Opzioni ALTER DATABASE SET &#40;&#41;Transact-SQL ](/sql/t-sql/statements/alter-database-transact-sql-set-options).  
  
 In alternativa, se il livello di isolamento della sessione è READ COMMITTED, è possibile utilizzare le transazioni in modalità autocommit.  
  
 Le transazioni SNAPSHOT avviate tramite codice [!INCLUDE[tsql](../includes/tsql-md.md)] interpretato non possono accedere alle tabelle ottimizzate per la memoria.  
  
 I livelli di isolamento delle transazioni supportati per le tabelle ottimizzate per la memoria forniscono le stesse garanzie logiche delle tabelle basate su disco. Il meccanismo utilizzato per fornire le garanzie del livello di isolamento è diverso.  
  
 Per le tabelle basate su disco la maggior parte delle garanzie del livello di isolamento vengono implementate mediante l'utilizzo dei blocchi, che impediscono l'insorgere di conflitti. Per le tabelle ottimizzate per la memoria le garanzie vengono applicate utilizzando un meccanismo di rilevamento dei conflitti, che consente di evitare l'utilizzo di blocchi. Fa eccezione l'isolamento SNAPSHOT per le tabelle basate su disco, che viene implementato in modo analogo all'isolamento SNAPSHOT per le tabelle ottimizzate per la memoria tramite un meccanismo di rilevamento dei conflitti.  
  
 SNAPSHOT  
 Questo livello di isolamento specifica che i dati letti da qualsiasi istruzione in una transazione rappresenteranno la versione coerente a livello di transazione dei dati presenti all'avvio della transazione stessa. La transazione può quindi accedere solo alle modifiche dei dati di cui è stato eseguito il commit prima dell'avvio della transazione. Le modifiche ai dati apportate da altre transazioni dopo l'avvio della transazione corrente non sono visibili per le istruzioni eseguite nella transazione corrente. Le istruzioni di una transazione ottengono uno snapshot dei dati di cui è stato eseguito il commit corrispondente a quelli presenti all'avvio della transazione.  
  
 Le operazioni di scrittura (aggiornamenti, inserimenti ed eliminazioni) vengono sempre isolate completamente da altre transazioni. Le operazioni di scrittura in una transazione SNAPSHOT possono pertanto entrare in conflitto con quelle eseguite da altre transazioni. Quando la transazione corrente tenta di aggiornare o eliminare una riga aggiornata o eliminata da un'altra transazione che ha eseguito il commit dopo l'avvio della transazione corrente, quest'ultima viene terminata con un messaggio di errore analogo al seguente.  
  
 Errore 41302. Tentativo da parte della transazione corrente di aggiornare un record nella tabella X che è già stato aggiornato dopo l'avvio della transazione. La transazione è stata interrotta.  
  
 Quando la transazione corrente tenta di inserire una riga con lo stesso valore di chiave primaria di una riga inserita da un'altra transazione che ha eseguito il commit prima della transazione corrente, si verificherà un errore di commit con un messaggio di errore analogo al seguente.  
  
 Errore 41325. Impossibile eseguire il commit della transazione corrente a causa di un errore di convalida serializzabile.  
  
 Se una transazione effettua la scrittura in una tabella eliminata prima del commit della transazione, la transazione viene terminata con un messaggio di errore analogo al seguente:  
  
 Errore 41305. Impossibile eseguire il commit della transazione corrente a causa di un errore di convalida di lettura ripetibile.  
  
 REPEATABLE READ  
 In questo livello di isolamento sono incluse le garanzie fornite dal livello di isolamento SNAPSHOT. REPEATABLE READ garantisce inoltre che, per ogni riga letta dalla transazione, al momento dell'esecuzione del commit da parte della transazione la riga non sia stata modificata da un'altra transazione. Ogni operazione di lettura nella transazione è ripetibile fino alla fine della transazione.  
  
 Se nella transazione corrente viene letta una qualsiasi riga aggiornata da un'altra transazione che ha eseguito il commit prima della transazione corrente, il commit ha esito negativo con un messaggio di errore analogo al seguente.  
  
 Errore 41305. Impossibile eseguire il commit della transazione corrente a causa di un errore di convalida di lettura ripetibile.  
  
 SERIALIZABLE  
 In questo livello di isolamento sono incluse le garanzie fornite dal livello di isolamento REPEATABLE READ. Nessuna riga fantasma è stata rilevata tra il momento dello snapshot e la fine della transazione. Le righe fantasma corrispondono alla condizione di filtro di una selezione, un aggiornamento o un'eliminazione.  
  
 La transazione viene eseguita come se non fossero presenti transazioni simultanee. Tutte le azioni si verificano virtualmente in un singolo punto di serializzazione (ora di commit).  
  
 Se una di queste garanzie viene violata, il commit della transazione non viene eseguito con un messaggio di errore analogo al seguente:  
  
 Errore 41325. Impossibile eseguire il commit della transazione corrente a causa di un errore di convalida serializzabile.  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sulle transazioni nelle tabelle ottimizzate per la memoria](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)   
 [Linee guida per i livelli di isolamento delle transazioni con tabelle con ottimizzazione per la memoria](../relational-databases/in-memory-oltp/memory-optimized-tables.md)   
 [Linee guida per la logica di riesecuzione per le transazioni in tabelle con ottimizzazione per la memoria](../../2014/database-engine/guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables.md)  
  
  
