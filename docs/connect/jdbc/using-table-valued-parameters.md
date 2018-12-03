---
title: Utilizzo di parametri con valori di tabella | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 3af61054-a886-4e1a-ad85-93f87c6d3584
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7fdccffc1ba4b2e1f0fc6c880fb605888e43abb9
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 11/27/2018
ms.locfileid: "52410398"
---
# <a name="using-table-valued-parameters"></a>Uso di parametri con valori di tabella

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

I parametri con valori di tabella offrono un modo semplice per effettuare il marshalling di più righe di dati da un'applicazione client di SQL Server senza richiedere più round trip o una logica speciale sul lato server per l'elaborazione dei dati. I parametri con valori di tabella possono essere usati per incapsulare le righe di dati in un'applicazione client e inviare i dati al server in un singolo comando con parametri. Le righe di dati in ingresso vengono archiviate in una variabile di tabella che può quindi essere utilizzata tramite Transact-SQL.  
  
I valori di colonna nei parametri con valori di tabella accessibili tramite istruzioni Transact-SQL SELECT standard. I parametri con valori di tabella sono fortemente tipizzati e la loro struttura viene convalidata automaticamente. Le dimensioni dei parametri con valori di tabella sono limitata solo dalla memoria del server.  
  
> [!NOTE]  
> Supporto per i parametri con valori di tabella è disponibile a partire da Microsoft JDBC Driver 6.0 per SQL Server.
>
> È possibile restituire i dati in un parametro con valori di tabella. I parametri con valori di tabella sono solo input. la parola chiave OUTPUT non è supportata.  
  
 Per altre informazioni sui parametri con valori di tabella, vedere le risorse seguenti.  
  
