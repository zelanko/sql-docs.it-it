---
title: Linee guida per la logica di ripetizione dei tentativi per le transazioni nelle tabelle ottimizzate per la memoria | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f2a35c37-4449-49ee-8bba-928028f1de66
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 01f719470419940b130967b7c1360c4ae0c281eb
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62779215"
---
# <a name="guidelines-for-retry-logic-for-transactions-on-memory-optimized-tables"></a>Linee guida per la logica di riesecuzione per le transazioni in tabelle con ottimizzazione per la memoria
  Esistono condizioni di errore che si verificano con le transazioni che accedono a tabelle ottimizzate per la memoria.  
  
-   41302. Tentativo da parte della transazione corrente di aggiornare un record che è già stato aggiornato dopo l'avvio della transazione.  
  
-   41305. Impossibile eseguire il commit della transazione corrente a causa di un errore di convalida di lettura ripetibile.  
  
-   41325. Impossibile eseguire il commit della transazione corrente a causa di un errore di convalida serializzabile.  
  
-   41301. Una transazione precedente da cui dipende la transazione corrente è stata interrotta. Impossibile eseguire il commit della transazione corrente.  
  
 Una causa comune di questi errori è con una transazione eseguita simultaneamente. L'azione correttiva normale consiste nel ripetere la transazione.  
  
 Per altre informazioni su queste condizioni di errore, vedere la sezione sul rilevamento dei conflitti, convalida e controlli di dipendenza di Commit in [transazioni in tabelle ottimizzate per la memoria](../relational-databases/in-memory-oltp/memory-optimized-tables.md).  
  
 I deadlock (codice di errore 1205) non possono verificarsi per le tabelle ottimizzate per la memoria. I blocchi non vengono utilizzati per le tabelle ottimizzate per la memoria. Se tuttavia nell'applicazione è già presente la logica di riesecuzione per i deadlock, la logica esistente può essere estesa in modo da includere i nuovi codici di errore.  
  
## <a name="considerations-for-retrying"></a>Considerazioni sulla riesecuzione  
 Nelle applicazioni si verificano in genere conflitti tra le transazioni ed è necessario implementare la logica di riesecuzione per risolverli. Il numero di conflitti rilevati dipende da una serie di fattori:  
  
-   Contesa per singole righe. Il rischio di conflitti aumenta man mano che aumenta il numero di transazioni che tenta di aggiornare la stessa riga.  
  
-   Numero di righe lette dalle transazioni REPEATABLE READ. Più righe vengono lette, maggiore è la probabilità che alcune di queste righe vengano aggiornate da transazioni simultanee. Questa condizione causa errori di convalida di lettura ripetibili.  
  
-   Dimensioni degli intervalli di analisi utilizzati dalle transazioni SERIALIZABLE. Maggiori sono le dimensioni degli intervalli di analisi, maggiore è la probabilità che le transazioni simultanee introducano righe fantasma, causando errori di convalida serializzabili.  
  
     È difficile evitare questi conflitti in un'applicazione, pertanto è necessaria la logica di riesecuzione.  
  
> [!IMPORTANT]  
>  Le transazioni di lettura e scrittura che accedono a tabelle ottimizzate per la memoria richiedono la logica di riesecuzione.  
  
### <a name="considerations-for-read-only-transactions-and-natively-compiled-stored-procedures"></a>Considerazioni sulle transazioni di sola lettura e sulle stored procedure compilate in modo nativo  
 Le transazioni di sola lettura che interessano una singola esecuzione di una stored procedure compilata in modo nativo non richiedono la convalida per le transazioni REPEATABLE READ e SERIALIZABLE. I conflitti di scrittura non possono verificarsi a causa di una transazione di sola lettura.  
  
 Gli errori di dipendenza possono tuttavia continuare a verificarsi. Gli errori di dipendenza sono meno comuni degli errori risultanti da conflitti. In molti casi non è quindi richiesta logica di riesecuzione specifica per le transazioni di sola lettura che interessano singole esecuzioni di stored procedure compilate in modo nativo.  
  
### <a name="considerations-for-read-only-transactions-and-cross-container-transactions"></a>Considerazioni sulle transazioni di sola lettura e sulle transazioni tra contenitori  
 Per le transazioni di sola lettura tra contenitori, ovvero transazioni che vengono avviate al di fuori del contesto di una stored procedure compilata in modo nativo, non viene eseguita la convalida se l'accesso alle tabelle ottimizzate per la memoria avviene nel livello di isolamento SNAPSHOT. Quando tuttavia si accede alle tabelle ottimizzate per la memoria nell'isolamento REPEATABLE READ o SERIALIZABLE, la convalida viene eseguita in fase di commit. In questo caso, potrebbe essere richiesta la logica di riesecuzione.  
  
 Per altre informazioni, vedere la sezione sulle transazioni tra contenitori in [livelli di isolamento delle transazioni](../../2014/database-engine/transaction-isolation-levels.md).  
  
