---
title: Supporto di Transact-SQL per OLTP in memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: b1cc7c30-1747-4c21-88ac-e95a5e58baac
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1db4c6895fb499458c198008319302a25b8cd34b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63156223"
---
# <a name="transact-sql-support-for-in-memory-oltp"></a>Supporto di Transact-SQL per OLTP in memoria
  È possibile accedere alle tabelle ottimizzate per la memoria usando qualsiasi query Transact-SQL o istruzione DML sta(SELECT, INSERT, UPDATE o DELETE), query ad hoc e modulo SQL, ad esempio stored procedure, funzioni con valori di tabella, funzioni scalari, trigger e visualizzazioni. Per altre informazioni, vedere [accesso tabelle utilizzando Transact-SQL interpretato](accessing-memory-optimized-tables-using-interpreted-transact-sql.md).  
  
 Le stored procedure che fanno riferimento solo alle tabelle ottimizzate per la memoria possono essere compilate in modo nativo nel codice macchina e in genere forniscono un notevole miglioramento delle prestazioni rispetto alle stored procedure interpretate (basate su disco). Usare le stored procedure compilate in modo nativo per l'accesso alle tabelle ottimizzate per la memoria. Per altre informazioni, vedere [Natively Compiled Stored Procedures](natively-compiled-stored-procedures.md) (Stored procedure compilate in modo nativo).  
  
 Durante la creazione e la modifica di oggetti database (istruzioni DDL) sarà necessario modificare le istruzioni seguenti:  
  
-   [Opzioni ALTER DATABASE File e Filegroup &#40;Transact-SQL&#41; ](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options) (vedere `MEMORY_OPTIMIZED_DATA`)  
  
-   [CREATE DATABASE &#40;SQL Server Transact-SQL&#41; ](/sql/t-sql/statements/create-database-sql-server-transact-sql) (vedere `MEMORY_OPTIMIZED_DATA`)  
  
-   [CREATE PROCEDURE &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-procedure-transact-sql) (vedere `NATIVE_COMPILATION`, `SCHEMABINDING`, `EXECUTE AS`, e `BEGIN ATOMIC`)  
  
-   [CREATE TABLE &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-table-transact-sql) (vedere `MEMORY_OPTIMIZED`, `DURABILITY`, `BUCKET_COUNT`, `INDEX`, e `HASH`)  
  
-   [CREATE TYPE &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-type-transact-sql) (vedere `MEMORY_OPTIMIZED`, `BUCKET_COUNT`, `INDEX`, e `HASH`)  
  
-   [DECLARE @local_variable &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/declare-local-variable-transact-sql) (see `NULL` | `NOT NULL`)  
  
 Le tabelle con ottimizzazione per la memoria supportano vincoli `PRIMARY KEY` e `NOT NULL`. Per informazioni sull'implementazione di vincoli non supportati, vedere [eseguire la migrazione verificare e Foreign Key Constraints](../../database-engine/migrating-check-and-foreign-key-constraints.md).  
  
 Per informazioni su funzionalità non supportate, vedere [Costrutti Transact-SQL non supportati da OLTP in memoria](transact-sql-constructs-not-supported-by-in-memory-oltp.md).  
  
## <a name="in-this-section"></a>In questa sezione  
  
-   [Tipi di dati supportati](supported-data-types-for-in-memory-oltp.md)  
  
-   [Accesso alle tabelle con ottimizzazione per la memoria utilizzando codice Transact-SQL interpretato](accessing-memory-optimized-tables-using-interpreted-transact-sql.md)  
  
-   [Viste di sistema, stored procedure, tipi di attesa e DMV per OLTP in memoria](../../database-engine/system-views-stored-procedures-dmvs-and-wait-types-for-in-memory-oltp.md)  
  
## <a name="see-also"></a>Vedere anche  
 [OLTP in memoria &#40;ottimizzazione per la memoria&#41;](in-memory-oltp-in-memory-optimization.md)   
 [Problemi di migrazione relativi alle stored procedure compilate in modo nativo](migration-issues-for-natively-compiled-stored-procedures.md)   
 [Funzionalità supportate di SQL Server](unsupported-sql-server-features-for-in-memory-oltp.md)   
 [Stored procedure compilate in modo nativo](natively-compiled-stored-procedures.md)  
  
  
