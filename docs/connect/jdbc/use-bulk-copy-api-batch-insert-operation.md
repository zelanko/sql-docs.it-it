---
title: Uso dell'API per la copia bulk per l'operazione di inserimento batch per il driver JDBC per MSSQL | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3050cdf87775a67618902dfbb88b656003020769
ms.sourcegitcommit: 9348f79efbff8a6e88209bb5720bd016b2806346
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 08/14/2019
ms.locfileid: "69027100"
---
# <a name="using-bulk-copy-api-for-batch-insert-operation"></a>Uso dell'API di copia bulk per un'operazione di inserimento batch

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Microsoft JDBC driver 7,0 per SQL Server supporta l'utilizzo dell'API per la copia bulk per le operazioni di inserimento batch per data warehouse di Azure. Questa funzionalità consente agli utenti di consentire al driver di eseguire l'operazione di copia bulk sottostanti durante l'esecuzione di operazioni di inserimento in batch. Il driver mira a migliorare le prestazioni e a inserire gli stessi dati del driver con operazioni di inserimento batch regolari. Il driver analizza la query SQL dell'utente, sfruttando l'API per la copia bulk invece della consueta operazione di inserimento batch. Di seguito sono riportati diversi modi per abilitare l'API per la copia bulk per la funzionalità di inserimento batch, nonché l'elenco delle relative limitazioni. Questa pagina contiene anche un piccolo codice di esempio che illustra un utilizzo e l'aumento delle prestazioni.

Questa funzionalità è applicabile solo alle `executeBatch()` `executeLargeBatch()` API PreparedStatement e CallableStatement  &  .

## <a name="prerequisites"></a>Prerequisites

Sono necessari due prerequisiti per abilitare l'API per la copia bulk per l'inserimento batch.

* Il server deve essere data warehouse di Azure.
* La query deve essere una query Insert (la query può contenere commenti, ma la query deve iniziare con la parola chiave INSERT per applicare questa funzionalità).

## <a name="enabling-bulk-copy-api-for-batch-insert"></a>Abilitazione dell'API per la copia bulk per l'inserimento batch

Sono disponibili tre modi per abilitare l'API per la copia bulk per l'inserimento batch.

### <a name="1-enabling-with-connection-property"></a>1. Abilitazione con proprietà di connessione

L'aggiunta di **useBulkCopyForBatchInsert = true;** alla stringa di connessione Abilita questa funzionalità.

```java
Connection connection = DriverManager.getConnection("jdbc:sqlserver://<server>:<port>;userName=<user>;password=<password>;database=<database>;useBulkCopyForBatchInsert=true;");
```

### <a name="2-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverconnection-object"></a>2. Abilitazione con il metodo setUseBulkCopyForBatchInsert () dall'oggetto SQLServerConnection

La chiamata a **SQLServerConnection. setUseBulkCopyForBatchInsert (true)** Abilita questa funzionalità.

**SQLServerConnection. getUseBulkCopyForBatchInsert ()** Recupera il valore corrente per la proprietà di connessione **useBulkCopyForBatchInsert** .

Il valore di **useBulkCopyForBatchInsert** rimane costante per ogni PreparedStatement al momento dell'inizializzazione. Tutte le chiamate successive a **SQLServerConnection. setUseBulkCopyForBatchInsert ()** non influiscono sui PreparedStatement già creati per quanto riguarda il relativo valore.

### <a name="3-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverdatasource-object"></a>3. Abilitazione con il metodo setUseBulkCopyForBatchInsert () da un oggetto SQLServerDataSource

Simile a quanto sopra, ma usando SQLServerDataSource per creare un oggetto SQLServerConnection. Entrambi i metodi ottengono lo stesso risultato.

## <a name="known-limitations"></a>Limitazioni note

Attualmente sono presenti limitazioni che si applicano a questa funzionalità.

