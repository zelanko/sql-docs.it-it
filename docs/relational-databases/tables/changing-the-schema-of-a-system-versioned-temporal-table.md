---
title: Modifica dello schema di una tabella temporale con controllo delle versioni di sistema | Microsoft Docs
ms.custom: ''
ms.date: 03/28/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 9dbe5a21-9335-4f8b-85fd-9da83df79946
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e9e3cdde5807172ef92f63179a4e9530b1540bfb
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "74165669"
---
# <a name="changing-the-schema-of-a-system-versioned-temporal-table"></a>Modifica dello schema di una tabella temporale con controllo delle versioni di sistema

[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

Usare l'istruzione **ALTER TABLE** per aggiungere, modificare o rimuovere una colonna.

## <a name="examples"></a>Esempi

Di seguito sono riportati alcuni esempi in cui viene modificato lo schema della tabella temporale.

```sql
ALTER TABLE dbo.Department
    ALTER COLUMN DeptName varchar(100);

ALTER TABLE dbo.Department
    ADD WebAddress nvarchar(255) NOT NULL
    CONSTRAINT DF_WebAddress DEFAULT 'www.mycompany.com';

ALTER TABLE dbo.Department
    ADD TempColumn INT;

GO

ALTER TABLE dbo.Department
    DROP COLUMN TempColumn;

/* Setting IsHidden property for period columns.
Use ALTER COLUMN <period_column> DROP HIDDEN to clear IsHidden flag */

ALTER TABLE dbo.Department
    ALTER COLUMN SysStartTime ADD HIDDEN;

ALTER TABLE dbo.Department
    ALTER COLUMN SysEndTime ADD HIDDEN;
```

### <a name="important-remarks"></a>Note importanti

- L'autorizzazione**CONTROL** nelle tabelle correnti e di cronologia è necessaria per modificare lo schema della tabella temporale.
- Durante un'operazione **ALTER TABLE** , il sistema mantiene un blocco dello schema su entrambe le tabelle.
- La modifica dello schema specificata viene propagata alla tabella di cronologia in modo appropriato (a seconda del tipo di modifica).
- Se si aggiunge una colonna non nullable o si altera la colonna esistente in modo che diventi non nullable, è necessario specificare il valore predefinito per le righe esistenti. Il sistema genererà un valore predefinito aggiuntivo con lo stesso valore e lo applicherà alla tabella di cronologia. L'aggiunta di **DEFAULT** a una tabella non vuota è un'operazione di dimensionamento dei dati in tutte le edizioni diverse da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Enterprise Edition, in cui si tratta di un'operazione di metadati.
- L'aggiunta di varchar(max), nvarchar(max), varbinary(max) o colonne XML con i valori predefiniti sarà un'operazione di aggiornamento dati in tutte le edizioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
- Se le dimensioni della riga dopo l'aggiunta delle colonne superano il limite di dimensioni della riga, non è possibile aggiungere nuove colonne online.
- Dopo aver esteso una tabella con una nuova colonna NON NULL, eliminare il vincolo predefinito nella tabella di cronologia in quanto tutte le colonne della tabella vengono popolate automaticamente dal sistema.
- L'opzione online (**WITH (ONLINE = ON**) non ha alcun effetto su **ALTER TABLE ALTER COLUMN** nel caso di una tabella temporale con controllo delle versioni di sistema. La colonna ALTER non viene eseguita come online indipendentemente dal valore che è stato specificato per l'opzione ONLINE.
- È possibile usare **ALTER COLUMN** per modificare la proprietà **IsHidden** per le colonne periodo.
- Non è possibile usare **ALTER** direttamente per le seguenti modifiche dello schema. Per questi tipi di modifiche, impostare **SYSTEM_VERSIONING = OFF**.

  - Aggiunta di una colonna calcolata
  - Aggiunta di una colonna **IDENTITY**
  - Aggiunta di una colonna **SPARSE** o modifica della colonna esistente in **SPARSE**quando la tabella di cronologia è impostata su **DATA_COMPRESSION = PAGE** o **DATA_COMPRESSION = ROW**, ovvero il valore predefinito per la tabella di cronologia.
  - Aggiunta di **COLUMN_SET**
  - Aggiunta di una colonna **ROWGUIDCOL** o modifica della colonna esistente in **ROWGUIDCOL**

L'esempio seguente mostra la modifica dello schema in cui l'impostazione **SYSTEM_VERSIONING = OFF** è comunque necessaria (aggiunta della colonna **IDENTITY** ). Questo esempio disabilita la verifica di coerenza dei dati. Questa verifica non è necessaria quando viene effettuata la modifica dello schema all'interno di una transazione in quanto non possono verificarsi modifiche simultanee dei dati.

```sql
    BEGIN TRAN
        ALTER TABLE [dbo].[CompanyLocation] SET (SYSTEM_VERSIONING = OFF);
        ALTER TABLE [CompanyLocation] ADD Cntr INT IDENTITY (1,1);
        ALTER TABLE [dbo].[CompanyLocationHistory] ADD Cntr INT NOT NULL DEFAULT 0;
        ALTER TABLE [dbo].[CompanyLocation]
    SET
         (
            SYSTEM_VERSIONING = ON
           ( HISTORY_TABLE = [dbo].[CompanyLocationHistory])
         );
    COMMIT ;
```

## <a name="next-steps"></a>Passaggi successivi

- [Tabelle temporali](../../relational-databases/tables/temporal-tables.md)
 [Introduzione alle tabelle temporali con controllo delle versioni di sistema](../../relational-databases/tables/getting-started-with-system-versioned-temporal-tables.md)
- [Gestire la conservazione dei dati cronologici nelle tabelle temporali con controllo delle versioni di sistema](../../relational-databases/tables/manage-retention-of-historical-data-in-system-versioned-temporal-tables.md)
- [Tabelle temporali con controllo delle versioni di sistema con tabelle con ottimizzazione per la memoria](../../relational-databases/tables/system-versioned-temporal-tables-with-memory-optimized-tables.md)
- [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)
- [Creazione di una tabella temporale con controllo delle versioni di sistema](../../relational-databases/tables/creating-a-system-versioned-temporal-table.md)
- [Modifica dei dati in una tabella temporale con controllo delle versioni di sistema](../../relational-databases/tables/modifying-data-in-a-system-versioned-temporal-table.md)
- [Query sui dati in una tabella temporale con controllo delle versioni di sistema](../../relational-databases/tables/querying-data-in-a-system-versioned-temporal-table.md)
- [Arresto del controllo delle versioni di sistema in una tabella temporale con controllo delle versioni di sistema](../../relational-databases/tables/stopping-system-versioning-on-a-system-versioned-temporal-table.md)
