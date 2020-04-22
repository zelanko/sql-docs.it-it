---
title: Uso della copia bulk con il driver JDBC
description: La classe SQLServerBulkCopy consente di scrivere soluzioni di caricamento dei dati in Java, che offrono notevoli vantaggi a livello di prestazioni rispetto alle API JDBC standard.
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 21e19635-340d-49bb-b39d-4867102fb5df
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 945bdaf05c9a10e3ab72b11e0049c6053dd108b5
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/17/2020
ms.locfileid: "81634021"
---
# <a name="using-bulk-copy-with-the-jdbc-driver"></a>Uso della copia bulk con il driver JDBC

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Microsoft SQL Server include una popolare utilità della riga di comando denominata **bcp** per eseguire rapidamente la copia bulk di file di grandi dimensioni in tabelle o viste nei database di SQL Server. La classe SQLServerBulkCopy consente di scrivere soluzioni di codice in Java che offrono funzionalità simili. Esistono altri modi per caricare dati in una tabella di SQL Server (ad esempio, istruzioni INSERT) ma SQLServerBulkCopy offre un significativo vantaggio in termini di prestazioni.  
  
La classe SQLServerBulkCopy può essere utilizzata per scrivere dati solo in tabelle di SQL Server. Tuttavia, l'origine dati non è limitata a SQL Server: può essere usata qualsiasi origine dati, purché i dati possano essere letti con un'implementazione di ResultSet, RowSet o ISQLServerBulkRecord.  
  
Utilizzando la classe SQLServerBulkCopy è possibile eseguire:  
  
- Una singola operazione di copia bulk  
  
- Più operazioni di copia bulk  
  
- Un'operazione di copia bulk con una transazione  
  
> [!NOTE]  
> Quando si utilizza Microsoft JDBC Driver 4.1 per SQL Server o una versione precedente (che non supporta la classe SQLServerBulkCopy), è invece possibile eseguire l'istruzione Transact-SQL BULK INSERT di SQL Server.  
  
## <a name="bulk-copy-example-setup"></a>Installazione di esempio della copia bulk  

La classe SQLServerBulkCopy può essere utilizzata per scrivere dati solo in tabelle di SQL Server. Negli esempi di codice di questo argomento viene usato il database di esempio di SQL Server, AdventureWorks. Per evitare di modificare le tabelle esistenti, gli esempi di codice scrivono i dati in tabelle che è prima necessario creare.  
  
Le tabelle BulkCopyDemoMatchingColumns e BulkCopyDemoDifferentColumns sono entrambe basate sulla tabella Production.Products di AdventureWorks. Negli esempi di codice che utilizzano queste tabelle, i dati vengono aggiunti dalla tabella Production.Products a una di queste tabelle di esempio. La tabella BulkCopyDemoDifferentColumns viene utilizzata quando l'esempio illustra come eseguire il mapping delle colonne dall'origine dati alla tabella di destinazione; BulkCopyDemoMatchingColumns viene utilizzata per la maggior parte degli altri esempi.  
  
Alcuni esempi di codice illustrano come utilizzare una sola classe SQLServerBulkCopy per scrivere in più tabelle. Per questi esempi, vengono utilizzate le tabelle BulkCopyDemoOrderHeader e BulkCopyDemoOrderDetail come tabelle di destinazione. Queste tabelle sono basate sulle tabelle Sales.SalesOrderHeader e Sales.SalesOrderDetail del database AdventureWorks.  
  
> [!NOTE]  
> Gli esempi di codice per SQLServerBulkCopy vengono forniti solo per illustrare la sintassi per l'utilizzo di SQLServerBulkCopy. Se le tabelle di origine e di destinazione si trovano nella stessa istanza di SQL Server, è più semplice e rapido usare un'istruzione Transact-SQL INSERT ... SELECT per copiare i dati.  

### <a name="table-setup"></a>Impostazione delle tabelle  

Per creare le tabelle necessarie per il corretto funzionamento degli esempi di codice, è necessario eseguire le seguenti istruzioni Transact-SQL in un database di SQL Server.  

```sql
USE AdventureWorks  
  
IF EXISTS (SELECT * FROM dbo.sysobjects
 WHERE id = object_id(N'[dbo].[BulkCopyDemoMatchingColumns]')
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoMatchingColumns]  
  
CREATE TABLE [dbo].[BulkCopyDemoMatchingColumns]([ProductID] [int] IDENTITY(1,1) NOT NULL,  
    [Name] [nvarchar](50) NOT NULL,  
    [ProductNumber] [nvarchar](25) NOT NULL,  
 CONSTRAINT [PK_ProductID] PRIMARY KEY CLUSTERED
(  
    [ProductID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects
 WHERE id = object_id(N'[dbo].[BulkCopyDemoDifferentColumns]')
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoDifferentColumns]  
  
CREATE TABLE [dbo].[BulkCopyDemoDifferentColumns]([ProdID] [int] IDENTITY(1,1) NOT NULL,  
    [ProdNum] [nvarchar](25) NOT NULL,  
    [ProdName] [nvarchar](50) NOT NULL,  
 CONSTRAINT [PK_ProdID] PRIMARY KEY CLUSTERED
(  
    [ProdID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobject
 WHERE id = object_id(N'[dbo].[BulkCopyDemoOrderHeader]')
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoOrderHeader]  
  
CREATE TABLE [dbo].[BulkCopyDemoOrderHeader]([SalesOrderID] [int] IDENTITY(1,1) NOT NULL,  
    [OrderDate] [datetime] NOT NULL,  
    [AccountNumber] [nvarchar](15) NULL,  
 CONSTRAINT [PK_SalesOrderID] PRIMARY KEY CLUSTERED
(  
    [SalesOrderID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects
 WHERE id = object_id(N'[dbo].[BulkCopyDemoOrderDetail]')
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoOrderDetail]  
  
CREATE TABLE [dbo].[BulkCopyDemoOrderDetail]([SalesOrderID] [int] NOT NULL,  
    [SalesOrderDetailID] [int] NOT NULL,  
    [OrderQty] [smallint] NOT NULL,  
    [ProductID] [int] NOT NULL,  
    [UnitPrice] [money] NOT NULL,  
 CONSTRAINT [PK_LineNumber] PRIMARY KEY CLUSTERED
(  
    [SalesOrderID] ASC,  
    [SalesOrderDetailID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
```

## <a name="single-bulk-copy-operations"></a>Singole operazioni di copia bulk

L'approccio più semplice per eseguire un'operazione di copia bulk di SQL Server consiste nell'eseguire una singola operazione su un database. Per impostazione predefinita, una copia bulk viene eseguita come un'operazione isolata: l'operazione di copia avviene in modalità non transazionale, senza la possibilità di eseguirne il rollback.  
  