| Risorsa                                                                                                             | Descrizione                                                                         |
| -------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| [Parametri con valori di tabella (motore di Database)](https://go.microsoft.com/fwlink/?LinkId=98363) nella documentazione Online di SQL Server | Viene descritto come creare e usare i parametri con valori di tabella                             |
| [Tipi di tabella definiti dall'utente](https://go.microsoft.com/fwlink/?LinkId=98364) nella documentazione Online di SQL Server                  | Vengono descritti i tipi di tabella definito dall'utente che vengono usati per dichiarare i parametri con valori di tabella |
| Il [Microsoft SQL Server Database Engine](https://go.microsoft.com/fwlink/?LinkId=120507) sezione di CodePlex        | Sono inclusi esempi che illustrano come usare funzionalità e caratteristiche di SQL Server  |
  
## <a name="passing-multiple-rows-in-previous-versions-of-sql-server"></a>Passare più righe nelle versioni precedenti di SQL Server  

Prima di parametri con valori di tabella sono stati introdotti in SQL Server 2008, le opzioni per passare più righe di dati a una stored procedure o un comando SQL con parametri erano limitate. Uno sviluppatore può scegliere tra le opzioni seguenti per passare più righe al server:  
  
- Usare una serie di parametri singoli per rappresentare i valori in più colonne e righe di dati. La quantità di dati che possono essere passati usando questo metodo è limitata dal numero di parametri consentiti. Procedure di SQL Server possono includere al massimo 2100 parametri. Per la logica lato server è necessaria per assemblare questi singoli valori in una variabile di tabella o una tabella temporanea per l'elaborazione.  
  
- Aggregare più valori di dati in stringhe delimitate o in documenti XML, quindi passare tali valori di testo a una routine o istruzione. Ciò richiede la routine o l'istruzione includa la logica necessaria per convalidare le strutture di dati e la separazione i valori.  
  
- Creare una serie di istruzioni SQL singole per modifiche ai dati che interessano più righe. Le modifiche possono essere inviate al server individualmente o raggruppate. Tuttavia, anche quando l'invio in batch che contengono più istruzioni, ogni istruzione viene eseguita separatamente nel server.  
  
- Utilizzare il programma di utilità bcp o la [SQLServerBulkCopy](https://msdn.microsoft.com/library/system.data.sqlclient.sqlbulkcopy(v=vs.110).aspx) oggetto per caricare numerose righe di dati in una tabella. Sebbene questa tecnica è molto efficiente, non supporta l'elaborazione sul lato server, a meno che i dati vengono caricati in una tabella temporanea o variabile di tabella.  
  
## <a name="creating-table-valued-parameter-types"></a>Creazione di tipi di parametro con valori di tabella  

I parametri con valori di tabella sono basati su strutture di tabella fortemente tipizzate definite tramite Transact-SQL `CREATE TYPE` istruzioni. È necessario creare un tipo di tabella e definire la struttura in SQL Server prima di poter usare i parametri con valori di tabella nelle applicazioni client. Per altre informazioni sulla creazione di tipi di tabella, vedere [tipi di tabella definiti dall'utente](https://go.microsoft.com/fwlink/?LinkID=98364) nella documentazione Online di SQL Server.  

```sql
CREATE TYPE dbo.CategoryTableType AS TABLE  
    ( CategoryID int, CategoryName nvarchar(50) )  
```

Dopo aver creato un tipo di tabella, è possibile dichiarare i parametri con valori di tabella basati su tale tipo. Nel frammento Transact-SQL seguente viene illustrato come dichiarare un parametro con valori di tabella in una definizione della stored procedure. Si noti che il `READONLY` parola chiave è obbligatoria per la dichiarazione di un parametro con valori di tabella.  

```sql
CREATE PROCEDURE usp_UpdateCategories
    (@tvpNewCategories dbo.CategoryTableType READONLY)  
```

## <a name="modifying-data-with-table-valued-parameters-transact-sql"></a>Modifica di dati con parametri con valori di tabella (Transact-SQL)  

Parametri con valori di tabella possono essere utilizzati nelle modifiche dei dati basata su set che riguardano più righe tramite l'esecuzione di una singola istruzione. Ad esempio, è possibile selezionare tutte le righe in un parametro con valori di tabella e inserirli in una tabella di database oppure è possibile creare un'istruzione update a far parte di un parametro con valori di tabella per la tabella da aggiornare.  
  
L'istruzione UPDATE Transact-SQL seguente viene illustrato come usare un parametro con valori di tabella creando un join con la tabella Categories. Quando si usa un parametro con valori di tabella con un JOIN in una clausola FROM, è necessario anche alias, come illustrato di seguito, dove il parametro con valori di tabella viene usato l'alias "ec":  

```sql
UPDATE dbo.Categories  
    SET Categories.CategoryName = ec.CategoryName  
    FROM dbo.Categories INNER JOIN @tvpEditedCategories AS ec  
    ON dbo.Categories.CategoryID = ec.CategoryID;  
```

In questo esempio di Transact-SQL viene illustrato come selezionare le righe da un parametro con valori di tabella per eseguire un'operazione di inserimento in una singola operazione basata su set.

```sql
INSERT INTO dbo.Categories (CategoryID, CategoryName)  
    SELECT nc.CategoryID, nc.CategoryName FROM @tvpNewCategories AS nc;  
```

## <a name="limitations-of-table-valued-parameters"></a>Limitazioni dei parametri con valori di tabella

Esistono alcune limitazioni per i parametri con valori di tabella:  
  
- È possibile passare i parametri con valori di tabella a funzioni definite dall'utente.  
  
- I parametri con valori di tabella possono essere indicizzati solo per supportare vincoli UNIQUE o PRIMARY KEY. SQL Server non gestisce statistiche su parametri con valori di tabella.  
  
- I parametri con valori di tabella sono di sola lettura nel codice Transact-SQL. Non è possibile aggiornare i valori delle colonne nelle righe di un parametro con valori di tabella e non è possibile inserire o eliminare righe. Per modificare i dati che viene passati a una stored procedure o istruzione con parametri in parametri con valori di tabella, è necessario inserire i dati in una tabella temporanea o in una variabile di tabella.  
  
- È possibile utilizzare istruzioni ALTER TABLE per modificare la progettazione di parametri con valori di tabella.

- È possibile trasmettere oggetti di grandi dimensioni in un parametro con valori di tabella.  
  
## <a name="configuring-a-table-valued-parameter"></a>Configurazione di un parametro con valori di tabella

A partire da Microsoft JDBC Driver 6.0 per SQL Server, sono supportati i parametri con valori di tabella con un'istruzione con parametri o una stored procedure con parametri. I parametri con valori di tabella possono essere compilati da un SQLServerDataTable, da un set di risultati o da un utente fornisce l'implementazione dell'interfaccia ISQLServerDataRecord. Quando si imposta un parametro con valori di tabella per una query preparata, è necessario specificare un nome di tipo che deve corrispondere al nome di un tipo compatibile creato in precedenza nel server.  
  
I frammenti di codice seguenti illustrano come configurare un parametro con valori di tabella con una SQLServerPreparedStatement e con un SQLServerCallableStatement per inserire i dati. Di seguito sourceTVPObject può essere un SQLServerDataTable, o un set di risultati o un oggetto ISQLServerDataRecord. Gli esempi presuppongono la connessione è un oggetto di connessione attivo.  

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
> Nella sezione **API di parametro con valori di tabella per il Driver JDBC** sotto per un elenco completo delle API disponibili per l'impostazione del parametro con valori di tabella.  
  
## <a name="passing-a-table-valued-parameter-as-a-sqlserverdatatable-object"></a>Passaggio di un parametro con valori di tabella come oggetto SQLServerDataTable  

A partire da Microsoft JDBC Driver 6.0 per SQL Server, la classe di SQLServerDataTable rappresenta una tabella in memoria dei dati relazionali. In questo esempio viene illustrato come costruire un parametro con valori di tabella dai dati in memoria usando l'oggetto SQLServerDataTable. Il codice prima di tutto crea un oggetto SQLServerDataTable, definisce lo schema e popola la tabella con i dati. Il codice viene quindi configurato un SQLServerPreparedStatement che passa questa tabella di dati come parametro con valori di tabella in SQL Server.  

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
> Nella sezione **API di parametro con valori di tabella per il Driver JDBC** sotto per un elenco completo delle API disponibili per l'impostazione del parametro con valori di tabella.  
  
## <a name="passing-a-table-valued-parameter-as-a-resultset-object"></a>Passando un parametro con valori di tabella come un oggetto ResultSet  

In questo esempio viene illustrato come trasmettere righe di dati da un set di risultati a un parametro con valori di tabella. Il codice recupera i dati da una tabella di origine in un crea un oggetto SQLServerDataTable, definisce lo schema e popola la tabella con i dati. Il codice viene quindi configurato un SQLServerPreparedStatement che passa questa tabella di dati come parametro con valori di tabella in SQL Server.  

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
> Nella sezione **API di parametro con valori di tabella per il Driver JDBC** sotto per un elenco completo delle API disponibili per l'impostazione del parametro con valori di tabella.  

## <a name="passing-a-table-valued-parameter-as-an-isqlserverdatarecord-object"></a>Passaggio di un parametro con valori di tabella come oggetto ISQLServerDataRecord  

A partire da Microsoft JDBC Driver 6.0 per SQL Server, una nuova interfaccia ISQLServerDataRecord è disponibile per lo streaming dei dati (a seconda del modo in cui l'utente fornisce l'implementazione per tale) usando un parametro con valori di tabella. Nell'esempio seguente viene illustrato come implementare l'interfaccia ISQLServerDataRecord e passarlo come parametro con valori di tabella. Per semplicità, nell'esempio seguente passa una sola riga con valori hardcoded per il parametro con valori di tabella. In teoria, l'utente potrebbe implementare questa interfaccia per trasmettere righe da qualsiasi origine, ad esempio da file di testo.  

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
> Nella sezione **API di parametro con valori di tabella per il Driver JDBC** sotto per un elenco completo delle API disponibili per l'impostazione del parametro con valori di tabella.

## <a name="table-valued-parameter-api-for-the-jdbc-driver"></a>Parametro con valori di tabella API per il Driver JDBC

### <a name="sqlservermetadata"></a>SQLServerMetaData

Questa classe rappresenta i metadati per una colonna. Utilizzato nell'interfaccia ISQLServerDataRecord per passare i metadati della colonna per il parametro con valori di tabella. I metodi in questa classe sono:  

| nome                                                                                                                                                                             | Descrizione                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| pubblica SQLServerMetaData (columnName stringa sqlType int, int mobile e precisione, scala int, useServerDefault booleano, isUniqueKey booleano, sortOrder SQLServerSortOrder sortOrdinal int) | Inizializza una nuova istanza della SQLServerMetaData con il nome della colonna specificata, tipo sql, precisione, scala e il server predefinito. Questo formato del costruttore supporta i parametri con valori di tabella, consentendo di specificare se la colonna è univoca nel parametro con valori di tabella, l'ordinamento per la colonna e il numero ordinale della colonna di ordinamento. <br/><br/>useServerDefault - specifica se questa colonna deve utilizzare il valore server predefinito. Valore predefinito è false.<br>isUniqueKey - indica se la colonna nel parametro con valori di tabella è univoca. Valore predefinito è false.<br>sortOrder - indica l'ordinamento per una colonna. Valore predefinito è SQLServerSortOrder.Unspecified.<br>sortOrdinal - specifica l'ordinale della colonna di ordinamento; sortOrdinal inizia da 0. Valore predefinito è -1. |
| pubblica SQLServerMetaData (columnName String, int sqlType)                                                                                                                        | Inizializza una nuova istanza della SQLServerMetaData utilizzando il nome della colonna e il tipo sql.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     |
| pubblica SQLServerMetaData (columnName stringa, sqlType int, int precisione, scala int)                                                                                              | Inizializza una nuova istanza della SQLServerMetaData usando il nome della colonna, tipo sql, precisione e scala.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| Pubblica SQLServerMetaData (SQLServerMetaData sqlServerMetaData)                                                                                                                    | Inizializza una nuova istanza della SQLServerMetaData da un altro oggetto SQLServerMetaData.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                      |
| pubblica getColumName() stringa                                                                                                                                                     | Recupera il nome della colonna.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
| getSqlType() int pubblico                                                                                                                                                          | Recupera il tipo di codice sql java.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| getPrecision() int pubblico                                                                                                                                                        | Recupera la precisione del tipo passato alla colonna.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| getScale() int pubblico                                                                                                                                                            | Recupera la scala del tipo passato alla colonna.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| pubblica SQLServerSortOrder getSortOrder()                                                                                                                                         | Recupera l'ordinamento.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| getSortOrdinal() int pubblico                                                                                                                                                      | Recupera il numero ordinale di ordinamento.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| pubblica isUniqueKey() booleano                                                                                                                                                     | Restituisce se la colonna è univoca.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| pubblica useServerDefault() booleano                                                                                                                                                | Monitorare se restituisce la colonna utilizza il valore server predefinito.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
  
### <a name="sqlserversortorder"></a>SQLServerSortOrder

Un'enumerazione che definisce l'ordinamento. I valori possibili sono Ascending, Descending e non specificato.
  
### <a name="sqlserverdatatable"></a>SQLServerDataTable

Questa classe rappresenta una tabella di dati in memoria da usare con i parametri con valori di tabella. I metodi in questa classe sono:  

| nome                                                          | Descrizione                                          |
| ------------------------------------------------------------- | ---------------------------------------------------- |
| SQLServerDataTable() pubblico                                   | Inizializza una nuova istanza di SQLServerDataTable.    |
| Iterator pubblici < voce\<Integer, Object [] >> getIterator()      | Recupera un iteratore sulle righe della tabella dati. |
| pubblica addColumnMetadata void (columnName String, int sqlType) | Aggiunge i metadati per la colonna specificata.              |
| public void addColumnMetadata (SQLServerDataColumn colonna)     | Aggiunge i metadati per la colonna specificata.              |
| public void addRow (valori dell'oggetto...)                          | Aggiunge una riga di dati alla tabella dati.              |
| Mappa pubblica\<Integer, SQLServerDataColumn > getColumnMetadata() | Recupera i metadati di colonna della tabella dati.       |
| pubblica Clear (void)                                           | Cancella questa tabella dati.                              |

### <a name="sqlserverdatacolumn"></a>SQLServerDataColumn

Questa classe rappresenta una colonna della tabella di dati in memoria rappresentata da SQLServerDataTable. I metodi in questa classe sono:  

| nome                                                       | Descrizione                                                                      |
| ---------------------------------------------------------- | -------------------------------------------------------------------------------- |
| pubblica SQLServerDataColumn (columnName String, int sqlType) | Inizializza una nuova istanza della SQLServerDataColumn con il nome della colonna e il tipo. |
| pubblica getColumnName() stringa                              | Recupera il nome della colonna.                                                       |
| getColumnType() int pubblico                                 | Recupera il tipo di colonna.                                                       |

### <a name="isqlserverdatarecord"></a>ISQLServerDataRecord

Questa classe rappresenta un'interfaccia che gli utenti possono implementare un flusso di dati a un parametro con valori di tabella. I metodi in questa interfaccia sono:  
  
| nome                                                    | Descrizione                                                                                             |
| ------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| pubblica SQLServerMetaData getColumnMetaData (int colonna). | Recupera i metadati di colonna dell'indice della colonna specificata.                                               |
| int pubblico getColumnCount();                            | Recupera il numero totale di colonne.                                                                  |
| Pubblica oggetti [] getRowData();                           | Recupera i dati per la riga corrente come matrice di oggetti.                                          |
| pubblica booleano Next ();                                  | Passa alla riga successiva. Restituisce True se lo spostamento ha esito positivo ed è presente una riga successiva, false in caso contrario. |

### <a name="sqlserverpreparedstatement"></a>SQLServerPreparedStatement

I metodi seguenti sono stati aggiunti a questa classe per supportare il passaggio di parametri con valori di tabella.  

| nome                                                                                                    | Descrizione                                                                                                                                                                                                                                                                                                |
| ------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| pubblica setStructured void finale (parametro parameterIndex int, stringa tvpName, SQLServerDataTable tvpDataTable)    | Consente di popolare un parametro con valori di tabella con una tabella di dati. parametro parameterIndex è l'indice del parametro, tvpName è il nome del parametro con valori di tabella e tvpDataTable è l'oggetto tabella di origine dati.                                                                                                          |
| pubblica setStructured void finale (parametro parameterIndex int, stringa tvpName, tvpResultSet ResultSet)             | Popola un parametro con valori di tabella con un set di risultati recuperato dalla tabella anther. parametro parameterIndex è l'indice del parametro, tvpName è il nome del parametro con valori di tabella e tvpResultSet è l'oggetto set di risultati di origine.                                                                               |
| pubblica setStructured void finale (parametro parameterIndex int, stringa tvpName, ISQLServerDataRecord tvpDataRecord) | Consente di popolare un parametro con valori di tabella con un oggetto ISQLServerDataRecord. ISQLServerDataRecord viene usato per i dati di streaming e l'utente decide come usarlo. parametro parameterIndex è l'indice del parametro, tvpName è il nome del parametro con valori di tabella e tvpDataRecord è un oggetto ISQLServerDataRecord. |
  
### <a name="sqlservercallablestatement"></a>SQLServerCallableStatement

I metodi seguenti sono stati aggiunti a questa classe per supportare il passaggio di parametri con valori di tabella.  
  
| nome                                                                                                        | Descrizione                                                                                                                                                                                                                                                                                                                      |
| ----------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| pubblica setStructured void finale (paratemeterName stringa, stringa tvpName, SQLServerDataTable tvpDataTable)    | Consente di popolare un parametro con valori di tabella passato a una stored procedure con una tabella di dati. paratemeterName è il nome del parametro e tvpName è il nome del tipo TVP tvpDataTable è l'oggetto tabella di dati.                                                                                                                 |
| pubblica setStructured void finale (paratemeterName stringa, stringa tvpName, tvpResultSet ResultSet)             | Consente di popolare un parametro con valori di tabella passato a una stored procedure con un set di risultati recuperato da un'altra tabella. paratemeterName è il nome del parametro e tvpName è il nome del tipo TVP tvpResultSet è l'oggetto set di risultati di origine.                                                                              |
| pubblica setStructured void finale (paratemeterName stringa, stringa tvpName, ISQLServerDataRecord tvpDataRecord) | Consente di popolare un parametro con valori di tabella passato a una stored procedure con un oggetto ISQLServerDataRecord. ISQLServerDataRecord viene usato per i dati di streaming e l'utente decide come usarlo. paratemeterName è il nome del parametro e tvpName è il nome del tipo TVP tvpDataRecord è un oggetto ISQLServerDataRecord. |

## <a name="see-also"></a>Vedere anche

[Panoramica del driver JDBC](../../connect/jdbc/overview-of-the-jdbc-driver.md)  
