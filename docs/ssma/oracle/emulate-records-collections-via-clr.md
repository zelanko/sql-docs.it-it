---
title: Emulazione di record e raccolte tramite UDT CLR
description: Illustra il modo in cui il SQL Server Migration Assistant (SSMA) per Oracle utilizza i tipi di dati definiti dall'utente SQL Server CLR (Common Language Runtime) per emulare i record e le raccolte Oracle.
author: nahk-ivanov
ms.prod: sql
ms.technology: ssma
ms.devlang: sql
ms.topic: article
ms.date: 1/22/2020
ms.author: alexiva
ms.openlocfilehash: 73991999cf0a6e7bd2c8cd541ec58a37d1f18f09
ms.sourcegitcommit: e572f1642f588b8c4c75bc9ea6adf4ccd48a353b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2020
ms.locfileid: "84779381"
---
# <a name="emulating-records-and-collections-via-clr-udt"></a>Emulazione di record e raccolte tramite UDT CLR

Questo articolo illustra il modo in cui il SQL Server Migration Assistant (SSMA) per Oracle USA i tipi di dati definiti dall'utente SQL Server CLR (Common Language Runtime) per emulare i record e le raccolte Oracle.

## <a name="declaring-record-or-collection-types-and-variables"></a>Dichiarazione di variabili e tipi di record e di raccolta

SSMA crea tre tipi definiti dall'utente basati su CLR:

* `CollectionIndexInt`
* `CollectionIndexString`
* `Record`

Il `CollectionIndexInt` tipo è concepito per l'emulazione di raccolte indicizzate in base a Integer, ad esempio `VARRAY` s, tabelle nidificate e matrici associative basate su chiavi intere. Il `CollectionIndexString` tipo viene utilizzato per le matrici associativi indicizzate in base ai tasti carattere. La funzionalità di record Oracle è emulata dal `Record` tipo.

Tutte le dichiarazioni dei tipi di record o di raccolta vengono convertite in questa dichiarazione Transact-SQL:

```sql
declare @Collection$TYPE varchar(max) = '<type definition>'
```

`<type definition>`Di seguito è riportato un testo descrittivo che identifica in modo univoco il tipo di origine PL/SQL.

Prendere in considerazione gli esempi seguenti:

```sql
DECLARE
    TYPE Manager IS RECORD
    (
        mgrid integer,
        mgrname varchar2(40),
        hiredate date
    );

    TYPE Manager_table is TABLE OF Manager INDEX BY PLS_INTEGER;

    Mgr_rec Manager;
    Mgr_table_rec Manager_table;
BEGIN
    mgr_rec.mgrid := 1;
    mgr_rec.mgrname := 'Mike';
    mgr_rec.hiredate := sysdate;

    select
        empno,
        ename,
        hiredate
    BULK COLLECT INTO
        mgr_table_rec
    FROM
        emp;
END;
```

Quando viene convertito usando SSMA, diventerà il codice Transact-SQL seguente:

```sql
BEGIN
    DECLARE
        @CollectionIndexInt$TYPE varchar(max) =
            ' TABLE INDEX BY INT OF ( RECORD ( MGRID INT , MGRNAME STRING , HIREDATE DATETIME ) )'

    DECLARE
        @Mgr_rec$mgrid int,
        @Mgr_rec$mgrname varchar(40),
        @Mgr_rec$hiredate datetime2(0),
        @Mgr_table_rec dbo.CollectionIndexInt =
            dbo.CollectionIndexInt::[Null].SetType(@CollectionIndexInt$TYPE)

    SET @mgr_rec$mgrid = 1
    SET @mgr_rec$mgrname = 'Mike'
    SET @mgr_rec$hiredate = sysdatetime()

    SET @mgr_table_rec = @mgr_table_rec.RemoveAll()
    SET @mgr_table_rec =
        @mgr_table_rec.AssignData(
            ssma_oracle.fn_bulk_collect2CollectionComplex((
                SELECT
                    CAST(EMP.EMPNO AS int) AS mgrid,
                    EMP.ENAME AS mgrname,
                    EMP.HIREDATE AS hiredate
                FROM dbo.EMP
                FOR XML PATH
            ))
        )
END
```

