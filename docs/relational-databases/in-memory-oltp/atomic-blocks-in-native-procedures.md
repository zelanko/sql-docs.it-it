---
title: Blocchi atomici | Microsoft Docs
description: Informazioni su BEGIN ATOMIC, parte dello standard SQL ANSI. SQL Server supporta i blocchi atomici nelle procedure native.
ms.custom: ''
ms.date: 10/26/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: 40e0e749-260c-4cfc-a848-444d30c09d85
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 7e5de0ea599650792feef01508c1eed54aed68c6
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97465432"
---
# <a name="atomic-blocks-in-native-procedures"></a>Blocchi atomici nelle procedure native
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  **BEGIN ATOMIC** fa parte dello standard SQL ANSI. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta i blocchi atomici al livello superiore di stored procedure compilate in modo nativo, nonché per le funzioni compilate in modo nativo e scalari definite dall'utente. Per altre informazioni su queste funzioni, vedere [Funzioni scalari definite dall'utente per OLTP in memoria](../../relational-databases/in-memory-oltp/scalar-user-defined-functions-for-in-memory-oltp.md).  
  
-   Ogni stored procedure compilata in modo nativo contiene un blocco di istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] . Si tratta di un blocco ATOMIC.  
  
-   Le stored procedure [!INCLUDE[tsql](../../includes/tsql-md.md)] interpretate e non native e i batch ad hoc non supportano i blocchi atomici.  
  
 I blocchi atomici vengono eseguiti (in modo atomico) nella transazione. Tutte le istruzioni nel blocco devono avere esito positivo, altrimenti verrà eseguito il rollback dell'intero blocco al punto di salvataggio creato all'inizio del blocco. Inoltre, per il blocco atomico tutte le impostazioni di sessione sono fisse. L'esecuzione dello stesso blocco atomico in sessioni con impostazioni diverse genera lo stesso comportamento, indipendentemente dalle impostazioni della sessione corrente.  
  
## <a name="transactions-and-error-handling"></a>Transazioni e gestione degli errori  
 Se in una sessione esiste già una transazione (perché un batch ha eseguito un'istruzione **BEGIN TRANSACTION** e la transazione rimane attiva), l'avvio di un blocco atomico creerà un punto di salvataggio nella transazione. Se il blocco viene chiuso senza un'eccezione, viene eseguito il commit del punto di salvataggio creato per il blocco, ma non verrà eseguito il commit della transazione finché non viene eseguito il commit a livello di sessione. Se il blocco genera un'eccezione, viene eseguito il rollback degli effetti del blocco, ma la transazione procede a livello di sessione, a meno che l'eccezione non la termini. Ad esempio, un conflitto di scrittura comporta la fine della transazione, ma non un errore di cast del tipo.  
  
 Se non è presente alcuna transazione attiva in una sessione, **BEGIN ATOMIC** avvia una nuova transazione. Se non viene generata alcuna eccezione all'esterno dell'ambito del blocco, verrà eseguito il commit della transazione alla fine del blocco. Se il blocco genera un'eccezione (l'eccezione non viene rilevata e gestita nel blocco), verrà eseguito il rollback della transazione. Per le transazioni che interessano un singolo blocco atomico (una singola stored procedure compilata in modo nativo), non è necessario scrivere istruzioni **BEGIN TRANSACTION** e **COMMIT** o **ROLLBACK** esplicite.  
  
 Le stored procedure compilate in modo nativo supportano i costrutti **TRY**, **CATCH** e **THROW** per la gestione degli errori. **RAISERROR** non è supportato.  
  
 Nell'esempio seguente viene illustrato il comportamento della gestione degli errori con blocchi atomici e stored procedure compilate in modo nativo:  
  
