---
title: Uso dell'API di copia bulk per un'operazione di inserimento batch per JDBC Driver per MSSQL | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 62843af006d730c3994519fe4c31182805923478
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 04/08/2020
ms.locfileid: "80916887"
---
# <a name="using-bulk-copy-api-for-batch-insert-operation"></a>Uso dell'API di copia bulk per un'operazione di inserimento batch

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Microsoft JDBC Driver 7.0 per SQL Server supporta l'uso dell'API di copia bulk per le operazioni di inserimento batch per Azure Data Warehouse. Con questa funzionalità gli utenti possono consentire al driver di eseguire l'operazione di copia bulk sottostante durante l'esecuzione di operazioni di inserimento batch. Il driver cerca di migliorare le prestazioni inserendo gli stessi dati che si avrebbero con una normale operazione di inserimento batch. Il driver analizza la query SQL dell'utente, sfruttando l'API di copia bulk invece della consueta operazione di inserimento batch. Di seguito sono illustrati diversi modi per abilitare l'API di copia bulk per la funzionalità di inserimento batch, nonché l'elenco delle relative limitazioni. Questa pagina contiene un piccolo codice di esempio che illustra un utilizzo e anche l'aumento delle prestazioni.

Questa funzionalità è applicabile solo alle API `executeBatch()` & `executeLargeBatch()` di PreparedStatement e CallableStatement.

## <a name="prerequisites"></a>Prerequisiti

L'abilitazione dell'API di copia bulk per l'inserimento batch presenta due prerequisiti.

* Il server deve essere Azure Data Warehouse.
* La query deve essere una query di inserimento (la query può contenere commenti, ma deve iniziare con la parola chiave INSERT perché questa funzionalità venga applicata).

## <a name="enabling-bulk-copy-api-for-batch-insert"></a>Abilitazione dell'API di copia bulk per l'inserimento batch

Sono disponibili tre modi per abilitare l'API di copia bulk per l'inserimento batch.

### <a name="1-enabling-with-connection-property"></a>1. Abilitazione con proprietà di connessione

L'aggiunta di **useBulkCopyForBatchInsert=true;** alla stringa di connessione consente di abilitare questa funzionalità.

```java
Connection connection = DriverManager.getConnection("jdbc:sqlserver://<server>:<port>;userName=<user>;password=<password>;database=<database>;useBulkCopyForBatchInsert=true;");
```

### <a name="2-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverconnection-object"></a>2. Abilitazione con il metodo setUseBulkCopyForBatchInsert() dall'oggetto SQLServerConnection

La chiamata di **SQLServerConnection. setUseBulkCopyForBatchInsert (true)** consente di abilitare questa funzionalità.

**SQLServerConnection.getUseBulkCopyForBatchInsert()** consente di recuperare il valore corrente per la proprietà di connessione **useBulkCopyForBatchInsert**.

Il valore per **useBulkCopyForBatchInsert** rimane costante per ogni PreparedStatement al momento della sua inizializzazione. Qualsiasi chiamata successiva a **SQLServerConnection.setUseBulkCopyForBatchInsert()** non influirà sulla PreparedStatement già creata per quanto riguarda il relativo valore.

### <a name="3-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverdatasource-object"></a>3. Abilitazione con il metodo setUseBulkCopyForBatchInsert() dall'oggetto SQLServerDataSource

Simile a quanto descritto sopra, ma con l'uso di SQLServerDataSource per creare un oggetto SQLServerConnection. Entrambi i metodi ottengono lo stesso risultato.

## <a name="known-limitations"></a>Limitazioni note

Al momento, questa funzionalità è soggetta alle limitazioni seguenti.

* Le query di inserimento contenenti valori senza parametri (ad esempio `INSERT INTO TABLE VALUES (?, 2`)) non sono supportate. I caratteri jolly (?) sono gli unici parametri supportati per questa funzione.
* Le query di inserimento contenenti espressioni INSERT-SELECT (ad esempio `INSERT INTO TABLE SELECT * FROM TABLE2`) non sono supportate.
* Le query di inserimento contenenti più espressioni VALUE (ad esempio `INSERT INTO TABLE VALUES (1, 2) (3, 4)`) non sono supportate.
* Le query di inserimento seguite dalla clausola OPTION, unite a più tabelle o seguite da un'altra query, non sono supportate.
* A causa delle limitazioni dell'API di copia bulk, i tipi di dati `MONEY`, `SMALLMONEY`, `DATE`, `DATETIME`, `DATETIMEOFFSET`, `SMALLDATETIME`, `TIME`, `GEOMETRY` e `GEOGRAPHY` non sono al momento supportati per questa funzionalità.

Se la query ha esito negativo a causa di errori non correlati a "SQL Server", il driver registrerà il messaggio di errore e il fallback alla logica originale per l'inserimento batch.

## <a name="example"></a>Esempio

Di seguito è riportato un esempio di codice che illustra il caso d'uso per un'operazione di inserimento in batch in Azure DW di un migliaio di righe, per entrambi gli scenari (normale e API di copia bulk).

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