Qui, poiché la `Manager` tabella è associata a un indice numerico ( `INDEX BY PLS_INTEGER` ), la dichiarazione T-SQL corrispondente utilizzata è di tipo `@CollectionIndexInt$TYPE` . Se la tabella è stata associata a un indice del set di caratteri, ad esempio `VARCHAR2` , la dichiarazione T-SQL corrispondente sarà di tipo `@CollectionIndexString$TYPE` :

```sql
-- Oracle
TYPE Manager_table is TABLE OF Manager INDEX BY VARCHAR2(40);

-- SQL Server
@CollectionIndexString$TYPE varchar(max) =
    ' TABLE INDEX BY STRING OF ( RECORD ( MGRID INT , MGRNAME STRING , HIREDATE DATETIME ) )'
```

La funzionalità di record Oracle è emulata `Record` solo dal tipo.

Ognuno dei tipi,, `CollectionIndexInt` `CollectionIndexString` e `Record` , ha una proprietà statica che `[Null]` restituisce un'istanza vuota. Il `SetType` metodo viene chiamato per ricevere un oggetto vuoto di un tipo specifico (come illustrato nell'esempio precedente).

## <a name="constructor-call-conversions"></a>Conversioni di chiamata del costruttore

La notazione del costruttore può essere utilizzata solo per le tabelle nidificate e i `VARRAY` , pertanto tutte le chiamate esplicite al costruttore vengono convertite utilizzando il `CollectionIndexInt` tipo. Le chiamate al costruttore vuote vengono convertite tramite chiamata richiamata `SetType` sull'istanza null di `CollectionIndexInt` . La `[Null]` proprietà restituisce l'istanza null. Se il costruttore contiene un elenco di elementi, le chiamate speciali al metodo vengono applicate in sequenza per aggiungere il valore alla raccolta.

Ad esempio:

```sql
-- Oracle

DECLARE
    TYPE nested_type IS TABLE OF VARCHAR2(20);
    TYPE varray_type IS VARRAY(5) OF INTEGER;

    v1 nested_type;
    v2 varray_type;
BEGIN
   v1 := nested_type('Arbitrary','number','of','strings');
   v2 := varray_type(10, 20, 40, 80, 160);
END;

-- SQL Server

BEGIN
    DECLARE
        @CollectionIndexInt$TYPE varchar(max) = ' VARRAY OF INT',
        @CollectionIndexInt$TYPE$2 varchar(max) = ' TABLE OF STRING',
        @v1 dbo.CollectionIndexInt,
        @v2 dbo.CollectionIndexInt

    SET @v1 =
        dbo.CollectionIndexInt::[Null]
            .SetType(@CollectionIndexInt$TYPE$2)
            .AddString('Arbitrary')
            .AddString('number')
            .AddString('of')
            .AddString('strings')

   SET @v2 =
       dbo.CollectionIndexInt::[Null]
            .SetType(@CollectionIndexInt$TYPE)
            .AddInt(10)
            .AddInt(20)
            .AddInt(40)
            .AddInt(80)
            .AddInt(160)
END
```

## <a name="referencing-and-assigning-record-and-collection-elements"></a>Riferimento e assegnazione di elementi di record e raccolta

Ognuno dei tipi definiti dall'utente dispone di un set di metodi che utilizzano gli elementi dei vari tipi di dati. Il metodo, ad esempio, `SetDouble` assegna un `float(53)` valore a record o raccolta ed è in `GetDouble` grado di leggere questo valore. Di seguito è riportato l'elenco completo dei metodi:

