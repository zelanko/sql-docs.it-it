---
title: Transazioni (Azure Synapse Analytics)
description: Una transazione è un gruppo di una o più istruzioni di database di cui è stato interamente eseguito il commit o il rollback.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 87e5e593-a121-4428-9d3c-3af876224e35
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || = sqlallproducts-allversions'
ms.openlocfilehash: 5a8b1aa27a301d67df200967b6cba36f042a7f75
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 11/26/2020
ms.locfileid: "92038895"
---
# <a name="transactions-azure-synapse-analytics"></a>Transazioni (Azure Synapse Analytics)

[!INCLUDE[applies-to-version/asa-pdw](../../includes/applies-to-version/asa-pdw.md)]

  Una transazione è un gruppo di una o più istruzioni di database di cui è stato interamente eseguito il commit o il rollback. Ogni transazione è atomica, coerente, isolata e duratura, dotata cioè delle cosiddette proprietà ACID. Se la transazione ha esito positivo, viene eseguito il commit di tutte le istruzioni al suo interno. Se la transazione ha esito negativo, ovvero se almeno una delle istruzioni del gruppo non riesce, viene eseguito il rollback dell'intero gruppo.  
  
 L'inizio e la fine delle transazioni dipendono dell'impostazione AUTOCOMMIT e dalle istruzioni BEGIN TRANSACTION, COMMIT e ROLLBACK. [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] supporta i tipi di transazioni seguenti:  
  
-   Le *transazioni esplicite* iniziano con l'istruzione BEGIN TRANSACTION e terminano con l'istruzione COMMIT o ROLLBACK.  
  
-   Le *transazioni con commit automatico* iniziano automaticamente all'interno di una sessione e non iniziano con l'istruzione BEGIN TRANSACTION. Se l'impostazione AUTOCOMMIT corrisponde a ON, ogni istruzione viene eseguita in una transazione e non è necessaria un'istruzione COMMIT o ROLLBACK esplicita. Se l'impostazione AUTOCOMMIT corrisponde a OFF, è necessaria un'istruzione COMMIT o ROLLBACK per determinare il risultato della transazione. In [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], le transazioni con commit automatico iniziano immediatamente dopo un'istruzione COMMIT o ROLLBACK oppure dopo un'istruzione SET AUTOCOMMIT OFF.  
  
 ![Icona di collegamento a un argomento](../../database-engine/configure-windows/media/topic-link.gif "Icona di collegamento a un argomento") [Convenzioni della sintassi Transact-SQL &#40;Transact-SQL&#41;](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintassi  
  
```syntaxsql
BEGIN TRANSACTION [;]  
COMMIT [ TRAN | TRANSACTION | WORK ] [;]  
ROLLBACK [ TRAN | TRANSACTION | WORK ] [;]  
SET AUTOCOMMIT { ON | OFF } [;]  
SET IMPLICIT_TRANSACTIONS { ON | OFF } [;]  
```  
  
## <a name="arguments"></a>Argomenti  
 BEGIN TRANSACTION  
 Contrassegna il punto di inizio di una transazione esplicita.  
  
 COMMIT [ WORK ]  
 Contrassegna la fine di una transazione esplicita o con commit automatico. Con questa istruzione viene eseguito il commit permanente nel database delle modifiche apportate alla transazione. L'istruzione COMMIT è identica alle istruzioni COMMIT WORK, COMMIT TRAN e COMMIT TRANSACTION.  
  
 ROLLBACK [ WORK ]  
 Esegue il rollback di una transazione fino all'inizio della transazione stessa. Nel database non viene eseguito il commit di alcuna modifica alla transazione. L'istruzione ROLLBACK è identica alle istruzioni ROLLBACK WORK, ROLLBACK TRAN e ROLLBACK TRANSACTION.  
  
 SET AUTOCOMMIT { **ON** | OFF }  
 Determina la modalità di inizio e di fine delle transazioni.  
  
 ON  
 Ogni istruzione viene eseguita in una transazione specifica. Non è necessaria un'istruzione COMMIT o ROLLBACK esplicita. Se AUTOCOMMIT corrisponde a ON, le transazioni esplicite sono consentite.  
  
 OFF  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] avvia automaticamente una transazione, se non ne è in corso alcuna. Tutte le istruzioni successive vengono eseguite nell'ambito della transazione ed è necessaria un'istruzione COMMIT o ROLLBACK per determinare il risultato della transazione. Non appena viene eseguito il commit o il rollback di una transazione in questa modalità operativa, la modalità rimane impostata su OFF e [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] avvia una nuova transazione. Se AUTOCOMMIT corrisponde a OFF, le transazioni esplicite non sono consentite.  
  
 Se si modifica l'impostazione AUTOCOMMIT all'interno di una transazione attiva, l'impostazione influisce sulla transazione corrente e ha effetto solo dopo il completamento della transazione.  
  
 Se AUTOCOMMIT corrisponde a ON, l'esecuzione di un'altra istruzione SET AUTOCOMMIT ON non ha alcun effetto. Analogamente, se AUTOCOMMIT corrisponde a OFF, l'esecuzione di un'altra istruzione SET AUTOCOMMIT OFF non ha alcun effetto.  
  
 SET IMPLICIT_TRANSACTIONS { ON | **OFF** }  
 Attiva e disattiva le stesse modalità di SET AUTOCOMMIT. Quando è impostata su ON, l'opzione SET IMPLICIT_TRANSACTIONS imposta per la connessione la modalità di transazione implicita. Quando è impostata su OFF, ripristina la modalità di transazione con commit automatico.  Per altre informazioni, vedere [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md).  
  
