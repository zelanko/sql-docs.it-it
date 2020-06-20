---
title: Usare parametri con valori di tabella (motore di database) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
f1_keywords:
- DECLARE
- CREATE TYPE
helpviewer_keywords:
- table-valued parameters
- table-valued parameters, about table-valued parameters
- parameters [SQL Server], table-valued
- TVP See table-valued parameters
ms.assetid: 5e95a382-1e01-4c74-81f5-055612c2ad99
author: stevestein
ms.author: sstein
ms.openlocfilehash: fa7013fddc6b2ce12ad9ad0f9fcb511d93915e05
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85002860"
---
# <a name="use-table-valued-parameters-database-engine"></a>Utilizzare parametri con valori di tabella (Motore di database)
  I parametri con valori di tabella vengono dichiarati utilizzando tipi di tabella definiti dall'utente. I parametri con valori di tabella consentono di inviare più righe di dati a un'istruzione o a una routine [!INCLUDE[tsql](../../includes/tsql-md.md)] , ad esempio una stored procedure o una funzione, senza creare una tabella temporanea o molti parametri.  
  
 I parametri con valori di tabella sono analoghi alle matrici di parametri in OLE DB e ODBC, ma offrono più flessibilità e maggiore integrazione con [!INCLUDE[tsql](../../includes/tsql-md.md)]. Un ulteriore vantaggio consiste nel fatto che tali parametri possono essere utilizzati in operazioni basate su set.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] passa i parametri con valori di tabella alle routine per riferimento in modo da evitare l'esecuzione di una copia dei dati di input. È possibile creare ed eseguire routine [!INCLUDE[tsql](../../includes/tsql-md.md)] con parametri con valori di tabella e chiamarle da codice [!INCLUDE[tsql](../../includes/tsql-md.md)] o client gestiti o nativi in qualsiasi linguaggio gestito.  
  
 **Contenuto dell'argomento:**  
  
 [Vantaggi](#Benefits)  
  
 [Restrizioni](#Restrictions)  
  
 [Parametri con valori di tabella  e operazioni BULK INSERT](#BulkInsert)  
  
 [Esempio](#Example)  
  
##  <a name="benefits"></a><a name="Benefits"></a> Vantaggi  
 L'ambito di un parametro con valori di tabella è costituito dalla stored procedure, dalla funzione o dal testo [!INCLUDE[tsql](../../includes/tsql-md.md)] dinamico, esattamente come per gli altri parametri. Analogamente, una variabile del tipo di tabella ha lo stesso ambito di qualsiasi altra variabile locale creata utilizzando un'istruzione DECLARE. È possibile dichiarare variabili con valori di tabella all'interno di istruzioni [!INCLUDE[tsql](../../includes/tsql-md.md)] dinamiche e passarle come parametri con valori di tabella a stored procedure e funzioni.  
  
 I parametri con valori di tabella offrono maggiore flessibilità e, in alcuni casi, prestazioni migliori rispetto alle tabelle temporanee o ad altre modalità disponibili per passare un elenco di parametri. I parametri con valori di tabella offrono i vantaggi seguenti:  
  
-   Non acquisiscono blocchi per il popolamento iniziale di dati da un client.  
  
-   Forniscono un modello di programmazione semplice.  
  
-   Consentono di includere logica di business complessa in una singola routine.  
  
-   Riducono il numero di round trip al server.  
  
-   Possono avere una struttura di tabella con cardinalità diversa.  
  
-   Sono fortemente tipizzati.  
  
-   Consentono al client di specificare tipo di ordinamento e chiavi univoche.  
  
-   Vengono memorizzati nella cache come una tabella temporanea quando vengono utilizzati in una stored procedure. A partire da [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], anche i parametri con valori di tabella sono memorizzati nella cache per le query con parametri.  
  
##  <a name="restrictions"></a><a name="Restrictions"></a> Restrizioni  
 Ai parametri con valori di tabella si applicano le restrizioni seguenti:  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] non gestisce statistiche su colonne di parametri con valori di tabella.  
  
-   I parametri con valori di tabella devono essere passati come parametri READONLY di input alle routine [!INCLUDE[tsql](../../includes/tsql-md.md)] . Non è possibile eseguire operazioni DML, ad esempio UPDATE, DELETE o INSERT, su un parametro con valori di tabella nel corpo di una routine.  
  
-   Non è possibile utilizzare un parametro con valori di tabella come destinazione di un'istruzione SELECT INTO o INSERT EXEC. Un parametro con valori di tabella può essere incluso nella clausola FROM di un'istruzione SELECT INTO o nella stringa o stored procedure INSERT EXEC.  
  
##  <a name="table-valued-parameters-vs-bulk-insert-operations"></a><a name="BulkInsert"></a>Confronto tra parametri con valori di tabella e operazioni BULK INSERT  
 L'utilizzo di parametri con valori di tabella è confrontabile con altre modalità di utilizzo di variabili basate su set, ma può spesso risultare più rapido nel caso di set di dati di notevoli dimensioni. Rispetto alle operazioni bulk, che comportano costi di avvio maggiori, i parametri con valori di tabella garantiscono livelli di prestazioni ottimali per operazioni di inserimento di non oltre 1.000 righe.  
  
 I parametri con valori di tabella riutilizzati possono sfruttare il vantaggio derivante dalla memorizzazione nella cache della tabella temporanea, che consente di ottenere una migliore scalabilità rispetto alle operazioni BULK INSERT equivalenti. Se si eseguono operazioni di inserimento di righe di entità ridotta, è possibile ottenere vantaggi minimi in termini di prestazioni utilizzando elenchi di parametri o istruzioni batch anziché operazioni BULK INSERT o parametri con valori di tabella. Tali metodi, tuttavia, risultano meno efficaci da programmare e le prestazioni si riducono rapidamente con l'aumentare del numero di righe.  
  
 I parametri con valori di tabella garantiscono livelli di prestazioni analoghi o migliori rispetto all'implementazione di una matrice di parametri equivalente.  
  
##  <a name="example"></a><a name="Example"></a>Esempio  
 Nell'esempio seguente viene utilizzato [!INCLUDE[tsql](../../includes/tsql-md.md)] e viene illustrato come creare un tipo di parametro con valori di tabella, dichiarare una variabile per farvi riferimento, riempire un elenco di parametri e quindi passare i valori a una stored procedure.  
  
```  
USE AdventureWorks2012;  
GO  
  
/* Create a table type. */  
CREATE TYPE LocationTableType AS TABLE   
( LocationName VARCHAR(50)  
, CostRate INT );  
GO  
  
/* Create a procedure to receive data for the table-valued parameter. */  
CREATE PROCEDURE dbo. usp_InsertProductionLocation  
    @TVP LocationTableType READONLY  
    AS   
    SET NOCOUNT ON  
    INSERT INTO AdventureWorks2012.Production.Location  
           (Name  
           ,CostRate  
           ,Availability  
           ,ModifiedDate)  
        SELECT *, 0, GETDATE()  
        FROM  @TVP;  
        GO  
  
/* Declare a variable that references the type. */  
DECLARE @LocationTVP AS LocationTableType;  
  
/* Add data to the table variable. */  
INSERT INTO @LocationTVP (LocationName, CostRate)  
    SELECT Name, 0.00  
    FROM AdventureWorks2012.Person.StateProvince;  
  
/* Pass the table variable data to a stored procedure. */  
EXEC usp_InsertProductionLocation @LocationTVP;  
GO  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Crea tipo &#40;&#41;Transact-SQL](/sql/t-sql/statements/create-type-transact-sql)   
 [DECLARE @local_variable &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/declare-local-variable-transact-sql)   
 [sys. Types &#40;&#41;Transact-SQL](/sql/relational-databases/system-catalog-views/sys-types-transact-sql)   
 [sys. Parameters &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-parameters-transact-sql)   
 [sys. parameter_type_usages &#40;&#41;Transact-SQL](/sql/relational-databases/system-catalog-views/sys-parameter-type-usages-transact-sql)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)   
 [CREATE FUNCTION &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-function-transact-sql)  
  
  
