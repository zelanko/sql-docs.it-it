---
title: Esecuzione di un'istruzione . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], executing
ms.assetid: e5f0d2ee-0453-4faf-b007-12978dd300a1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c3ce09809c896a4d1d9333da00367f972655f96b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305742"
---
# <a name="executing-a-statement"></a>Esecuzione di un'istruzione
Esistono quattro modi per eseguire un'istruzione, a seconda di quando vengono compilati (preparati) dal motore di database e che li definisce:There are four ways to execute a statement, depending on when they are compiled (prepared) by the database engine and who defines them:  
  
-   **Esecuzione diretta** L'applicazione definisce l'istruzione SQL. Viene preparato ed eseguito in fase di esecuzione in un unico passaggio.  
  
-   **Esecuzione preparata** L'applicazione definisce l'istruzione SQL. Viene preparato ed eseguito in fase di esecuzione in passaggi separati. L'istruzione può essere preparata una sola volta ed eseguita più volte.  
  
-   **Procedure** L'applicazione può definire e compilare una o più istruzioni SQL in fase di sviluppo e archiviare queste istruzioni nell'origine dati come routine. La procedura viene eseguita una o più volte in fase di esecuzione. L'applicazione può enumerare le stored procedure disponibili utilizzando le funzioni di catalogo.  
  
-   **Funzioni di catalogo** Il writer del driver crea una funzione che restituisce un set di risultati predefinito. In genere, questa funzione invia un'istruzione SQL predefinita o chiama una procedura creata per questo scopo. La funzione viene eseguita una o più volte in fase di esecuzione.  
  
 Una particolare istruzione (identificata dal relativo handle di istruzione) può essere eseguita un numero qualsiasi di volte. L'istruzione può essere eseguita con una varietà di istruzioni SQL diverse oppure può essere eseguita ripetutamente con la stessa istruzione SQL. Ad esempio, il codice seguente utilizza lo stesso handle di istruzione (*hstmt1*) per recuperare e visualizzare le tabelle nel database Sales. Viene quindi riutilizzato questo handle per recuperare le colonne in una tabella selezionata dall'utente.  
  
```  
SQLHSTMT    hstmt1;  
SQLCHAR *   Table;  
  
// Create a result set of all tables in the Sales database.  
SQLTables(hstmt1, "Sales", SQL_NTS, "sysadmin", SQL_NTS, NULL, 0, NULL, 0);  
  
// Fetch and display the table names; then close the cursor.  
// Code not shown.  
  
// Have the user select a particular table.  
SelectTable(Table);  
  
// Reuse hstmt1 to create a result set of all columns in Table.  
SQLColumns(hstmt1, "Sales", SQL_NTS, "sysadmin", SQL_NTS, Table, SQL_NTS, NULL, 0);  
  
// Fetch and display the column names in Table; then close the cursor.  
// Code not shown.  
```  
  
 Il codice seguente mostra come viene utilizzato un singolo handle per eseguire ripetutamente la stessa istruzione per eliminare righe da una tabella.  
  
```  
SQLHSTMT      hstmt1;  
SQLUINTEGER   OrderID;  
SQLINTEGER    OrderIDInd = 0;  
  
// Prepare a statement to delete orders from the Orders table.  
SQLPrepare(hstmt1, "DELETE FROM Orders WHERE OrderID = ?", SQL_NTS);  
  
// Bind OrderID to the parameter for the OrderID column.  
SQLBindParameter(hstmt1, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
                  &OrderID, 0, &OrderIDInd);  
  
// Repeatedly execute hstmt1 with different values of OrderID.  
while ((OrderID = GetOrderID()) != 0) {  
   SQLExecute(hstmt1);  
}  
```  
  
 Per molti driver, l'allocazione di istruzioni è un'attività costosa, pertanto riutilizzare la stessa istruzione in questo modo è in genere più efficiente rispetto alla liberazione di istruzioni esistenti e all'allocazione di nuove. Le applicazioni che creano set di risultati in un'istruzione devono prestare attenzione a chiudere il cursore sul set di risultati prima di rieseguire l'istruzione. Per ulteriori informazioni, consultate [Chiusura del cursore.](../../../odbc/reference/develop-app/closing-the-cursor.md)  
  
 Il riutilizzo delle istruzioni impone inoltre all'applicazione di evitare una limitazione in alcuni driver del numero di istruzioni che possono essere attive contemporaneamente. La definizione esatta di "attivo" è specifica del driver, ma spesso si riferisce a qualsiasi istruzione che è stata preparata o eseguita e ha ancora risultati disponibili. Ad esempio, dopo la preparazione di un'istruzione **INSERT,** viene in genere considerata attiva; dopo l'esecuzione di un'istruzione **SELECT** e l'apertura del cursore, in genere viene considerata attiva; dopo l'esecuzione di un'istruzione **CREATE TABLE,** in genere non viene considerata attiva.  
  
 Un'applicazione determina quante istruzioni possono essere attive su una singola connessione contemporaneamente chiamando **SQLGetInfo** con l'opzione SQL_MAX_CONCURRENT_ACTIVITIES. Un'applicazione può utilizzare più istruzioni attive di questo limite aprendo più connessioni all'origine dati. perché le connessioni possono essere costose, tuttavia, l'effetto sulle prestazioni deve essere considerato.  
  
 Le applicazioni possono limitare il periodo di tempo assegnato per l'esecuzione di un'istruzione con l'attributo di istruzione SQL_ATTR_QUERY_TIMEOUT. Se il periodo di timeout scade prima che l'origine dati restituisca il set di risultati, la funzione che esegue l'istruzione SQL restituisce SQLSTATE HYT00 (Timeout scaduto). Per impostazione predefinita, non è previsto alcun timeout.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Esecuzione diretta](../../../odbc/reference/develop-app/direct-execution-odbc.md)  
  
-   [Esecuzione preparata](../../../odbc/reference/develop-app/prepared-execution-odbc.md)  
  
-   [Procedure](../../../odbc/reference/develop-app/procedures-odbc.md)  
  
-   [Batch di istruzioni SQL](../../../odbc/reference/develop-app/batches-of-sql-statements.md)  
  
-   [Esecuzione delle funzioni di catalogo](../../../odbc/reference/develop-app/executing-catalog-functions.md)