## <a name="permissions"></a>Autorizzazioni  
 Per eseguire le istruzioni correlate alle transazioni non sono necessarie autorizzazioni specifiche. Le autorizzazioni sono necessarie per eseguire le istruzioni all'interno della transazione.  
  
## <a name="error-handling"></a>Gestione degli errori  
 Se si eseguono istruzioni COMMIT o ROLLBACK e non è presente alcuna transazione attiva, viene generato un errore.  
  
 Se si esegue un'istruzione BEGIN TRANSACTION mentre è già in corso una transazione, viene generato un errore. Ciò può verificarsi se un'istruzione BEGIN TRANSACTION si verifica dopo un'istruzione BEGIN TRANSACTION con esito positivo o se la sessione è in modalità SET AUTOCOMMIT OFF.  
  
 Se una transazione esplicita non viene eseguita correttamente a causa di un errore non correlato all'esecuzione di un'istruzione, [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] esegue automaticamente il rollback della transazione e libera tutte le risorse usate dalla transazione stessa. Se ad esempio viene interrotta la connessione di rete tra il client e un'istanza di [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] o se il client si disconnette dall'applicazione, quando la rete notifica l'interruzione all'istanza viene eseguito il rollback di tutte le transazioni della connessione di cui non è ancora stato eseguito il commit.  
  
 Se si verifica un errore durante l'esecuzione di un'istruzione in un batch, [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] si comporta in modo coerente con l'impostazione di **XACT_ABORT** su **ON** in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e viene eseguito il rollback dell'intera transazione. Per altre informazioni sull'impostazione **XACT_ABORT**, vedere [SET XACT_ABORT (Transact-SQL)](../statements/set-xact-abort-transact-sql.md).  
  
## <a name="general-remarks"></a>Osservazioni generali  
 In un momento specifico, una sessione può eseguire solo una transazione. I punti di salvataggio e le transazioni annidate non sono supportati.  
  
 È compito del programmatore di [!INCLUDE[DWsql](../../includes/dwsql-md.md)] eseguire l'istruzione COMMIT solo quando tutti i dati a cui la transazione fa riferimento sono logicamente corretti.  
  
 Se una sessione viene terminata prima del completamento di una transazione, viene eseguito il rollback della transazione stessa.  
  
 Le modalità di transazione vengono gestite a livello di sessione. Se, ad esempio, una sessione inizia una transazione esplicita oppure imposta AUTOCOMMIT su OFF o IMPLICIT_TRANSACTIONS su ON, non ha alcun effetto sulle modalità delle transazioni di qualsiasi altra sessione.  
  