> [!NOTE]  
> Se è necessario eseguire il rollback di una parte o dell'intera operazione di copia bulk quando si verifica un errore, è possibile utilizzare una transazione gestita da SQLServerBulkCopy o eseguire l'operazione di copia bulk in una transazione esistente.  
> Per altre informazioni, vedere [Transazioni e operazioni di copia bulk](#transaction-and-bulk-copy-operations)  
  
 I passaggi generali per eseguire un'operazione di copia bulk sono:  
  
1. Connettersi al server di origine e ottenere i dati da copiare. I dati possono provenire anche da altre origini, se l'origine può essere recuperata da un oggetto ResultSet o un'implementazione di ISQLServerBulkRecord.  
  
2. Connettersi al server di destinazione (a meno che non si desideri che **SQLServerBulkCopy** stabilisca automaticamente una connessione).  
  
3. Creare un oggetto SQLServerBulkCopy, impostando le proprietà necessarie tramite **setBulkCopyOptions**.  
  
4. Chiamare il metodo **setDestinationTableName** per indicare la tabella di destinazione per l'operazione di inserimento bulk.  
  
5. Chiamare uno dei metodi **writeToServer**.  
  
6. Facoltativamente, aggiornare le proprietà mediante **setBulkCopyOptions** e chiamare nuovamente **writeToServer** in base alle esigenze.  
  
7. Chiamare **close** o eseguire il wrapping delle operazioni di copia bulk all'interno di un'istruzione try-with-resources.  
  
> [!CAUTION]  
> È consigliabile che i tipi di dati delle colonne di origine e di destinazione corrispondano. Se i tipi di dati non corrispondono, SQLServerBulkCopy tenta di convertire ogni valore di origine nel tipo di dati di destinazione. Le conversioni possono influire sulle prestazioni, nonché provocare errori imprevisti. Ad esempio, un tipo di dati double può essere convertito in un tipo di dati decimal nella maggior parte dei casi, ma non sempre.  
  
### <a name="example"></a>Esempio

L'applicazione riportata di seguito illustra come caricare i dati utilizzando la classe SQLServerBulkCopy. In questo esempio, viene utilizzato un ResultSet per copiare i dati dalla tabella Production.Product nel database AdventureWorks di SQL Server in una tabella simile dello stesso database.  
  
> [!IMPORTANT]  
> Questo esempio non funzionerà, a meno che non siano state create le tabelle di lavoro come descritto in [Impostazione delle tabelle](#table-setup). Questo codice viene fornito solo per illustrare la sintassi per l'utilizzo di SQLServerBulkCopy. Se le tabelle di origine e di destinazione si trovano nella stessa istanza di SQL Server, è più semplice e rapido usare un'istruzione Transact-SQL INSERT ... SELECT per copiare i dati.  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;

public class BulkCopySingle {
    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";
        String destinationTable = "dbo.BulkCopyDemoMatchingColumns";
        int countBefore, countAfter;
        ResultSet rsSourceData;

        try (Connection sourceConnection = DriverManager.getConnection(connectionUrl);
                Connection destinationConnection = DriverManager.getConnection(connectionUrl);
                Statement stmt = sourceConnection.createStatement();
                SQLServerBulkCopy bulkCopy = new SQLServerBulkCopy(destinationConnection)) {

            // Empty the destination table.
            stmt.executeUpdate("DELETE FROM " + destinationTable);

            // Perform an initial count on the destination table.
            countBefore = getRowCount(stmt, destinationTable);

            // Get data from the source table as a ResultSet.
            rsSourceData = stmt.executeQuery("SELECT ProductID, Name, ProductNumber FROM Production.Product");

            // In real world applications you would
            // not use SQLServerBulkCopy to move data from one table to the other
            // in the same database. This is for demonstration purposes only.

            // Set up the bulk copy object.
            // Note that the column positions in the source
            // table match the column positions in
            // the destination table so there is no need to
            // map columns.
            bulkCopy.setDestinationTableName(destinationTable);

            // Write from the source to the destination.
            bulkCopy.writeToServer(rsSourceData);

            // Perform a final count on the destination
            // table to see how many rows were added.
            countAfter = getRowCount(stmt, destinationTable);
            System.out.println((countAfter - countBefore) + " rows were added.");
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static int getRowCount(Statement stmt,
            String tableName) throws SQLException {
        ResultSet rs = stmt.executeQuery("SELECT COUNT(*) FROM " + tableName);
        rs.next();
        int count = rs.getInt(1);
        rs.close();
        return count;
    }
}
```

### <a name="performing-a-bulk-copy-operation-using-transact-sql"></a>Esecuzione di un'operazione di copia bulk con Transact-SQL

Nell'esempio seguente viene illustrato come utilizzare il metodo executeUpdate per eseguire l'istruzione BULK INSERT.  
  
> [!NOTE]  
> Il percorso del file per l'origine dati è relativo al server. Affinché l'operazione di copia bulk abbia esito positivo, il processo server deve avere accesso a tale percorso.  

```java
try (Connection con = DriverManager.getConnection(connectionUrl);
        Statement stmt = con.createStatement()) {
    // Perform the BULK INSERT
    stmt.executeUpdate(
            "BULK INSERT Northwind.dbo.[Order Details] " + "FROM 'f:\\mydata\\data.tbl' " + "WITH ( FORMATFILE='f:\\mydata\\data.fmt' )");
}
```  

## <a name="multiple-bulk-copy-operations"></a>Più operazioni di copia bulk  

È possibile eseguire più operazioni di copia bulk utilizzando una singola istanza di una classe SQLServerBulkCopy. Se i parametri delle operazioni cambiano tra le copie (ad esempio, il nome della tabella di destinazione), è necessario aggiornarli prima delle chiamate successive a uno dei metodi writeToServer, come illustrato nell'esempio seguente. A meno che non vengano modificati in modo esplicito, tutti i valori delle proprietà rimangono invariati rispetto alla precedente operazione di copia bulk per una determinata istanza.  

> [!NOTE]  
> L'esecuzione di più operazioni di copia bulk utilizzando la stessa istanza di SQLServerBulkCopy in genere è più efficiente rispetto all'utilizzo di un'istanza distinta per ogni operazione.  
  
Se si eseguono più operazioni di copia bulk utilizzando lo stesso oggetto SQLServerBulkCopy, non vi sono restrizioni relativamente al fatto che le informazioni di origine o di destinazione sono uguali o diverse in ogni operazione. È tuttavia necessario assicurarsi che le informazioni di associazione delle colonne siano impostate correttamente ogni volta che si esegue la scrittura nel server.  
  
> [!IMPORTANT]  
> Questo esempio non funzionerà, a meno che non siano state create le tabelle di lavoro come descritto in [Impostazione delle tabelle](#table-setup). Questo codice viene fornito solo per illustrare la sintassi per l'utilizzo di SQLServerBulkCopy. Se le tabelle di origine e di destinazione si trovano nella stessa istanza di SQL Server, è più semplice e rapido usare un'istruzione Transact-SQL INSERT ... SELECT per copiare i dati.  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopyOptions;

public class BulkCopyMultiple {
    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";
        String destinationHeaderTable = "dbo.BulkCopyDemoOrderHeader";
        String destinationDetailTable = "dbo.BulkCopyDemoOrderDetail";
        int countHeaderBefore, countDetailBefore, countHeaderAfter, countDetailAfter;
        ResultSet rsHeader, rsDetail;

        try (Connection sourceConnection1 = DriverManager.getConnection(connectionUrl);
                Connection sourceConnection2 = DriverManager.getConnection(connectionUrl);
                Statement stmt = sourceConnection1.createStatement();
                PreparedStatement preparedStmt1 = sourceConnection1.prepareStatement(
                        "SELECT [SalesOrderID], [OrderDate], [AccountNumber] FROM [Sales].[SalesOrderHeader] WHERE [AccountNumber] = ?;");
                PreparedStatement preparedStmt2 = sourceConnection2.prepareStatement(
                        "SELECT [Sales].[SalesOrderDetail].[SalesOrderID], [SalesOrderDetailID], [OrderQty], [ProductID], [UnitPrice] FROM "
                                + "[Sales].[SalesOrderDetail] INNER JOIN [Sales].[SalesOrderHeader] ON "
                                + "[Sales].[SalesOrderDetail].[SalesOrderID] = [Sales].[SalesOrderHeader].[SalesOrderID] WHERE [AccountNumber] = ?;");
                SQLServerBulkCopy bulkCopy = new SQLServerBulkCopy(connectionUrl);) {

            // Empty the destination tables.
            stmt.executeUpdate("DELETE FROM " + destinationHeaderTable);
            stmt.executeUpdate("DELETE FROM " + destinationDetailTable);

            // Perform an initial count on the destination
            // table with matching columns.
            countHeaderBefore = getRowCount(stmt, destinationHeaderTable);

            // Perform an initial count on the destination
            // table with different column positions.
            countDetailBefore = getRowCount(stmt, destinationDetailTable);

            // Get data from the source table as a ResultSet.
            // The Sales.SalesOrderHeader and Sales.SalesOrderDetail
            // tables are quite large and could easily cause a timeout
            // if all data from the tables is added to the destination.
            // To keep the example simple and quick, a parameter is
            // used to select only orders for a particular account
            // as the source for the bulk insert.
            preparedStmt1.setString(1, "10-4020-000034");
            rsHeader = preparedStmt1.executeQuery();

            // Get the Detail data in a separate connection.
            preparedStmt2.setString(1, "10-4020-000034");
            rsDetail = preparedStmt2.executeQuery();

            // Create the SQLServerBulkCopySQLServerBulkCopy object.
            SQLServerBulkCopyOptions copyOptions = new SQLServerBulkCopyOptions();
            copyOptions.setBulkCopyTimeout(100);
            bulkCopy.setBulkCopyOptions(copyOptions);
            bulkCopy.setDestinationTableName(destinationHeaderTable);

            // Guarantee that columns are mapped correctly by
            // defining the column mappings for the order.
            bulkCopy.addColumnMapping("SalesOrderID", "SalesOrderID");
            bulkCopy.addColumnMapping("OrderDate", "OrderDate");
            bulkCopy.addColumnMapping("AccountNumber", "AccountNumber");

            // Write rsHeader to the destination.
            bulkCopy.writeToServer(rsHeader);

            // Set up the order details destination.
            bulkCopy.setDestinationTableName(destinationDetailTable);

            // Clear the existing column mappings
            bulkCopy.clearColumnMappings();

            // Add order detail column mappings.
            bulkCopy.addColumnMapping("SalesOrderID", "SalesOrderID");
            bulkCopy.addColumnMapping("SalesOrderDetailID", "SalesOrderDetailID");
            bulkCopy.addColumnMapping("OrderQty", "OrderQty");
            bulkCopy.addColumnMapping("ProductID", "ProductID");
            bulkCopy.addColumnMapping("UnitPrice", "UnitPrice");

            // Write rsDetail to the destination.
            bulkCopy.writeToServer(rsDetail);

            // Perform a final count on the destination
            // tables to see how many rows were added.
            countHeaderAfter = getRowCount(stmt, destinationHeaderTable);
            countDetailAfter = getRowCount(stmt, destinationDetailTable);

            System.out.println((countHeaderAfter - countHeaderBefore) + " rows were added to the Header table.");
            System.out.println((countDetailAfter - countDetailBefore) + " rows were added to the Detail table.");
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static int getRowCount(Statement stmt,
            String tableName) throws SQLException {
        ResultSet rs = stmt.executeQuery("SELECT COUNT(*) FROM " + tableName);
        rs.next();
        int count = rs.getInt(1);
        rs.close();
        return count;
    }
}
```

## <a name="transaction-and-bulk-copy-operations"></a>Transazioni e operazioni di copia bulk

 Le operazioni di copia bulk possono essere eseguite come operazioni isolate oppure come parte di una transazione in più passaggi. Quest'ultima opzione consente di eseguire più di un'operazione di copia bulk all'interno della stessa transazione, nonché di eseguire altre operazioni sul database (come inserimenti, aggiornamenti ed eliminazioni), mantenendo comunque la possibilità di eseguire il commit o il rollback dell'intera transazione.  
  
 Per impostazione predefinita, una copia bulk viene eseguita come un'operazione isolata. L'operazione di copia bulk avviene in modalità non transazionale, senza la possibilità di eseguirne il rollback. Se è necessario eseguire il rollback di una parte o dell'intera operazione di copia bulk quando si verifica un errore, è possibile utilizzare una transazione gestita da SQLServerBulkCopy o eseguire l'operazione di copia bulk in una transazione esistente.  
  
### <a name="performing-a-non-transacted-bulk-copy-operation"></a>Esecuzione di un'operazione di copia bulk non transazionale

L'applicazione riportata di seguito illustra cosa accade quando si verifica un errore durante un'operazione di copia bulk non transazionale.  
  
Nell'esempio la tabella di origine e la tabella di destinazione includono una colonna Identity denominata **ProductID**. Il codice innanzitutto prepara la tabella di destinazione eliminando tutte le righe e quindi inserendo una singola riga il cui **ProductID** è presente nella tabella di origine. Per impostazione predefinita, viene generato un nuovo valore per la colonna Identity nella tabella di destinazione per ogni riga aggiunta. In questo esempio, all'apertura della connessione viene invece impostata un'opzione che impone al processo di caricamento bulk di utilizzare i valori Identity della tabella di origine.  
  
L'operazione di copia bulk viene eseguita con la proprietà **BatchSize** impostata su 10. Quando è rilevata la riga non valida, viene generata un'eccezione. In questo primo esempio, l'operazione di copia bulk è non transazionale. Viene eseguito il commit di tutti i batch copiati fino al punto dell'errore. Viene eseguito il rollback del batch che contiene la chiave duplicata e l'operazione di copia bulk viene interrotta prima dell'elaborazione di altri batch.  
  
> [!NOTE]  
> Questo esempio non funzionerà, a meno che non siano state create le tabelle di lavoro come descritto in [Impostazione delle tabelle](#table-setup). Questo codice viene fornito solo per illustrare la sintassi per l'utilizzo di SQLServerBulkCopy. Se le tabelle di origine e di destinazione si trovano nella stessa istanza di SQL Server, è più semplice e rapido usare un'istruzione Transact-SQL INSERT ... SELECT per copiare i dati.  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopyOptions;

public class BulkCopyNonTransacted {
    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";
        String destinationTable = "dbo.BulkCopyDemoMatchingColumns";
        int countBefore, countAfter;
        ResultSet rsSourceData;

        try (Connection sourceConnection = DriverManager.getConnection(connectionUrl);
                Statement stmt = sourceConnection.createStatement();
                SQLServerBulkCopy bulkCopy = new SQLServerBulkCopy(connectionUrl)) {

            // Empty the destination table.
            stmt.executeUpdate("DELETE FROM " + destinationTable);

            // Add a single row that will result in duplicate key
            // when all rows from source are bulk copied.
            // Note that this technique will only be successful in
            // illustrating the point if a row with ProductID = 446
            // exists in the AdventureWorks Production.Products table.
            // If you have made changes to the data in this table, change
            // the SQL statement in the code to add a ProductID that
            // does exist in your version of the Production.Products
            // table. Choose any ProductID in the middle of the table
            // (not first or last row) to best illustrate the result.
            stmt.executeUpdate("SET IDENTITY_INSERT " + destinationTable + " ON;" + "INSERT INTO " + destinationTable
                    + "([ProductID], [Name] ,[ProductNumber]) VALUES(446, 'Lock Nut 23','LN-3416'); SET IDENTITY_INSERT " + destinationTable
                    + " OFF");

            // Perform an initial count on the destination table.
            countBefore = getRowCount(stmt, destinationTable);

            // Get data from the source table as a ResultSet.
            rsSourceData = stmt.executeQuery("SELECT ProductID, Name, ProductNumber FROM Production.Product");

            // Set up the bulk copy object using the KeepIdentity option and BatchSize = 10.
            SQLServerBulkCopyOptions copyOptions = new SQLServerBulkCopyOptions();
            copyOptions.setKeepIdentity(true);
            copyOptions.setBatchSize(10);

            bulkCopy.setBulkCopyOptions(copyOptions);
            bulkCopy.setDestinationTableName(destinationTable);

            // Write from the source to the destination.
            // This should fail with a duplicate key error
            // after some of the batches have been copied.
            try {
                bulkCopy.writeToServer(rsSourceData);
            }
            catch (SQLException e) {
                e.printStackTrace();
            }

            // Perform a final count on the destination
            // table to see how many rows were added.
            countAfter = getRowCount(stmt, destinationTable);
            System.out.println((countAfter - countBefore) + " rows were added.");
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static int getRowCount(Statement stmt,
            String tableName) throws SQLException {
        ResultSet rs = stmt.executeQuery("SELECT COUNT(*) FROM " + tableName);
        rs.next();
        int count = rs.getInt(1);
        rs.close();
        return count;
    }
}
```

### <a name="performing-a-dedicated-build-copy-operation-in-a-transaction"></a>Esecuzione di un'operazione di copia bulk dedicata in una transazione 

Per impostazione predefinita, un'operazione di copia bulk costituisce la propria transazione. Quando si desidera eseguire un'operazione di copia bulk dedicata, creare una nuova istanza di SQLServerBulkCopy con una stringa di connessione. In questo scenario, l'operazione di copia bulk crea e quindi esegue il commit o il rollback della transazione. È possibile specificare esplicitamente l'opzione **UseInternalTransaction** in **SQLServerBulkCopyOptions** per fare in modo che un'operazione di copia bulk venga eseguita nella propria transazione, determinando l'esecuzione di ogni batch dell'operazione di copia bulk all'interno di una transazione distinta.  
  
> [!NOTE]  
> Poiché i diversi batch vengono eseguiti in diverse transazioni, se si verifica un errore durante l'operazione di copia bulk, verrà eseguito il rollback di tutte le righe nel batch corrente, ma le righe dei batch precedenti rimarranno nel database.  
  
Quando si specifica l'opzione **UseInternalTransaction** in **BulkCopyNonTransacted**, l'operazione di copia bulk è inclusa in una transazione esterna di dimensioni maggiori. Quando si verifica l'errore di violazione della chiave primaria, viene eseguito il rollback dell'intera transazione e non vengono aggiunte righe alla tabella di destinazione.

```java
SQLServerBulkCopyOptions copyOptions = new SQLServerBulkCopyOptions();
copyOptions.setKeepIdentity(true);
copyOptions.setBatchSize(10);
copyOptions.setUseInternalTransaction(true);
```

### <a name="using-existing-transactions"></a>Utilizzo di transazioni esistenti

È possibile passare un oggetto connessione che ha transazioni abilitate come parametro in un costruttore SQLServerBulkCopy. In questo caso, l'operazione di copia bulk viene eseguita in una transazione esistente e non viene apportata alcuna modifica allo stato della transazione (ovvero, non ne viene eseguito il commit, né viene interrotta). Questo consente a un'applicazione di includere l'operazione di copia bulk in una transazione con altre operazioni sul database. Se è necessario eseguire il rollback dell'intera copia bulk perché si verifica un errore o se la copia bulk deve essere eseguita come parte di un processo più ampio di cui sia possibile eseguire il rollback, è possibile eseguire il rollback dell'oggetto connessione in qualsiasi momento dopo l'operazione di copia bulk.  
  
La seguente applicazione è simile a **BulkCopyNonTransacted**, con una sola eccezione: in questo esempio, l'operazione di copia bulk è inclusa in una transazione esterna di maggiori dimensioni. Quando si verifica l'errore di violazione della chiave primaria, viene eseguito il rollback dell'intera transazione e non vengono aggiunte righe alla tabella di destinazione.

> [!NOTE]  
> Questo esempio non funzionerà, a meno che non siano state create le tabelle di lavoro come descritto in [Impostazione delle tabelle](#table-setup). Questo codice viene fornito solo per illustrare la sintassi per l'utilizzo di SQLServerBulkCopy. Se le tabelle di origine e di destinazione si trovano nella stessa istanza di SQL Server, è più semplice e rapido usare un'istruzione Transact-SQL INSERT ... SELECT per copiare i dati.  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopyOptions;

public class BulkCopyExistingTransactions {
    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";
        String destinationTable = "dbo.BulkCopyDemoMatchingColumns";
        int countBefore, countAfter;
        ResultSet rsSourceData;
        SQLServerBulkCopyOptions copyOptions;

        try (Connection sourceConnection = DriverManager.getConnection(connectionUrl);
                Connection destinationConnection = DriverManager.getConnection(connectionUrl);
                Statement stmt = sourceConnection.createStatement();
                SQLServerBulkCopy bulkCopy = new SQLServerBulkCopy(destinationConnection);) {

            // Empty the destination table.
            stmt.executeUpdate("DELETE FROM " + destinationTable);

            // Add a single row that will result in duplicate key
            // when all rows from source are bulk copied.
            // Note that this technique will only be successful in
            // illustrating the point if a row with ProductID = 446
            // exists in the AdventureWorks Production.Products table.
            // If you have made changes to the data in this table, change
            // the SQL statement in the code to add a ProductID that
            // does exist in your version of the Production.Products
            // table. Choose any ProductID in the middle of the table
            // (not first or last row) to best illustrate the result.
            stmt.executeUpdate("SET IDENTITY_INSERT " + destinationTable + " ON;" + "INSERT INTO " + destinationTable
                    + "([ProductID], [Name] ,[ProductNumber]) VALUES(446, 'Lock Nut 23','LN-3416'); SET IDENTITY_INSERT " + destinationTable
                    + " OFF");

            // Perform an initial count on the destination table.
            countBefore = getRowCount(stmt, destinationTable);

            // Get data from the source table as a ResultSet.
            rsSourceData = stmt.executeQuery("SELECT ProductID, Name, ProductNumber FROM Production.Product");

            // Set up the bulk copy object inside the transaction.
            destinationConnection.setAutoCommit(false);

            copyOptions = new SQLServerBulkCopyOptions();
            copyOptions.setKeepIdentity(true);
            copyOptions.setBatchSize(10);

            bulkCopy.setBulkCopyOptions(copyOptions);
            bulkCopy.setDestinationTableName(destinationTable);

            // Write from the source to the destination.
            // This should fail with a duplicate key error.
            try {
                bulkCopy.writeToServer(rsSourceData);
                destinationConnection.commit();
            }
            catch (SQLException e) {
                e.printStackTrace();
            }

            // Perform a final count on the destination
            // table to see how many rows were added.
            countAfter = getRowCount(stmt, destinationTable);
            System.out.println((countAfter - countBefore) + " rows were added.");
        }
        catch (Exception e) {
            // Handle any errors that may have occurred.
            e.printStackTrace();
        }
    }

    private static int getRowCount(Statement stmt,
            String tableName) throws SQLException {
        ResultSet rs = stmt.executeQuery("SELECT COUNT(*) FROM " + tableName);
        rs.next();
        int count = rs.getInt(1);
        rs.close();
        return count;
    }
}
```

### <a name="bulk-copy-from-a-csv-file"></a>Copia bulk da un file CSV  

 L'applicazione riportata di seguito illustra come caricare i dati utilizzando la classe SQLServerBulkCopy. In questo esempio, viene utilizzato un file CSV per copiare i dati esportati dalla tabella Production.Product nel database AdventureWorks di SQL Server in una tabella simile del database.  
  
> [!IMPORTANT]  
> Questo esempio non funzionerà, a meno che non siano state create le tabelle di lavoro come descritto in [Impostazione delle tabelle](#table-setup).  
  
1. Aprire **SQL Server Management Studio** e connettersi a SQL Server con il database AdventureWorks.  
  
2. Espandere i database, fare clic con il pulsante destro del mouse sul database AdventureWorks e scegliere **Attività**, **Esporta dati**.  
  
3. Per l'origine dati, selezionare l'**origine dati** che consente di connettersi a SQL Server (ad esempio SQL Server Native Client 11.0), controllare la configurazione e quindi fare clic su **Avanti**  
  
4. Per la destinazione, selezionare **Destinazione file flat** e immettere un **nome file** con una destinazione, ad esempio C:\Test\TestBulkCSVExample.csv. Verificare che **Formato** sia impostato su Delimitato, che **Qualificatore di testo** sia impostato su Nessuno e abilitare **Nomi di colonne nella prima riga di dati**, quindi selezionare **Avanti**  
  
5. Selezionare **Scrivi una query per specificare i dati da trasferire** e fare clic su **Avanti**.  Immettere l'**istruzione SQL** SELECT ProductID, Name, ProductNumber FROM Production.Product e fare clic su **Avanti**  
  
6. Controllare la configurazione: È possibile lasciare {CR}{LF} come delimitatore di riga e la virgola {,} come delimitatore di colonna.  Selezionare **Modifica mapping** e verificare che il **tipo** di dati sia corretto per ogni colonna (ad esempio, integer per ProductID e stringa Unicode per le altre colonne).  
  
7. Proseguire fino alla **fine** ed eseguire l'esportazione.  

```java
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import com.microsoft.sqlserver.jdbc.SQLServerBulkCSVFileRecord;
import com.microsoft.sqlserver.jdbc.SQLServerBulkCopy;

public class BulkCopyCSV {
    public static void main(String[] args) {
        String connectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=AdventureWorks;user=<user>;password=<password>";
        String destinationTable = "dbo.BulkCopyDemoMatchingColumns";
        int countBefore, countAfter;

        // Get data from the source file by loading it into a class that implements ISQLServerBulkRecord.
        // Here we are using the SQLServerBulkCSVFileRecord implementation to import the example CSV file.
        try (Connection destinationConnection = DriverManager.getConnection(connectionUrl);
                Statement stmt = destinationConnection.createStatement();
                SQLServerBulkCopy bulkCopy = new SQLServerBulkCopy(destinationConnection);
                SQLServerBulkCSVFileRecord fileRecord = new SQLServerBulkCSVFileRecord("C:\\Test\\TestBulkCSVExample.csv", true);) {

            // Set the metadata for each column to be copied.
            fileRecord.addColumnMetadata(1, null, java.sql.Types.INTEGER, 0, 0);
            fileRecord.addColumnMetadata(2, null, java.sql.Types.NVARCHAR, 50, 0);
            fileRecord.addColumnMetadata(3, null, java.sql.Types.NVARCHAR, 25, 0);

            // Empty the destination table.
            stmt.executeUpdate("DELETE FROM " + destinationTable);

            // Perform an initial count on the destination table.
            countBefore = getRowCount(stmt, destinationTable);

            // Set up the bulk copy object.
            // Note that the column positions in the source
            // data reader match the column positions in
            // the destination table so there is no need to
            // map columns.
            bulkCopy.setDestinationTableName(destinationTable);

            // Write from the source to the destination.
            bulkCopy.writeToServer(fileRecord);

            // Perform a final count on the destination
            // table to see how many rows were added.
            countAfter = getRowCount(stmt, destinationTable);
            System.out.println((countAfter - countBefore) + " rows were added.");
        }
        // Handle any errors that may have occurred.
        catch (SQLException e) {
            e.printStackTrace();
        }
    }

    private static int getRowCount(Statement stmt,
            String tableName) throws SQLException {
        ResultSet rs = stmt.executeQuery("SELECT COUNT(*) FROM " + tableName);
        rs.next();
        int count = rs.getInt(1);
        rs.close();
        return count;
    }
}
```  

### <a name="bulk-copy-with-always-encrypted-columns"></a>Copia bulk con colonne Always Encrypted  

A partire da Microsoft JDBC Driver 6.0 per SQL Server è supportata la copia bulk con colonne Always Encrypted.  
  
A seconda delle opzioni di copia bulk e del tipo di crittografia delle tabelle di origine e di destinazione il driver JDBC può decrittografare in modo trasparente e quindi crittografare i dati oppure può inviare i dati crittografati senza alcuna modifica. Ad esempio, quando si esegue una copia bulk dei dati da una colonna crittografata a una colonna non crittografata, il driver decrittografa in modo trasparente i dati prima dell'invio a SQL Server. Ad esempio, quando si esegue una copia bulk dei dati da una colonna crittografata a una colonna non crittografata, il driver decrittografa in modo trasparente i dati prima dell'invio a SQL Server. Se entrambe le colonne di origine e di destinazione sono crittografate, a seconda dell'opzione di copia bulk **allowEncryptedValueModifications**, il driver invia i dati senza alcuna modifica oppure decrittografa i dati e li crittografa nuovamente prima di inviarli a SQL Server.  
  
Per altre informazioni, vedere l'opzione di copia bulk **allowEncryptedValueModifications** descritta di seguito e [Uso di Always Encrypted con il driver JDBC](using-always-encrypted-with-the-jdbc-driver.md).  
  
> [!IMPORTANT]  
> Limitazione di Microsoft JDBC Driver 6.0 per SQL Server durante la copia bulk di dati da un file CSV a colonne crittografate:  
>
> Per i tipi date e time è supportato solo il formato di valori letterali di stringa predefinito di Transact-SQL  
>
> I tipi di dati DATETIME e SMALLDATETIME non sono supportati  
  
## <a name="bulk-copy-api-for-jdbc-driver"></a>API della copia bulk per il driver JDBC  
  
### <a name="sqlserverbulkcopy"></a>SQLServerBulkCopy 

Consente di eseguire in modo efficiente il caricamento bulk di una tabella di SQL Server con i dati da un'altra origine.  
  
Microsoft SQL Server include una popolare utilità del prompt dei comandi denominata bcp per lo spostamento dei dati da una tabella all'altra, sia in un singolo server che tra diversi server. La classe SQLServerBulkCopy consente di scrivere soluzioni di codice in Java che offrono funzionalità simili. Esistono altri modi per caricare dati in una tabella di SQL Server (ad esempio, istruzioni INSERT), ma SQLServerBulkCopy offre un significativo vantaggio in termini di prestazioni.  
  
La classe SQLServerBulkCopy può essere utilizzata per scrivere dati solo in tabelle di SQL Server. Tuttavia l'origine dati non è limitata a SQL Server: può essere usata qualsiasi origine dati, purché i dati possano essere letti con un'istanza di ResultSet o un'implementazione di ISQLServerBulkRecord.  
  
| Costruttore                             | Descrizione                                                                                                                                                                                                                    |
| --------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| SQLServerBulkCopy(Connection)           | Inizializza una nuova istanza della classe SQLServerBulkCopy usando l'istanza aperta specificata di SQLServerConnection. Se la connessione ha transazioni abilitate, le operazioni di copia verranno eseguite all'interno della transazione. |
| SQLServerBulkCopy(String connectionURL) | Inizializza e apre una nuova istanza di SQLServerConnection in base al valore connectionURL specificato. Il costruttore usa SQLServerConnection per inizializzare una nuova istanza della classe SQLServerBulkCopy.                     |
  
| Proprietà                    | Descrizione                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| --------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| String DestinationTableName | Nome della tabella di destinazione nel server.<br /><br /> Se DestinationTableName non è stato impostato quando viene chiamato writeToServer, viene generata un'eccezione SQLServerException.<br /><br /> DestinationTableName è un nome composto da tre parti (\<database>.\<nomeschema>.\<nome>). Se si desidera, è possibile qualificare il nome della tabella con i relativi database e schema. Tuttavia, se il nome della tabella contiene un carattere di sottolineatura ("_") o altri caratteri speciali, è necessario racchiudere il nome tra parentesi quadre. Per ulteriori informazioni, vedere "Identificatori" nella documentazione online di SQL Server. |
| ColumnMappings              | I mapping delle colonne definiscono le relazioni tra le colonne nell'origine dati e le colonne nella destinazione.<br /><br /> Se i mapping non sono definiti, le colonne vengono mappate in modo implicito in base alla posizione ordinale. Per il corretto funzionamento, gli schemi di origine e di destinazione devono corrispondere. In caso contrario viene generata un'eccezione.<br /><br /> Se i mapping non sono vuoti, non tutte le colonne presenti nell'origine dati devono essere specificate. Le colonne di cui non viene eseguito il mapping sono ignorate.<br /><br /> È possibile fare riferimento alle colonne di origine e di destinazione in base al nome o alla posizione ordinale.               |
  
| Metodo                                                                | Descrizione                                                                                                                                                                |
| --------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Void addColumnMapping((int sourceColumn, int destinationColumn)       | Aggiunge un nuovo mapping di colonne, usando numeri ordinali per specificare le colonne di origine e di destinazione.                                                                                  |
| Void addColumnMapping ((int sourceColumn, String destinationColumn)   | Aggiunge un nuovo mapping di colonne, usando un numero ordinale per la colonna di origine e un nome di colonna per la colonna di destinazione.                                                            |
| Void addColumnMapping ((String sourceColumn, int destinationColumn)   | Aggiunge un nuovo mapping di colonne, usando un nome colonna per descrivere la colonna di origine e un numero ordinale per specificare la colonna di destinazione.                                             |
| Void addColumnMapping (String sourceColumn, String destinationColumn) | Aggiunge un nuovo mapping di colonne, usando nomi di colonna per specificare le colonne di origine e di destinazione.                                                                              |
| Void clearColumnMappings()                                            | Cancella il contenuto dei mapping di colonne.                                                                                                                                |
| Void close()                                                          | Chiude l'istanza di SQLServerBulkCopy.                                                                                                                                     |
| SQLServerBulkCopyOptions getBulkCopyOptions()                         | Recupera il set corrente di SQLServerBulkCopyOptions.                                                                                                                     |
| String getDestinationTableName()                                      | Recupera il nome della tabella di destinazione corrente.                                                                                                                               |
| Void setBulkCopyOptions(SQLServerBulkCopyOptions copyOptions)         | Aggiorna il comportamento dell'istanza di SQLServerBulkCopy in base alle opzioni fornite.                                                                                  |
| Void setDestinationTableName(String tableName)                        | Imposta il nome della tabella di destinazione.                                                                                                                                    |
| Void writeToServer(ResultSet sourceData)                              | Copia tutte le righe nel ResultSet specificato in una tabella di destinazione specificata dalla proprietà DestinationTableName dell'oggetto SQLServerBulkCopy.                           |
| Void writeToServer(RowSet sourceData)                                 | Copia tutte le righe nel RowSet specificato in una tabella di destinazione specificata dalla proprietà DestinationTableName dell'oggetto SQLServerBulkCopy.                              |
| Void writeToServer(ISQLServerBulkRecord sourceData)                   | Copia tutte le righe nell'implementazione ISQLServerBulkRecord specificata in una tabella di destinazione specificata dalla proprietà DestinationTableName dell'oggetto SQLServerBulkCopy. |
  
### <a name="sqlserverbulkcopyoptions"></a>SQLServerBulkCopyOptions  

 Raccolta di impostazioni che controllano il comportamento dei metodi writeToServer in un'istanza di SQLServerBulkCopy.  
  
| Costruttore                | Descrizione                                                                                              |
| -------------------------- | -------------------------------------------------------------------------------------------------------- |
| SQLServerBulkCopyOptions() | Inizializza una nuova istanza della classe SQLServerBulkCopyOptions utilizzando i valori predefiniti per tutte le impostazioni. |
  
 Sono disponibili metodi di richiamo e di impostazione per le opzioni seguenti:  
  
| Opzione                                   | Descrizione                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | Predefinito                                                              |
| ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------- |
| Boolean CheckConstraints                 | Controllare i vincoli durante l'inserimento dei dati.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         | False - i vincoli non vengono controllati                                   |
| Boolean FireTriggers                     | Se specificato, il server genera i trigger di inserimento per le righe da inserire nel database.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | False - non vengono generati trigger                                        |
| Boolean KeepIdentity                     | Mantenere i valori Identity di origine.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        | False - i valori Identity vengono assegnati dalla destinazione              |
| Boolean KeepNulls                        | Mantenere i valori null nella tabella di destinazione indipendentemente dalle impostazioni per i valori predefiniti.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | False - i valori null vengono sostituiti dai valori predefiniti, dove applicabile. |
| Boolean TableLock                        | Ottenere un blocco di aggiornamento bulk per la durata dell'operazione di copia bulk.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | False - vengono utilizzati i blocchi a livello di riga.                                          |
| Boolean UseInternalTransaction           | Se specificato, ogni batch dell'operazione di copia bulk viene eseguito all'interno di una transazione. Se SQLServerBulkCopy utilizza una connessione esistente (come specificato dal costruttore), si verificherà un'eccezione SQLServerException.  Se SQLServerBulkCopy ha creato una connessione dedicata, verrà abilitata una transazione.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    | False - nessuna transazione                                               |
| Int BatchSize                            | Numero di righe in ogni batch. Al termine di ogni batch, le righe nel batch vengono inviate al server.<br /><br /> Un batch è completato quando le righe BatchSize sono state elaborate o non sono più disponibili righe da inviare all'origine dati di destinazione.  Se l'istanza di SQLServerBulkCopy è stata dichiarata senza applicare l'opzione UseInternalTransaction, le righe vengono inviate al server in base al valore di BatchSize, ma non viene eseguita alcuna azione relativa alla transazione. Se viene applicata l'opzione UseInternalTransaction, ogni batch di righe viene inserito come una transazione distinta.                                                                                                                                                                                                                                                                                                                                                                                                                                           | 0 - indica che ogni operazione writeToServer è un singolo batch    |
| Int BulkCopyTimeout                      | Numero di secondi per il completamento dell'operazione prima del timeout. Il valore 0 indica nessun limite; la copia bulk attenderà per un tempo illimitato.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | 60 secondi.                                                          |
| Boolean allowEncryptedValueModifications | Questa opzione è disponibile con Microsoft JDBC Driver 6.0 (o versioni successive) per SQL Server.<br /><br /> Quando è specificata, **allowEncryptedValueModifications** abilita la copia bulk dei dati crittografati tra tabelle o database senza decrittografia dei dati. Solitamente un'applicazione seleziona i dati dalle colonne crittografate di un'unica tabella senza decrittografarli (l'app si connette al database con la parola chiave di impostazione della crittografia delle colonne impostata sullo stato disabilitato) e quindi usa questa opzione per eseguire l'inserimento bulk dei dati che sono ancora crittografati. Per altre informazioni, vedere [Utilizzo di Always Encrypted con il driver JDBC](using-always-encrypted-with-the-jdbc-driver.md).<br /><br /> Prestare attenzione quando si specifica **allowEncryptedValueModifications** in quanto questa operazione può causare il danneggiamento del database, perché il driver non verifica se i dati vengono effettivamente crittografati o se vengono crittografati correttamente usando lo stesso tipo di crittografia, l'algoritmo e la chiave come colonna di destinazione. |
  
 Getter e setter:  
  
| Metodi                                                                            | Descrizione                                                                                                                                                                               |
| ---------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Boolean isCheckConstraints()                                                       | Indica se i vincoli devono essere controllati durante l'inserimento dei dati.                                                                                                      |
| Void setCheckConstraints(Boolean checkConstraints)                                 | Specifica se i vincoli devono essere controllati durante l'inserimento dei dati.                                                                                                           |
| Boolean isFireTriggers()                                                           | Indica se il server deve generare i trigger di inserimento per le righe da inserire nel database.                                                                                    |
| Void setFireTriggers(Boolean fireTriggers)                                         | Specifica se il server deve essere impostato per la generazione dei trigger per le righe da inserire nel database.                                                                                     |
| Boolean isKeepIdentity()                                                           | Indica se mantenere i valori dell'identità di origine.                                                                                                                          |
| Void setKeepIdentity(Boolean keepIdentity)                                         | Specifica se mantenere i valori dell'identità.                                                                                                                                          |
| Boolean isKeepNulls()                                                              | Indica se mantenere i valori Null nella tabella di destinazione indipendentemente dalle impostazioni per i valori predefiniti o se sostituirli con i valori predefiniti (se applicabile). |
| Void setKeepNulls(Boolean keepNulls)                                               | Specifica se mantenere i valori Null nella tabella di destinazione indipendentemente dalle impostazioni per i valori predefiniti o se sostituirli con i valori predefiniti (se applicabile).      |
| Boolean isTableLock()                                                              | Indica se SQLServerBulkCopy deve ottenere un blocco di aggiornamento bulk per la durata dell'operazione di copia bulk.                                                                         |
| Void setTableLock(Boolean tableLock)                                               | Specifica se SQLServerBulkCopy deve ottenere un blocco di aggiornamento bulk per la durata dell'operazione di copia bulk.                                                                              |
| Boolean isUseInternalTransaction()                                                 | Indica se ogni batch dell'operazione di copia bulk viene eseguito all'interno di una transazione.                                                                                                  |
| Void setUseInternalTranscation(Boolean useInternalTransaction)                     | Determina se ogni batch delle operazioni di copia bulk viene eseguito all'interno di una transazione.                                                                                               |
| Int getBatchSize()                                                                 | Ottiene il numero di righe in ogni batch. Al termine di ogni batch, le righe nel batch vengono inviate al server.                                                                             |
| Void setBatchSize(int batchSize)                                                   | Imposta il numero di righe in ogni batch. Al termine di ogni batch, le righe nel batch vengono inviate al server.                                                                            |
| Int getBulkCopyTimeout()                                                           | Ottiene il numero di secondi per il completamento dell'operazione prima del timeout.                                                                                                             |
| Void  setBulkCopyTimeout(int timeout)                                              | Imposta il numero di secondi per il completamento dell'operazione prima del timeout.                                                                                                             |
| boolean isAllowEncryptedValueModifications()                                       | Indica se l'impostazione allowEncryptedValueModifications è abilitata o disabilitata.                                                                                                        |
| void setAllowEncryptedValueModifications(boolean allowEncryptedValueModifications) | Configura l'impostazione allowEncryptedValueModifications usata per la copia bulk con colonne Always Encrypted.                                                                         |
  
### <a name="isqlserverbulkrecord"></a>ISQLServerBulkRecord  

 L'interfaccia ISQLServerBulkRecord può essere utilizzata per creare classi che leggono i dati da qualsiasi origine (ad esempio un file) e consentono a un'istanza di SQLServerBulkCopy di eseguire il caricamento bulk di una tabella di SQL Server con tali dati.  
  
| Metodi di interfaccia                   | Descrizione                                                                                                                                                                                                                                                                                            |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Set\<Integer> getColumnOrdinals()   | Ottenere gli ordinali per ognuna delle colonne rappresentate nel record di dati.                                                                                                                                                                                                                              |
| String getColumnName(int column)    | Ottenere il nome della colonna specificata.                                                                                                                                                                                                                                                                      |
| Int getColumnType(int column)       | Ottenere il tipo di dati JDBC della colonna specificata.                                                                                                                                                                                                                                                            |
| Int getPrecision(int column)        | Ottenere la precisione per la colonna specificata.                                                                                                                                                                                                                                                                |
| Object[] getRowData()               | Ottenere i dati per la riga corrente come una matrice di oggetti.<br /><br /> Ogni oggetto deve corrispondere al tipo di linguaggio Java utilizzato per rappresentare il tipo di dati JDBC indicato per la colonna specificata.  Per altre informazioni sui mapping appropriati, vedere 'Informazioni sui tipi di dati del driver JDBC'. |
| Int getScale(int column)            | Ottenere la scala per la colonna specificata.                                                                                                                                                                                                                                                                    |
| Boolean isAutoIncrement(int column) | Indica se la colonna rappresenta una colonna Identity.                                                                                                                                                                                                                                            |
| Boolean next()                      | Passa alla riga di dati successiva.                                                                                                                                                                                                                                                                         |
  
### <a name="sqlserverbulkcsvfilerecord"></a>SQLServerBulkCSVFileRecord  

Una semplice implementazione dell'interfaccia ISQLServerBulkRecord che può essere utilizzata per leggere i tipi di dati Java di base da un file delimitato in cui ogni riga rappresenta una riga di dati.  
  
Note sull'implementazione e limitazioni:  
  
1. La quantità massima di dati consentiti in una determinata riga è limitata dalla memoria disponibile, poiché i dati vengono letti una riga alla volta.  
  
2. Il flusso di tipi di dati di grandi dimensioni come varchar(max), varbinary(max), nvarchar(max), sqlxml e ntext non è supportato.  
  
3. Il delimitatore specificato per il file CSV non deve essere contenuto nei dati e deve essere sottoposto a escape in modo appropriato se è un carattere con limitazioni nelle espressioni regolari di Java.  
  
4. Nell'implementazione del file CSV le virgolette doppie vengono considerate parte dei dati. Ad esempio, la riga hello,"world","hello,world" verrebbe considerata come contenente quattro colonne con i valori hello, "world", "hello e world" se il delimitatore è una virgola.  
  
5. I caratteri a capo vengono usati come caratteri di terminazione della riga e non sono consentiti nei dati.  
  
| Costruttore                                                                                                                                                                 | Descrizione                                                                                                                                                                                                                                                                                                                        |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| SQLServerBulkCSVFileRecord(String fileToParse, String encoding, String delimiter, Boolean firstLineIsColumnNamesSQLServerBulkCSVFileRecord(String, String, String, boolean) | Inizializza una nuova istanza della classe SQLServerBulkCSVFileRecord che analizza ogni riga in fileToParse con il delimitatore e la codifica specificati. Se firstLineIsColumnNames è impostato su True, la prima riga nel file sarà analizzata come nomi di colonna.  Se la codifica è NULL, verrà utilizzata la codifica predefinita.            |
| SQLServerBulkCSVFileRecord(String fileToParse, String encoding, Boolean firstLineIsColumnNamesSQLServerBulkCSVFileRecord(String, String, boolean)                           | Inizializza una nuova istanza della classe SQLServerBulkCSVFileRecord che analizza ogni riga in fileToParse con una virgola come delimitatore e la codifica specificata. Se firstLineIsColumnNames è impostato su True, la prima riga nel file sarà analizzata come nomi di colonna.  Se la codifica è NULL, verrà utilizzata la codifica predefinita. |
| SQLServerBulkCSVFileRecord(String fileToParse, Boolean firstLineIsColumnNamesSQLServerBulkCSVFileRecord(String, boolean)                                                    | Inizializza una nuova istanza della classe SQLServerBulkCSVFileRecord che analizza ogni riga in fileToParse con una virgola come delimitatore e la codifica predefinita. Se firstLineIsColumnNames è impostato su True, la prima riga nel file sarà analizzata come nomi di colonna.                                                           |
  
| Metodo                                                                                                 | Descrizione                                                                                         |
| ------------------------------------------------------------------------------------------------------ | --------------------------------------------------------------------------------------------------- |
| Void addColumnMetadata(int positionInFile, String columnName, int jdbcType, int precision, int scale)  | Aggiunge i metadati per la colonna specificata nel file.                                                     |
| Void close()                                                                                           | Rilascia le risorse associate al lettore di file.                                             |
| Void setTimestampWithTimezoneFormat(DateTim eFormatter dateTimeFormatter                               | Imposta il formato per l'analisi dei dati Timestamp del file come java.sql.Types.TIMESTAMP_WITH_TIMEZONE. |
| Void setTimestampWithTimezoneFormat(String dateTimeFormat)setTimeWithTimezoneFormat(DateTimeFormatter) | Imposta il formato per l'analisi dei dati Time del file come java.sql.Types.TIME_WITH_TIMEZONE.           |
| Void setTimeWithTimezoneFormat(DateTimeForm atter dateTimeFormatter)                                   | Imposta il formato per l'analisi dei dati Time del file come java.sql.Types.TIME_WITH_TIMEZONE.           |
| Void setTimeWithTimezoneFormat(String timeFormat)                                                      | Imposta il formato per l'analisi dei dati Time del file come java.sql.Types.TIME_WITH_TIMEZONE.           |
  
## <a name="see-also"></a>Vedere anche  

[Panoramica del driver JDBC](overview-of-the-jdbc-driver.md)  
