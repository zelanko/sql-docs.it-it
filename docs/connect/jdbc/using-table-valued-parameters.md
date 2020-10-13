---
title: Uso di parametri con valori di tabella
description: I parametri con valori di tabella rappresentano un modo efficiente per inviare più righe di dati da un client a SQL Server in un singolo comando con parametri.
ms.custom: ''
ms.date: 11/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3af61054-a886-4e1a-ad85-93f87c6d3584
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eac620d522408ff9fb4de5550d92cfcbd0f3ec4a
ms.sourcegitcommit: c7f40918dc3ecdb0ed2ef5c237a3996cb4cd268d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/05/2020
ms.locfileid: "91727472"
---
# <a name="using-table-valued-parameters"></a>Uso di parametri con valori di tabella

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

I parametri con valori di tabella offrono un modo semplice per effettuare il marshalling di più righe di dati da un'applicazione client di SQL Server senza richiedere più round trip o una logica speciale sul lato server per l'elaborazione dei dati. I parametri con valori di tabella possono essere usati per incapsulare le righe di dati in un'applicazione client e inviare i dati al server in un singolo comando con parametri. Le righe di dati in ingresso vengono archiviate in una variabile di tabella su cui è possibile operare tramite Transact-SQL.  
  
I valori di colonna nei parametri con valori di tabella sono accessibili tramite istruzioni Transact-SQL SELECT standard. I parametri con valori di tabella sono fortemente tipizzati e la convalida della relativa struttura è automatica. La dimensione dei parametri con valori di tabella è limitata solo dalla memoria del server.  
  
> [!NOTE]  
> Il supporto per i parametri con valori di tabella è disponibile a partire da Microsoft JDBC Driver 6.0 per SQL Server.
>
> Non è possibile restituire dati in un parametro con valori di tabella. I parametri con valori di tabella sono di solo input; la parola chiave OUTPUT non è supportata.  
  
 Per altre informazioni sui parametri con valori di tabella, vedere le risorse seguenti.  
  
