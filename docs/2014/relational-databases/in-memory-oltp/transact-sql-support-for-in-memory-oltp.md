---
title: Supporto di Transact-SQL per OLTP in memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: b1cc7c30-1747-4c21-88ac-e95a5e58baac
author: rothja
ms.author: jroth
ms.openlocfilehash: bf3708a258e3bb97231e45b10bea2c59351a06a2
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85025487"
---
# <a name="transact-sql-support-for-in-memory-oltp"></a>Supporto di Transact-SQL per OLTP in memoria
  È possibile accedere alle tabelle ottimizzate per la memoria usando qualsiasi query Transact-SQL o istruzione DML sta(SELECT, INSERT, UPDATE o DELETE), query ad hoc e modulo SQL, ad esempio stored procedure, funzioni con valori di tabella, funzioni scalari, trigger e visualizzazioni. Per altre informazioni, vedere [accesso alle tabelle ottimizzate per la memoria usando Transact-SQL interpretato](accessing-memory-optimized-tables-using-interpreted-transact-sql.md).  
  
 Le stored procedure che fanno riferimento solo alle tabelle ottimizzate per la memoria possono essere compilate in modo nativo nel codice macchina e in genere forniscono un notevole miglioramento delle prestazioni rispetto alle stored procedure interpretate (basate su disco). Usare le stored procedure compilate in modo nativo per l'accesso alle tabelle ottimizzate per la memoria. Per altre informazioni, vedere [Natively Compiled Stored Procedures](natively-compiled-stored-procedures.md) (Stored procedure compilate in modo nativo).  
  
 Durante la creazione e la modifica di oggetti database (istruzioni DDL) sarà necessario modificare le istruzioni seguenti:  
  
-   [Opzioni per file e filegroup ALTER DATABASE &#40;&#41;Transact-SQL](/sql/t-sql/statements/alter-database-transact-sql-file-and-filegroup-options) (vedere `MEMORY_OPTIMIZED_DATA` )  
  
-   [Creazione di &#40;di DATABASE SQL Server&#41;Transact-SQL](/sql/t-sql/statements/create-database-sql-server-transact-sql) (vedere `MEMORY_OPTIMIZED_DATA` )  
  
-   [Create procedure &#40;&#41;Transact-SQL](/sql/t-sql/statements/create-procedure-transact-sql) (vedere `NATIVE_COMPILATION` , `SCHEMABINDING` , `EXECUTE AS` e `BEGIN ATOMIC` )  
  
-   [Create Table &#40;&#41;Transact-SQL](/sql/t-sql/statements/create-table-transact-sql) (vedere `MEMORY_OPTIMIZED` ,,, `DURABILITY` `BUCKET_COUNT` `INDEX` e `HASH` )  
  
-   [Crea tipo &#40;&#41;Transact-SQL](/sql/t-sql/statements/create-type-transact-sql) (vedere `MEMORY_OPTIMIZED` , `BUCKET_COUNT` , `INDEX` e `HASH` )  
  
-   [Dichiarare @local_variable &#40;&#41;Transact-SQL](/sql/t-sql/language-elements/declare-local-variable-transact-sql) (vedere `NULL`  |  `NOT NULL` )  
  
 Le tabelle con ottimizzazione per la memoria supportano vincoli `PRIMARY KEY` e `NOT NULL`. Per informazioni sull'implementazione di vincoli non supportati, vedere [migrazione dei vincoli check e Foreign Key](../../database-engine/migrating-check-and-foreign-key-constraints.md).  
  
 Per informazioni su funzionalità non supportate, vedere [Costrutti Transact-SQL non supportati da OLTP in memoria](transact-sql-constructs-not-supported-by-in-memory-oltp.md).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Tipi di dati supportati](supported-data-types-for-in-memory-oltp.md)  
  
-   [Accesso alle tabelle con ottimizzazione per la memoria utilizzando codice Transact-SQL interpretato](accessing-memory-optimized-tables-using-interpreted-transact-sql.md)  
  
-   [Viste di sistema, stored procedure, tipi di attesa e DMV per OLTP in memoria](../../database-engine/system-views-stored-procedures-dmvs-and-wait-types-for-in-memory-oltp.md)  
  
## <a name="see-also"></a>Vedere anche  
 [OLTP in memoria &#40;l'ottimizzazione in memoria&#41;](in-memory-oltp-in-memory-optimization.md)   
 [Problemi di migrazione per le stored procedure compilate in modo nativo](migration-issues-for-natively-compiled-stored-procedures.md)   
 [Funzionalità di SQL Server supportate](unsupported-sql-server-features-for-in-memory-oltp.md)   
 [stored procedure compilate in modo nativo](natively-compiled-stored-procedures.md)  
  
  