```sql
GetCollectionIndexInt(@key <KeyType>) returns CollectionIndexInt;
SetCollectionIndexInt(@key <KeyType>, @value CollectionIndexInt) returns <UDT_type>;
GetCollectionIndexString(@key <KeyType>) returns CollectionIndexString;
SetCollectionIndexString(@key <KeyType>, @value CollectionIndexString) returns <UDT_type>;
Record GetRecord(@key <KeyType>) returns Record;
SetRecord(@key <KeyType>, @value Record) returns <UDT_type>;
GetString(@key <KeyType>) returns nvarchar(max);
SetString(@key <KeyType>, @value nvarchar(max)) returns nvarchar(max);
GetDouble(@key <KeyType>) returns float(53);
SetDouble(@key <KeyType>, @value float(53)) returns <UDT_type>;
GetDatetime(@key <KeyType>) returns datetime;
SetDatetime(@key <KeyType>, @value datetime) returns <UDT_type>;
GetVarbinary(@key <KeyType>) returns varbinary(max);
SetVarbinary(@key <KeyType>, @value varbinary(max)) returns <UDT_type>;
SqlDecimal GetDecimal(@key <KeyType>);
SetDecimal(@key <KeyType>, @value numeric) returns <UDT_type>;
GetXml(@key <KeyType>) returns xml;
SetXml(@key <KeyType>, @value xml) returns <UDT_type>;
GetInt(@key <KeyType>) returns bigint;
SetInt(@key <KeyType>, @value bigint) returns <UDT_type>;
```

Questi metodi vengono utilizzati quando si fa riferimento o si assegna un valore a un elemento di una raccolta o di un record.

```sql
-- Oracle
a_collection(i) := 'VALUE';

-- SQL Server
SET @a_collection = @a_collection.SetString(@i, 'VALUE');
```

Quando si convertono istruzioni di assegnazione per raccolte multidimensionali o raccolte con elementi record, SSMA aggiunge i metodi seguenti per fare riferimento a un elemento padre all'interno del metodo set:

```sql
GetOrCreateCollectionIndexInt(@key <KeyType>) returns CollectionIndexInt;
GetOrCreateCollectionIndexString(@key <KeyType>) returns CollectionIndexString;
GetOrCreateRecord(@key <KeyType>) returns Record;
```

Ad esempio, viene creata una raccolta di elementi record in questo modo:

```sql
-- Oracle
DECLARE
    TYPE rec_details IS RECORD (id int, name varchar2(20));
    TYPE ntb1 IS TABLE of rec_details index BY binary_integer;
    c ntb1;
BEGIN
    c(1).id := 1;
END;

-- SQL Server
DECLARE
   @CollectionIndexInt$TYPE varchar(max) =
       ' TABLE INDEX BY INT OF ( RECORD ( ID INT , NAME STRING ) )',
   @c dbo.CollectionIndexInt =
       dbo.CollectionIndexInt::[Null].SetType(@CollectionIndexInt$TYPE)

SET @c = @c.SetRecord(1, @c.GetOrCreateRecord(1).SetInt(N'ID', 1))
```

## <a name="collection-built-in-methods"></a>Metodi predefiniti della raccolta

SSMA usa i seguenti metodi UDT per emulare i metodi predefiniti delle raccolte PL/SQL.

Metodi di raccolta Oracle | `CollectionIndexInt`e `CollectionIndexString` equivalente
--- | ---
COUNT | `Count returns int`
DELETE | `RemoveAll() returns <UDT_type>`
Elimina (n) | `Remove(@index int) returns <UDT_type>`
Elimina (m, n) | `RemoveRange(@indexFrom int, @indexTo int) returns <UDT_type>`
EXISTS | `ContainsElement(@index int) returns bit`
ESTENDERE | `Extend() returns <UDT_type>`
Estendi (n) | `Extend() returns <UDT_type>`
Estendi (n, i) | `ExtendDefault(@count int, @def int) returns <UDT_type>`
FIRST | `First() returns int`
LAST | `Last() returns int`
LIMIT | N/D
PRIOR | `Prior(@current int) returns int`
NEXT | `Next(@current int) returns int`
TRIM | `Trim() returns <UDT_type>`
TRIM (n) | `TrimN(@count int) returns <UDT_type>`

