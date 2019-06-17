---
title: Usando l'API della copia Bulk per l'operazione di inserimento Batch per il Driver JDBC MSSQL | Microsoft Docs
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 347ce28dc28016f95de2795bd2f5e491dd29e2d8
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66802635"
---
# <a name="using-bulk-copy-api-for-batch-insert-operation"></a>Uso dell'API di copia bulk per un'operazione di inserimento batch

[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

Microsoft JDBC Driver 7.0 per SQL Server supporta l'utilizzo delle API della copia Bulk per le operazioni di inserimento batch per Azure Data Warehouse. Questa funzionalità consente agli utenti di abilitare driver a un'operazione di copia Bulk sottostante quando l'esecuzione batch le operazioni di inserimento. Gli obiettivi di driver per ottenere il miglioramento delle prestazioni durante l'inserimento degli stessi dati come il driver avrebbe con batch normale operazione di inserimento. Il driver analizza Query SQL dell'utente, sfruttando le API della copia Bulk anziché l'operazione di inserimento batch normale. Di seguito sono vari modi per abilitare l'API della copia Bulk per batch inserire funzionalità, nonché l'elenco delle relative limitazioni. Questa pagina contiene anche un codice di esempio di piccole dimensioni che illustra un uso e anche l'aumento delle prestazioni.

Questa funzionalità è applicabile solo ai PreparedStatement e del CallableStatement `executeBatch()`  &  `executeLargeBatch()` API.

## <a name="pre-requisites"></a>Prerequisiti

Esistono due prerequisiti per abilitare l'API della copia Bulk per inserimenti batch.

* Il server deve essere Data Warehouse di Azure.
* La query deve essere una query insert (la query può contenere commenti, ma la query deve iniziare con la parola chiave di inserimento per questa funzionalità diventi effettiva).

## <a name="enabling-bulk-copy-api-for-batch-insert"></a>Abilitazione API della copia Bulk per l'inserimento di batch

Esistono tre modi per abilitare l'API della copia Bulk per inserimenti batch.

### <a name="1-enabling-with-connection-property"></a>1. Abilitazione con proprietà di connessione

Aggiunta **useBulkCopyForBatchInsert = true;** alla connessione stringa rende disponibile questa funzionalità.

```java
Connection connection = DriverManager.getConnection("jdbc:sqlserver://<server>:<port>;userName=<user>;password=<password>;database=<database>;useBulkCopyForBatchInsert=true;");
```

### <a name="2-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverconnection-object"></a>2. Abilitazione con metodo setUseBulkCopyForBatchInsert() dall'oggetto SQLServerConnection

La chiamata **SQLServerConnection.setUseBulkCopyForBatchInsert(true)** rende disponibile questa funzionalità.

**SQLServerConnection.getUseBulkCopyForBatchInsert()** recupera il valore corrente per **useBulkCopyForBatchInsert** proprietà di connessione.

Il valore per **useBulkCopyForBatchInsert** rimane costante per ogni impostazione PreparedStatement al momento dell'inizializzazione. Tutte le chiamate successive a **SQLServerConnection.setUseBulkCopyForBatchInsert()** non avrà effetto sulle impostazione PreparedStatement già creata per quanto riguarda il relativo valore.

### <a name="3-enabling-with-setusebulkcopyforbatchinsert-method-from-sqlserverdatasource-object"></a>3. Abilitazione con metodo setUseBulkCopyForBatchInsert() dall'oggetto SQLServerDataSource

Analogamente al precedente, ma usando SQLServerDataSource per creare un oggetto SQLServerConnection. Entrambi i metodi ottengono lo stesso risultato.

## <a name="known-limitations"></a>Limitazioni note

Sono attualmente presenti queste limitazioni che si applicano a questa funzionalità.

* Inserire le query che contengono valori senza parametri (ad esempio, `INSERT INTO TABLE VALUES (?, 2`)), non sono supportati. I caratteri jolly (?) sono gli unici parametri supportati per questa funzione.
* Le query che contengono espressioni INSERT-SELECT di inserimento (ad esempio, `INSERT INTO TABLE SELECT * FROM TABLE2`), non sono supportati.
* Inserire le query che contengono più espressioni valore (ad esempio, `INSERT INTO TABLE VALUES (1, 2) (3, 4)`), non sono supportati.
* Query di accodamento sono aggiungendo la clausola OPTION, unito in join con più tabelle o seguita da un'altra query, non sono supportate.
* A causa di limitazioni dell'API della copia Bulk, `MONEY`, `SMALLMONEY`, `DATE`, `DATETIME`, `DATETIMEOFFSET`, `SMALLDATETIME`, `TIME`, `GEOMETRY`, e `GEOGRAPHY` tipi di dati, non sono attualmente supportate per questo oggetto funzionalità.

Se la query ha esito negativo a causa non correlati a errori di "SQL server", il driver registreranno il messaggio di errore e del fallback per la logica per l'inserimento batch originale.

## <a name="example"></a>Esempio

Di seguito è riportato un esempio di codice che dimostra il caso d'uso per un'operazione di inserimento batch con Azure Data Warehouse di un migliaio di righe, per entrambi gli scenari (vs normali API della copia Bulk).

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