## <a name="implementing-retry-logic"></a>Implementare della logica di riesecuzione  
 Come per tutte le transazioni che accedono a tabelle ottimizzate per la memoria, è necessario considerare la logica di riesecuzione per gestire possibili errori, ad esempio conflitti di scrittura (codice di errore 41302) o errori di dipendenza (codice di errore 41301). Nella maggior parte delle applicazioni il tasso di errori sarà basso, ma è comunque necessario gestire gli errori rieseguendo la transazione. È consigliabile implementare la logica di riesecuzione nei due modi seguenti:  
  
-   Tentativi sul lato client. I tentativi sul lato client costituiscono il modo consigliato per implementare la logica di riesecuzione nel caso generale. L'applicazione client rileva l'errore generato dalla transazione e riesegue la transazione. Se un'applicazione client esistente dispone di una logica di riesecuzione per la gestione di deadlock, è possibile estendere l'applicazione per gestire i nuovi codici di errore.  
  
-   Utilizzo di una stored procedure del wrapper. Il client chiama una stored procedure [!INCLUDE[tsql](../includes/tsql-md.md)] interpretata che chiama la stored procedure compilata in modo nativo oppure esegue la transazione. La procedura del wrapper utilizza la logica try/catch per rilevare l'errore e per ripetere la chiamata di procedura, se necessario. È possibile che i risultati vengano restituiti al client prima dell'errore e che il client non sia in grado di rimuoverli. Per essere sicuri, è pertanto preferibile utilizzare questo metodo solo con le stored procedure compilate in modo nativo che non restituiscono alcun set di risultati al client.  
  
 La logica di riesecuzione può essere implementata in [!INCLUDE[tsql](../includes/tsql-md.md)] o nel livello intermedio del codice di un'applicazione.  
  
 Di seguito sono indicate due possibili motivi per considerare la logica di riesecuzione:  
  
-   L'applicazione client dispone di logica di riesecuzione per altri codici di errore, ad esempio 1205, che è possibile estendere.  
  
-   I conflitti sono rari ed è importante ridurre la latenza end-to-end mediante un'esecuzione preparata. Per altre informazioni sull'esecuzione in modo nativo stored procedure compilate direttamente, vedere [Natively Compiled Stored Procedures](../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).  
  
 Nell'esempio seguente viene illustrata la logica di riesecuzione in una stored procedure [!INCLUDE[tsql](../includes/tsql-md.md)] interpretata che contiene una chiamata a una stored procedure compilata in modo nativo o a una transazione tra contenitori.  
  
```sql  
CREATE PROCEDURE usp_my_procedure @param1 type1, @param2 type2, ...  
AS  
BEGIN  
  -- number of retries - tune based on the workload  
  DECLARE @retry INT = 10  
  
  WHILE (@retry > 0)  
  BEGIN  
    BEGIN TRY  
  
      -- exec usp_my_native_proc @param1, @param2, ...  
  
      --       or  
  
      -- BEGIN TRANSACTION  
      --   ...  
      -- COMMIT TRANSACTION  
  
      SET @retry = 0  
    END TRY  
    BEGIN CATCH  
      SET @retry -= 1  
  
      -- the error number for deadlocks (1205) does not need to be included for   
      -- transactions that do not access disk-based tables  
      IF (@retry > 0 AND error_number() in (41302, 41305, 41325, 41301, 1205))  
      BEGIN  
        -- these error conditions are transaction dooming - rollback the transaction  
        -- this is not needed if the transaction spans a single native proc execution  
        --   as the native proc will simply rollback when an error is thrown   
        IF XACT_STATE() = -1  
          ROLLBACK TRANSACTION  
  
        -- use a delay if there is a high rate of write conflicts (41302)  
        --   length of delay should depend on the typical duration of conflicting transactions  
        -- WAITFOR DELAY '00:00:00.001'  
      END  
      ELSE  
      BEGIN  
        -- insert custom error handling for other error conditions here  
  
        -- throw if this is not a qualifying error condition  
        ;THROW  
      END  
    END CATCH  
  END  
END  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Informazioni sulle transazioni nelle tabelle ottimizzate per la memoria](../../2014/database-engine/understanding-transactions-on-memory-optimized-tables.md)   
 [Transazioni nelle tabelle ottimizzate per la memoria](../relational-databases/in-memory-oltp/memory-optimized-tables.md)   
 [Linee guida per i livelli di isolamento delle transazioni con tabelle con ottimizzazione per la memoria](../../2014/database-engine/guidelines-for-transaction-isolation-levels-with-memory-optimized-tables.md)  
  
  