* Le query INSERT che contengono valori senza parametri (ad esempio, `INSERT INTO TABLE VALUES (?, 2`)) non sono supportate. I caratteri jolly (?) sono gli unici parametri supportati per questa funzione.
* Le query INSERT che contengono espressioni INSERT-SELECT (ad esempio `INSERT INTO TABLE SELECT * FROM TABLE2`,) non sono supportate.
* Le query INSERT che contengono più espressioni di valore (ad `INSERT INTO TABLE VALUES (1, 2) (3, 4)`esempio,) non sono supportate.
* Le query di inserimento seguite dalla clausola OPTION, unite a più tabelle o seguite da un'altra query, non sono supportate.
* A causa delle limitazioni dell'API per la copia `MONEY`bulk `SMALLMONEY`, `DATE` `GEOMETRY` `DATETIMEOFFSET` `SMALLDATETIME` `DATETIME`i tipi di dati `TIME`,,, `GEOGRAPHY` ,,,, e non sono attualmente supportati per questa funzionalità.

Se la query ha esito negativo a causa di errori non correlati a "SQL Server", il driver registrerà il messaggio di errore e il fallback alla logica originale per l'inserimento batch.

## <a name="example"></a>Esempio

Di seguito è riportato un esempio di codice che illustra il caso d'uso per un'operazione di inserimento in batch in Azure DW di un migliaio di righe, per entrambi gli scenari (normali API per la copia bulk).

```java
    public static void main(String[] args) throws Exception
    {
        String tableName = "batchTest";
        String tableNameBulkCopyAPI = "batchTestBulk";

        String azureDWconnectionUrl = "jdbc:sqlserver://<server>:<port>;databaseName=<database>;user=<user>;password=<password>";

        try (Connection con = DriverManager.getConnection(azureDWconnectionUrl); // connects to an Azure Data Warehouse.
                Statement stmt = con.createStatement();
                PreparedStatement pstmt = con.prepareStatement("insert into " + tableName + " values (?, ?)");) {

            String dropSql = "if exists (select * from dbo.sysobjects where id = object_id(N'[dbo].[" + tableName + "]') and OBJECTPROPERTY(id, N'IsUserTable') = 1) DROP TABLE [" + tableName + "]";
            stmt.execute(dropSql);

            String createSql = "create table " + tableName + " (c1 int, c2 varchar(20))";
            stmt.execute(createSql);

            System.out.println("Starting batch operation using regular batch insert operation.");
            long start = System.currentTimeMillis();
            for (int i = 0; i < 1000; i++) {
                pstmt.setInt(1, i);
                pstmt.setString(2, "test" + i);
                pstmt.addBatch();
            }
            pstmt.executeBatch();

            long end = System.currentTimeMillis();

            System.out.println("Finished. Time taken : " + (end - start) + " milliseconds.");
        }

        try (Connection con = DriverManager.getConnection(azureDWconnectionUrl + ";useBulkCopyForBatchInsert=true"); // connects to an Azure Data Warehouse, with useBulkCopyForBatchInsert connection property set to true.
                Statement stmt = con.createStatement();
                PreparedStatement pstmt = con.prepareStatement("insert into " + tableNameBulkCopyAPI + " values (?, ?)");) {

            String dropSql = "if exists (select * from dbo.sysobjects where id = object_id(N'[dbo].[" + tableNameBulkCopyAPI + "]') and OBJECTPROPERTY(id, N'IsUserTable') = 1) DROP TABLE [" + tableNameBulkCopyAPI + "]";
            stmt.execute(dropSql);

            String createSql = "create table " + tableNameBulkCopyAPI + " (c1 int, c2 varchar(20))";
            stmt.execute(createSql);

            System.out.println("Starting batch operation using Bulk Copy API.");
            long start = System.currentTimeMillis();
            for (int i = 0; i < 1000; i++) {
                pstmt.setInt(1, i);
                pstmt.setString(2, "test" + i);
                pstmt.addBatch();
            }
            pstmt.executeBatch();

            long end = System.currentTimeMillis();

            System.out.println("Finished. Time taken : " + (end - start) + " milliseconds.");
        }
    }
```

Risultato:

```bash
Starting batch operation using regular batch insert operation.
Finished. Time taken : 104132 milliseconds.
Starting batch operation using Bulk Copy API.
Finished. Time taken : 1058 milliseconds.
```

## <a name="see-also"></a>Vedere anche

[Uso del driver JDBC per il miglioramento di prestazioni e affidabilità](../../connect/jdbc/improving-performance-and-reliability-with-the-jdbc-driver.md)