## <a name="bulk-collect-operation"></a>Operazione di raccolta BULK

SSMA converte `BULK COLLECT INTO` le istruzioni in SQL Server `SELECT ... FOR XML PATH` istruzione, il cui risultato è incluso in una delle funzioni seguenti:

* `ssma_oracle.fn_bulk_collect2CollectionSimple`
* `ssma_oracle.fn_bulk_collect2CollectionComplex`

La scelta dipende dal tipo di oggetto di destinazione. Queste funzioni restituiscono valori XML che possono essere analizzati `CollectionIndexInt` dai `CollectionIndexString` `Record` tipi e. Una `AssignData` funzione speciale assegna una raccolta basata su XML al tipo definito dall'utente.

SSMA riconosce tre tipi di `BULK COLLECT INTO` istruzioni.

### <a name="the-collection-contains-elements-with-scalar-types-and-the-select-list-contains-one-column"></a>La raccolta contiene elementi con tipi scalari e l' `SELECT` elenco contiene una colonna

```sql
-- Oracle
SELECT column_name_1
BULK COLLECT INTO <collection_name_1>
FROM <data_source>

-- SQL Server
SET @<collection_name_1> =
    @<collection_name_1>.AssignData(
        ssma_oracle.fn_bulk_collect2CollectionSimple(
            (SELECT column_name_1 FROM <data_source> FOR XML PATH)))
```

### <a name="the-collection-contains-elements-with-record-types-and-the-select-list-contains-one-column"></a>La raccolta contiene elementi con tipi di record e l' `SELECT` elenco contiene una colonna

```sql
-- Oracle
SELECT
    column_name_1[, column_name_2...]
BULK COLLECT INTO
    <collection_name_1>
FROM
    <data_source>

-- SQL Server
SET @<collection_name_1> =
    @<collection_name_1>.AssignData(
        ssma_oracle.fn_bulk_collect2CollectionComplex(
            (SELECT
                column_name_1 as [collection_name_1_element_field_name_1],
                column_name_2 as [collection_name_1_element_field_name_2]
            FROM <data_source>
            FOR XML PATH)))
```

### <a name="the-collection-contains-elements-with-scalar-type-and-the-select-list-contains-multiple-columns"></a>La raccolta contiene elementi con tipo scalare e l' `SELECT` elenco contiene più colonne

```sql
-- Oracle
SELECT
    column_name_1[, column_name_2 ...]
BULK COLLECT INTO
    <collection_name_1>[, <collection_name_2> ...]
FROM
    <data_source>

-- SQL Server
;WITH bulkC AS (
    SELECT
        column_name_1 [collection_name_1_element_field_name_1],
        column_name_2 [collection_name_1_element_field_name_2]
    FROM
        <data_source>
)
SELECT
    @<collection_name_1> =
        @<collection_name_1>.AssignData(
            ssma_oracle.fn_bulk_collect2CollectionSimple(
                (SELECT
                    [collection_name_1_element_field_name_1]
                FROM
                    bulkC
                FOR XML PATH))),
    @<collection_name_2> =
        @<collection_name_2>.AssignData(
            ssma_oracle.fn_bulk_collect2CollectionSimple(
                (SELECT
                    [collection_name_1_element_field_name_2]
                FROM bulkC
                FOR XML PATH)))
```

## <a name="select-into-record"></a>Record SELECT INTO

Quando il risultato della query Oracle viene salvato in una variabile di record PL/SQL, sono disponibili due opzioni, a seconda dell'impostazione di SSMA per **Convert record come elenco di variabili separate** (disponibili nel menu **strumenti** , **Impostazioni progetto**, quindi **General**  ->  **conversione**generale). Se il valore di questa impostazione è **Sì** (impostazione predefinita), SSMA non crea un'istanza del tipo di record. Suddivide invece il record nei campi costitutivi creando una variabile Transact-SQL separata per ogni campo di record. Se l'impostazione è **No**, viene creata un'istanza del record e a ogni campo viene assegnato un valore tramite i `Set` metodi.