## <a name="limitations-and-restrictions"></a>Limitazioni e restrizioni  
 Non è possibile eseguire il rollback di una transazione dopo l'esecuzione di un'istruzione COMMIT. Le modifiche dei dati del database, infatti, sono diventate permanenti.  
  
 Non è possibile usare i comandi [CREATE DATABASE &#40;Azure Synapse Analytics&#41; ](../statements/create-database-transact-sql.md) e [DROP DATABASE &#40;Transact-SQL&#41; ](../../t-sql/statements/drop-database-transact-sql.md) all'interno di una transazione esplicita.  
  
 [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] non ha un meccanismo di condivisione delle transazioni. Ciò comporta il fatto che in qualsiasi momento solo una sessione può eseguire operazioni per una transazione nel sistema.  
  
## <a name="locking-behavior"></a>Comportamento di blocco  
 Per garantire l'integrità delle transazioni e mantenere la coerenza dei database se più utenti accedono simultaneamente ai dati, [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] usa la funzionalità di blocco. Il blocco viene usato sia dalle transazioni implicite che dalle transazioni esplicite. Ogni transazione richiede blocchi di tipo diverso per le risorse, ad esempio per le tabelle o i database di quali dipende. Tutti i blocchi di [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] sono a livello di tabella o superiore. I blocchi impediscono alle altre transazioni di modificare le risorse in modo tale da creare problemi alla transazione che richiede il blocco. Ogni transazione rilascia i propri blocchi quando non ha più una dipendenza dalle risorse bloccate. Le transazioni esplicite mantengono blocchi finché la transazione non viene completata tramite commit o rollback.  
  
## <a name="examples-sssdwfull-and-sspdw"></a>Esempi: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] e [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="a-using-an-explicit-transaction"></a>R. Uso di una transazione esplicita  
  
```sql  
BEGIN TRANSACTION;  
DELETE FROM HumanResources.JobCandidate  
    WHERE JobCandidateID = 13;  
COMMIT;  
```  
  
### <a name="b-rolling-back-a-transaction"></a>B. Rollback di una transazione  
 Nell'esempio seguente viene illustrato l'effetto del rollback di una transazione.  In questo esempio l'istruzione ROLLBACK esegue il rollback dell'istruzione INSERT, ma la tabella creata sarà ancora presente.  
  
```sql  
CREATE TABLE ValueTable (id INT);  
BEGIN TRANSACTION;  
       INSERT INTO ValueTable VALUES(1);  
       INSERT INTO ValueTable VALUES(2);  
ROLLBACK;  
```  
  
### <a name="c-setting-autocommit"></a>C. Impostazione di AUTOCOMMIT  
 L'esempio seguente imposta AUTOCOMMIT su `ON`.  
  
```sql  
SET AUTOCOMMIT ON;  
```  
  
 L'esempio seguente imposta AUTOCOMMIT su `OFF`.  
  
```sql  
SET AUTOCOMMIT OFF;  
```  
  
### <a name="d-using-an-implicit-multi-statement-transaction"></a>D. Uso di una transazione implicita con istruzioni multiple  
  
```sql  
SET AUTOCOMMIT OFF;  
CREATE TABLE ValueTable (id INT);  
INSERT INTO ValueTable VALUES(1);  
INSERT INTO ValueTable VALUES(2);  
COMMIT;  
```  
  
## <a name="see-also"></a>Vedere anche  
 [SET IMPLICIT_TRANSACTIONS &#40;Transact-SQL&#41;](../../t-sql/statements/set-implicit-transactions-transact-sql.md)   
 [SET TRANSACTION ISOLATION LEVEL &#40;Transact-SQL&#41;](../../t-sql/statements/set-transaction-isolation-level-transact-sql.md)   
 [@@TRANCOUNT &#40;Transact-SQL&#41;](../../t-sql/functions/trancount-transact-sql.md)  
  