| Risorsa                                                                                                             | Descrizione                                                                         |
| -------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| [Parametri con valori di tabella (Motore di database)](/previous-versions/sql/sql-server-2008/bb510489(v=sql.100)) nella documentazione online di SQL Server | Viene descritto come creare e usare parametri con valori di tabella                             |
| [Tipi di tabella definiti dall'utente](/previous-versions/sql/sql-server-2008/bb522526(v=sql.100)) nella documentazione online di SQL Server                  | Vengono descritti i tipi di tabella definiti dall'utente usati per dichiarare parametri con valori di tabella |
| Sezione relativa al [Motore di database di Microsoft SQL Server](https://go.microsoft.com/fwlink/?LinkId=120507) di CodePlex        | Sono inclusi esempi che illustrano come usare le funzionalità di SQL Server  |
  
## <a name="passing-multiple-rows-in-previous-versions-of-sql-server"></a>Passaggio di più righe nelle versioni precedenti di SQL Server  

Prima dell'introduzione dei parametri con valori di tabella in SQL Server 2008, le opzioni per passare più righe di dati a una stored procedure o a un comando SQL con parametri erano limitate. Uno sviluppatore può scegliere tra le opzioni seguenti per passare più righe al server:  
  
- usare una serie di parametri singoli per rappresentare i valori in più colonne e righe di dati. La quantità di dati che è possibile passare usando questo metodo è limitata dal numero di parametri consentiti. Le stored procedure di SQL Server possono includere al massimo 2100 parametri. La logica lato server è necessaria per assemblare questi singoli valori in una variabile di tabella o in una tabella temporanea per l'elaborazione.  
  
- Aggregare più valori di dati in stringhe delimitate o in documenti XML, quindi passare i valori di testo a una procedura o a un'istruzione. Questa operazione richiede che la routine o l'istruzione includa la logica necessaria per convalidare le strutture dei dati e disaggregare i valori.  
  
- Creare una serie di singole istruzioni SQL per le modifiche ai dati che interessano più righe. È possibile inviare le modifiche al server singolarmente o in batch in gruppi. Tuttavia, anche in caso di invio in batch contenenti più istruzioni, ogni istruzione viene eseguita separatamente sul server.  
  
- Usare il programma di utilità bcp o [SQLServerBulkCopy](using-bulk-copy-with-the-jdbc-driver.md) per caricare molte righe di dati in una tabella. Sebbene questa tecnica sia molto efficiente, non supporta l'elaborazione sul lato server, a meno che i dati non vengano caricati in una tabella temporanea o in una variabile di tabella.
  
## <a name="creating-table-valued-parameter-types"></a>Creazione dei tipi di parametro con valori di tabella  

I parametri con valori di tabella sono basati su strutture di tabella fortemente tipizzate definite tramite istruzioni Transact-SQL `CREATE TYPE`. Per poter usare i parametri con valori di tabella nelle applicazioni client, è prima necessario creare un tipo di tabella e definire la struttura in SQL Server. Per altre informazioni sulla creazione di tipi di tabella, vedere [Tipi di tabella definiti](/previous-versions/sql/sql-server-2008/bb522526(v=sql.100)) dall'utente nella documentazione online di SQL Server.  

```sql
CREATE TYPE dbo.CategoryTableType AS TABLE  
    ( CategoryID int, CategoryName nvarchar(50) )  
```

Dopo aver creato un tipo di tabella, è possibile dichiarare i parametri con valori di tabella in base a tale tipo. Nel frammento Transact-SQL seguente viene illustrato come dichiarare un parametro con valori di tabella in una definizione di stored procedure. Si noti che la parola chiave `READONLY` è obbligatoria per dichiarare un parametro con valori di tabella.  

```sql
CREATE PROCEDURE usp_UpdateCategories
    (@tvpNewCategories dbo.CategoryTableType READONLY)  
```

## <a name="modifying-data-with-table-valued-parameters-transact-sql"></a>Modifica di dati con parametri con valori di tabella (Transact-SQL)  

I parametri con valori di tabella possono essere usati nelle modifiche ai dati basate su set che interessano più righe eseguendo un'unica istruzione. È possibile, ad esempio, selezionare tutte le righe in un parametro con valori di tabella e inserirle in una tabella di database oppure creare un'istruzione di aggiornamento tramite l'aggiunta di un parametro con valori di tabella alla tabella che si desidera aggiornare.  
  
L'istruzione UPDATE Transact-SQL seguente illustra come usare un parametro con valori di tabella tramite la sua unione in join con la tabella Categories. Quando si usa un parametro con valori di tabella con un JOIN in una clausola FROM, è anche necessario usare un alias per il parametro, come illustrato di seguito, dove per il parametro con valori di tabella viene usato l'alias "ec":  

```sql
UPDATE dbo.Categories  
    SET Categories.CategoryName = ec.CategoryName  
    FROM dbo.Categories INNER JOIN @tvpEditedCategories AS ec  
    ON dbo.Categories.CategoryID = ec.CategoryID;  
```

In questo esempio Transact-SQL viene illustrato come selezionare le righe da un parametro con valori di tabella per eseguire un'istruzione INSERT in una singola operazione basata su set.

```sql
INSERT INTO dbo.Categories (CategoryID, CategoryName)  
    SELECT nc.CategoryID, nc.CategoryName FROM @tvpNewCategories AS nc;  
```

## <a name="limitations-of-table-valued-parameters"></a>Limitazioni dei parametri con valori di tabella

Esistono diverse limitazioni per i parametri con valori di tabella:  
  
- Non è possibile passare i parametri con valori di tabella a funzioni definite dall'utente.  
  
- I parametri con valori di tabella possono essere indicizzati solo per supportare vincoli UNIQUE o PRIMARY KEY. SQL Server non gestisce statistiche su parametri con valori di tabella.  
  
- I parametri con valori di tabella sono di sola lettura nel codice Transact-SQL. Non è possibile aggiornare i valori delle colonne nelle righe di un parametro con valori di tabella e non è possibile inserire o eliminare righe. Per modificare i dati trasferiti a un'istruzione stored procedure o parametrizzata in un parametro con valori di tabella, è necessario inserire i dati in una tabella temporanea o in una variabile di tabella.  
  
- Non è possibile usare le istruzioni ALTER TABLE per modificare la progettazione dei parametri con valori di tabella.

- È possibile eseguire lo streaming di oggetti di grandi dimensioni in un parametro con valori di tabella.  
  
## <a name="configuring-a-table-valued-parameter"></a>Configurazione di un parametro con valori di tabella

A partire da Microsoft JDBC Driver 6.0 per SQL Server, i parametri con valori di tabella sono supportati con un'istruzione con parametri o una stored procedure con parametri. I parametri con valori di tabella possono essere popolati da un SQLServerDataTable, da un ResultSet o da un'implementazione fornita dall'utente dell'interfaccia ISQLServerDataRecord. Quando si imposta un parametro con valori di tabella per una query preparata, è necessario specificare il nome di un tipo che deve corrispondere al nome di un tipo compatibile creato in precedenza sul server.  
  
I due frammenti di codice seguenti illustrano come configurare un parametro con valori di tabella con un SQLServerPreparedStatement e con SQLServerCallableStatement per inserire i dati. Qui sourceTVPObject può essere un SQLServerDataTable o un ResultSet o un oggetto ISQLServerDataRecord. Negli esempi si presuppone che la connessione sia un oggetto connessione attivo.  

```java
// Using table-valued parameter with a SQLServerPreparedStatement.  
SQLServerPreparedStatement pStmt =
    (SQLServerPreparedStatement) connection.prepareStatement("INSERT INTO dbo.Categories SELECT * FROM ?");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceTVPObject);  
pStmt.execute();  
```

```java
// Using table-valued parameter with a SQLServerCallableStatement.  
SQLServerCallableStatement pStmt =
    (SQLServerCallableStatement) connection.prepareCall("exec usp_InsertCategories ?");
pStmt.setStructured(1, "dbo.CategoryTableType", sourceTVPObject);;  
pStmt.execute();  
```

> [!NOTE]  
> Per un elenco completo delle API disponibili per l'impostazione del parametro con valori di tabella, vedere la sezione **API del parametro con valori di tabella per il driver JDBC** riportata di seguito.  
  
## <a name="passing-a-table-valued-parameter-as-a-sqlserverdatatable-object"></a>Passaggio di un parametro con valori di tabella come oggetto SQLServerDataTable  

A partire da Microsoft JDBC Driver 6.0 per SQL Server, la classe SQLServerDataTable rappresenta una tabella in memoria di dati relazionali. In questo esempio viene illustrato come costruire un parametro con valori di tabella da dati in memoria usando l'oggetto SQLServerDataTable. Il codice crea prima di tutto un oggetto SQLServerDataTable, ne definisce lo schema e popola la tabella con i dati. Il codice configura quindi un'istruzione SQLServerPreparedStatement che passa questa tabella di dati come parametro con valori di tabella a SQL Server.  

```java
/* Assumes connection is an active Connection object. */

// Create an in-memory data table.  
SQLServerDataTable sourceDataTable = new SQLServerDataTable();
  
// Define metadata for the data table.  
sourceDataTable.addColumnMetadata("CategoryID" ,java.sql.Types.INTEGER);
sourceDataTable.addColumnMetadata("CategoryName" ,java.sql.Types.NVARCHAR);
  
// Populate the data table.  
sourceDataTable.addRow(1, "CategoryNameValue1");
sourceDataTable.addRow(2, "CategoryNameValue2");
  
// Pass the data table as a table-valued parameter using a prepared statement.  
SQLServerPreparedStatement pStmt =
        (SQLServerPreparedStatement) connection.prepareStatement(  
            "INSERT INTO dbo.Categories SELECT * FROM ?;");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceDataTable);  
pStmt.execute();  
```

> [!NOTE]  
> Per un elenco completo delle API disponibili per l'impostazione del parametro con valori di tabella, vedere la sezione **API del parametro con valori di tabella per il driver JDBC** riportata di seguito.  
  
## <a name="passing-a-table-valued-parameter-as-a-resultset-object"></a>Passaggio di un parametro con valori di tabella come oggetto ResultSet  

In questo esempio viene illustrato come eseguire lo streaming di righe di dati da un ResultSet a un parametro con valori di tabella. Il codice recupera prima di tutto i dati da una tabella di origine in un oggetto SQLServerDataTable, ne definisce lo schema e popola la tabella con i dati. Il codice configura quindi un'istruzione SQLServerPreparedStatement che passa questa tabella di dati come parametro con valori di tabella a SQL Server.  

```java
/* Assumes connection is an active Connection object. */

// Create the source ResultSet object. Here SourceCategories is a table defined with the same schema as Categories table.
ResultSet sourceResultSet = connection.createStatement().executeQuery("SELECT * FROM SourceCategories");  

// Pass the source result set as a table-valued parameter using a prepared statement.  
SQLServerPreparedStatement pStmt =
        (SQLServerPreparedStatement) connection.prepareStatement(  
                "INSERT INTO dbo.Categories SELECT * FROM ?;");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceResultSet);  
pStmt.execute();  
```

> [!NOTE]  
> Per un elenco completo delle API disponibili per l'impostazione del parametro con valori di tabella, vedere la sezione **API del parametro con valori di tabella per il driver JDBC** riportata di seguito.  

## <a name="passing-a-table-valued-parameter-as-an-isqlserverdatarecord-object"></a>Passaggio di un parametro con valori di tabella come oggetto ISQLServerDataRecord  

A partire da Microsoft JDBC Driver 6.0 per SQL Server, è disponibile una nuova interfaccia ISQLServerDataRecord per lo streaming dei dati (a seconda del modo in cui l'utente fornisce l'implementazione) utilizzando un parametro con valori di tabella. Nell'esempio seguente viene illustrato come implementare l'interfaccia ISQLServerDataRecord e come passarla come parametro con valori di tabella. Per semplicità, nell'esempio seguente viene passata solo una riga con valori hardcoded al parametro con valori di tabella. Idealmente, l'utente deve implementare questa interfaccia per eseguire lo streaming di righe da qualsiasi origine, ad esempio da file di testo.  

```java
class MyRecords implements ISQLServerDataRecord  
{  
    int currentRow = 0;  
    Object[] row = new Object[2];  
  
    MyRecords(){  
        // Constructor. This implementation has just one row.
        row[0] = new Integer(1);  
        row[1] = "categoryName1";  
    }  
  
    public int getColumnCount(){  
        // Return the total number of columns, for this example it is 2.  
        return 2;  
    }  
  
    public SQLServerMetaData getColumnMetaData(int columnIndex) {  
        // Return the column metadata.  
        if (1 == columnIndex)  
            return new SQLServerMetaData("CategoryID", java.sql.Types.INTEGER);  
        else  
            return new SQLServerMetaData("CategoryName", java.sql.Types.NVARCHAR);  
    }  
  
    public Object[] getRowData(){  
        // Return the columns in the current row as an array of objects. This implementation has just one row.  
        return row;
    }  
  
    public boolean next(){  
        // Move to the next row. This implementation has just one row, after processing the first row, return false.  
        currentRow++;  
        if (1 == currentRow)  
            return true;  
        else  
            return false;  
    }
}

// Following code demonstrates how to pass MyRecords object as a table-valued parameter.  
MyRecords sourceRecords = new MyRecords();  
SQLServerPreparedStatement pStmt =
        (SQLServerPreparedStatement) connection.prepareStatement(  
                "INSERT INTO dbo.Categories SELECT * FROM ?;");  
pStmt.setStructured(1, "dbo.CategoryTableType", sourceRecords);  
pStmt.execute();  
```

> [!NOTE]  
> Per un elenco completo delle API disponibili per l'impostazione del parametro con valori di tabella, vedere la sezione **API del parametro con valori di tabella per il driver JDBC** riportata di seguito.

## <a name="table-valued-parameter-api-for-the-jdbc-driver"></a>API del parametro con valori di tabella per il driver JDBC

### <a name="sqlservermetadata"></a>SQLServerMetaData

Questa classe rappresenta i metadati per una colonna. Viene utilizzata nell'interfaccia ISQLServerDataRecord per passare i metadati della colonna al parametro con valori di tabella. I metodi in questa classe sono:  

| Nome                                                                                                                                                                             | Descrizione                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| public SQLServerMetaData(String columnName, int sqlType, int precision, int scale, boolean useServerDefault, boolean isUniqueKey, SQLServerSortOrder sortOrder, int sortOrdinal) | Inizializza una nuova istanza di SQLServerMetaData con il nome della colonna, il tipo SQL, la precisione, la scala e il valore predefinito del server specificati. Questo formato del costrutto supporta i parametri con valori di tabella consentendo di specificare se la colonna è univoca nel parametro con valori di tabella, nell'ordinamento per la colonna e nel numero ordinale della colonna di ordinamento. <br/><br/>useServerDefault: specifica se questa colonna deve usare il valore server predefinito. Il valore predefinito è False.<br>isUniqueKey: indica se la colonna nel parametro con valori di tabella è univoca. Il valore predefinito è False.<br>sortOrder: indica il tipo di ordinamento per una colonna. Il valore predefinito è SQLServerSortOrder.Unspecified.<br>sortOrdinal - specifica l'ordinale della colonna di ordinamento. sortOrdinal inizia da 0; il valore predefinito è -1. |
| public SQLServerMetaData( String columnName, int sqlType)                                                                                                                        | Inizializza una nuova istanza di SQLServerMetaData usando il nome della colonna e il tipo SQL.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| public SQLServerMetaData( String columnName, int sqlType, int length)                                                                                                                        | Inizializza una nuova istanza di SQLServerMetaData usando il nome della colonna, il tipo SQL e la lunghezza (per i dati della stringa). La lunghezza viene utilizzata per distinguere stringhe di grandi dimensioni da stringhe con lunghezza inferiore a 4000 caratteri. Introdotta nella versione 7.2 del driver JDBC.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| public SQLServerMetaData( String columnName, int sqlType, int precision, int scale)                                                                                              | Inizializza una nuova istanza di SQLServerMetaData usando il nome della colonna, il tipo SQL, la precisione e la scala.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Public SQLServerMetaData(SQLServerMetaData sqlServerMetaData)                                                                                                                    | Inizializza una nuova istanza di SQLServerMetaData da un altro oggetto SQLServerMetaData.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| public String getColumName()                                                                                                                                                     | Recupera il nome della colonna.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| public int getSqlType()                                                                                                                                                          | Recupera il tipo SQL Java.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| public int getPrecision()                                                                                                                                                        | Recupera la precisione del tipo passato alla colonna.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| public int getScale()                                                                                                                                                            | Recupera la scala del tipo passato alla colonna.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| public SQLServerSortOrder getSortOrder()                                                                                                                                         | Recupera il criterio di ordinamento.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| public int getSortOrdinal()                                                                                                                                                      | Recupera l'ordinale di ordinamento.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| public boolean isUniqueKey()                                                                                                                                                     | Restituisce un valore che indica se la colonna è univoca.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| public boolean useServerDefault()                                                                                                                                                | Restituisce un valore che indica se la colonna usa il valore predefinito del server.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
  
### <a name="sqlserversortorder"></a>SQLServerSortOrder

Enumerazione che definisce l'ordinamento. I valori possibili sono Ascending (Crescente), Descending (Decrescente) e Unspecified (Non specificato).
  
### <a name="sqlserverdatatable"></a>SQLServerDataTable

Questa classe rappresenta una tabella di dati in memoria da utilizzare con i parametri con valori di tabella. I metodi in questa classe sono:  

| Nome                                                          | Descrizione                                          |
| ------------------------------------------------------------- | ---------------------------------------------------- |
| Public SQLServerDataTable()                                   | Inizializza una nuova istanza di SQLServerDataTable.    |
| public Iterator<Entry\<Integer, Object[]>> getIterator()      | Recupera un iteratore nelle righe della tabella dati. |
| public void addColumnMetadata(String columnName, int sqlType) | Aggiunge metadati per la colonna specificata.              |
| public void addColumnMetadata(SQLServerDataColumn column)     | Aggiunge metadati per la colonna specificata.              |
| public void addRow(Object... values)                          | Aggiunge una riga di dati alla tabella dati.              |
| public Map\<Integer, SQLServerDataColumn> getColumnMetadata() | Recupera i metadati della colonna di questa tabella dati.       |
| public void clear()                                           | Cancella questa tabella dati.                              |

### <a name="sqlserverdatacolumn"></a>SQLServerDataColumn

Questa classe rappresenta una colonna della tabella dati in memoria rappresentata da SQLServerDataTable. I metodi in questa classe sono:  

| Nome                                                       | Descrizione                                                                      |
| ---------------------------------------------------------- | -------------------------------------------------------------------------------- |
| public SQLServerDataColumn(String columnName, int sqlType) | Inizializza una nuova istanza di SQLServerDataColumn con il nome della colonna e il tipo. |
| public String getColumnName()                              | Recupera il nome della colonna.                                                       |
| public int getColumnType()                                 | Recupera il tipo della colonna.                                                       |

### <a name="isqlserverdatarecord"></a>ISQLServerDataRecord

Questa classe rappresenta un'interfaccia che gli utenti possono implementare per eseguire lo streaming dei dati a un parametro con valori di tabella. I metodi in questa interfaccia sono:  
  
| Nome                                                    | Descrizione                                                                                             |
| ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| public SQLServerMetaData getColumnMetaData(int column); | Recupera i metadati della colonna dell'indice di colonna specificato.                                               |
| public int getColumnCount();                            | Recupera il numero di colonne totali.                                                                  |
| public Object[] getRowData();                           | Recupera i dati per la riga corrente come matrice di oggetti.                                          |
| public boolean next();                                  | Passa alla riga successiva. Restituisce True se lo spostamento ha esito positivo ed è presente una riga successiva; in caso contrario, false. |

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

A questa classe sono stati aggiunti i metodi seguenti per supportare il passaggio di parametri con valori di tabella.  

| Nome                                                                                                    | Descrizione                                                                                                                                                                                                                                                                                                |
| ------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| public final void setStructured(int parameterIndex, String tvpName, SQLServerDataTable tvpDataTable)    | Popola un parametro con valori di tabella con una tabella di dati. parameterIndex è l'indice del parametro, tvpName è il nome del parametro con valori di tabella e tvpDataTable è l'oggetto tabella dati di origine.                                                                                                          |
| public final void setStructured(int parameterIndex, String tvpName, ResultSet tvpResultSet)             | Popola un parametro con valori di tabella con un ResultSet recuperato da un'altra tabella. parameterIndex è l'indice del parametro, tvpName è il nome del parametro con valori di tabella e tvpResultSet è l'oggetto set di risultati di origine.                                                                               |
| public final void setStructured(int parameterIndex, String tvpName, ISQLServerDataRecord tvpDataRecord) | Popola un parametro con valori di tabella con un oggetto ISQLServerDataRecord. ISQLServerDataRecord viene usato per il flusso di dati e l'utente decide come usarlo. parameterIndex è l'indice del parametro, tvpName è il nome del parametro con valori di tabella e tvpDataRecord è un oggetto ISQLServerDataRecord. |
  
### <a name="sqlservercallablestatement"></a>SQLServerCallableStatement

A questa classe sono stati aggiunti i metodi seguenti per supportare il passaggio di parametri con valori di tabella.  
  
| Nome                                                                                                        | Descrizione                                                                                                                                                                                                                                                                                                                      |
| ----------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| public final void setStructured(String paratemeterName, String tvpName, SQLServerDataTable tvpDataTable)    | Popola un parametro con valori di tabella passato a una stored procedure con una tabella di dati. paratemeterName è il nome del parametro, tvpName è il nome del tipo TVP e tvpDataTable è l'oggetto tabella di dati.                                                                                                                 |
| public final void setStructured(String paratemeterName, String tvpName, ResultSet tvpResultSet)             | Popola un parametro con valori di tabella passato a una stored procedure con un ResultSet recuperato da un'altra tabella. paratemeterName è il nome del parametro, tvpName è il nome del tipo TVP e tvpResultSet è l'oggetto set di risultati di origine.                                                                              |
| public final void setStructured(String paratemeterName, String tvpName, ISQLServerDataRecord tvpDataRecord) | Popola un parametro con valori di tabella passato a una stored procedure con un oggetto ISQLServerDataRecord. ISQLServerDataRecord viene usato per il flusso di dati e l'utente decide come usarlo. paratemeterName è il nome del parametro, tvpName è il nome del tipo TVP e tvpDataRecord è un oggetto ISQLServerDataRecord. |

## <a name="see-also"></a>Vedere anche

[Panoramica del driver JDBC](overview-of-the-jdbc-driver.md)