```sql  
-- sample table  
CREATE TABLE dbo.t1 (  
  c1 int not null primary key nonclustered  
)  
WITH (MEMORY_OPTIMIZED=ON)  
GO  
  
-- sample proc that inserts 2 rows  
CREATE PROCEDURE dbo.usp_t1 @v1 bigint not null, @v2 bigint not null  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS  
BEGIN ATOMIC  
WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'us_english', DELAYED_DURABILITY = ON)  
  
  INSERT dbo.t1 VALUES (@v1)  
  INSERT dbo.t1 VALUES (@v2)  
  
END  
GO  
  
-- insert two rows  
EXEC dbo.usp_t1 1, 2  
GO  
  
-- verify we have no active transaction  
SELECT @@TRANCOUNT  
GO  
  
-- verify the rows 1 and 2 were committed  
SELECT c1 FROM dbo.t1  
GO  
  
-- execute proc with arithmetic overflow  
EXEC dbo.usp_t1 3, 4444444444444  
GO  
-- expected error message:  
-- Msg 8115, Level 16, State 0, Procedure usp_t1  
-- Arithmetic overflow error converting bigint to data type int.  
  
-- verify we have no active transaction  
SELECT @@TRANCOUNT  
GO  
  
-- verify rows 3 was not committed; usp_t1 has been rolled back  
SELECT c1 FROM dbo.t1  
GO  
  
-- start a new transaction  
BEGIN TRANSACTION  
  -- insert rows 3 and 4  
  EXEC dbo.usp_t1 3, 4  
  
  -- verify there is still an active transaction  
  SELECT @@TRANCOUNT  
  
  -- verify the rows 3 and 4 were inserted  
  SELECT c1 FROM dbo.t1 WITH (SNAPSHOT)   
  ORDER BY c1  
  
  -- catch the arithmetic overflow error  
  BEGIN TRY  
    EXEC dbo.usp_t1 5, 4444444444444  
  END TRY  
  BEGIN CATCH  
    PRINT N'Error occurred: ' + error_message()  
  END CATCH  
  
  -- verify there is still an active transaction  
  SELECT @@TRANCOUNT  
  
  -- verify rows 3 and 4 are still in the table, and row 5 has not been inserted  
  SELECT c1 FROM dbo.t1 WITH (SNAPSHOT)   
  ORDER BY c1  
  
COMMIT  
GO  
  
-- verify we have no active transaction  
SELECT @@TRANCOUNT  
GO  
  
-- verify rows 3 and 4 has been committed  
SELECT c1 FROM dbo.t1  
ORDER BY c1  
GO  
```  
  
 I messaggi di errore seguenti specifici delle tabelle ottimizzate per la memoria comportano la fine della transazione. Se si verificano nell'ambito di un blocco atomico, causano l'interruzione della transazione: 10772, 41301, 41302, 41305, 41325, 41332, 41333 e 41839.  
  
## <a name="session-settings"></a>Impostazioni sessione  
 Le impostazioni di sessione nei blocchi atomici sono fisse quando la stored procedure è compilata. Alcune impostazioni possono essere specificate con **BEGIN ATOMIC** , mentre altre sono sempre fisse sullo stesso valore.  
  
 Le opzioni seguenti sono necessarie con **BEGIN ATOMIC**:  
  
|Impostazione necessaria|Descrizione|  
|----------------------|-----------------|  
|**TRANSACTION ISOLATION LEVEL**|I valori supportati sono **SNAPSHOT**, **REPEATABLEREAD** e **SERIALIZABLE**.|  
|**LANGUAGE**|Determina i formati data e ora e i messaggi di sistema. Tutti i linguaggi e gli alias in [sys.syslanguages &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-syslanguages-transact-sql.md) sono supportati.|  
  
 Le impostazioni seguenti sono facoltative:  
  
|Impostazione facoltativa|Descrizione|  
|----------------------|-----------------|  
|**DATEFORMAT**|Tutti i formati data di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sono supportati. Quando viene specificata, **DATEFORMAT** esegue l'override del formato data predefinito associato a **LANGUAGE**.|  
|**DATEFORMAT**|Quando viene specificata, **DATEFIRST** esegue l'override del valore predefinito associato a **LANGUAGE**.|  
|**DELAYED_DURABILITY**|I valori supportati sono **OFF** e **ON**.<br /><br /> Il commit delle transazioni [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] può essere completamente durevole, che è l'impostazione predefinita, oppure con durabilità ritardata. Per altre informazioni, vedere [Controllo della durabilità delle transazioni](../../relational-databases/logs/control-transaction-durability.md).|  
  
 Le opzioni SET seguenti presentano lo stesso valore predefinito di sistema per tutti i blocchi atomici in tutte le stored procedure compilate in modo nativo:  
  
|Opzione SET|Impostazione predefinita di sistema per i blocchi atomici|  
|----------------|--------------------------------------|  
|ANSI_NULLS|ON|  
|ANSI_PADDING|ON|  
|ANSI_WARNING|ON|  
|ARITHABORT|ON|  
|ARITHIGNORE|OFF|  
|CONCAT_NULL_YIELDS_NULL|ON|  
|IDENTITY_INSERT|OFF|  
|NOCOUNT|ON|  
|NUMERIC_ROUNDABORT|OFF|  
|QUOTED_IDENTIFIER|ON|  
|ROWCOUNT|0|  
|TEXTSIZE|0|  
|XACT_ABORT|OFF<br /><br /> Le eccezioni non rilevate causano il rollback dei blocchi atomici, ma non l'interruzione della transazione, a meno che l'errore non comporti la fine della transazione.|  
  
## <a name="see-also"></a>Vedere anche  
 [Stored procedure compilate in modo nativo](./a-guide-to-query-processing-for-memory-optimized-tables.md)  
  
