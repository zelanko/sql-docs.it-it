---
description: Esecuzione di un'istruzione
title: Esecuzione di un'istruzione | Microsoft Docs
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
ms.openlocfilehash: 4ce060c91e2500b016e824e733d8189c99334e1b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461473"
---
# <a name="executing-a-statement"></a>Esecuzione di un'istruzione
Esistono quattro modi per eseguire un'istruzione, a seconda del momento in cui vengono compilati (preparati) dal motore di database e che li definiscono:  
  
-   **Esecuzione diretta** L'applicazione definisce l'istruzione SQL. Viene preparata ed eseguita in fase di esecuzione in un singolo passaggio.  
  
-   **Esecuzione preparata** L'applicazione definisce l'istruzione SQL. Viene preparata ed eseguita in fase di esecuzione in passaggi distinti. L'istruzione può essere preparata una volta ed eseguita più volte.  
  
-   **Procedure** L'applicazione può definire e compilare una o più istruzioni SQL in fase di sviluppo e archiviare queste istruzioni nell'origine dati come procedura. La procedura viene eseguita una o più volte in fase di esecuzione. L'applicazione può enumerare le stored procedure disponibili utilizzando le funzioni di catalogo.  
  
-   **Funzioni di catalogo** Il writer del driver crea una funzione che restituisce un set di risultati predefinito. In genere, questa funzione Invia un'istruzione SQL predefinita o chiama una procedura creata a questo scopo. La funzione viene eseguita una o più volte in fase di esecuzione.  
  
 Un'istruzione specifica (identificata dal relativo handle di istruzione) può essere eseguita un numero qualsiasi di volte. L'istruzione può essere eseguita con un'ampia gamma di istruzioni SQL diverse oppure può essere eseguita ripetutamente con la stessa istruzione SQL. Nel codice seguente, ad esempio, viene utilizzato lo stesso handle di istruzione (*hstmt1*) per recuperare e visualizzare le tabelle nel database Sales. Riutilizza quindi questo handle per recuperare le colonne in una tabella selezionata dall'utente.  
  
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
  
 Nel codice seguente viene illustrato come utilizzare un singolo handle per eseguire ripetutamente la stessa istruzione per eliminare le righe da una tabella.  
  
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
  
 Per molti driver, l'allocazione di istruzioni è un'attività costosa, quindi il riutilizzo della stessa istruzione in questo modo è in genere più efficiente rispetto alla liberazione di istruzioni esistenti e all'allocazione di nuove. Per le applicazioni che creano set di risultati in un'istruzione è necessario prestare attenzione a chiudere il cursore sul set di risultati prima di rieseguire l'istruzione. Per ulteriori informazioni, vedere [chiusura del cursore](../../../odbc/reference/develop-app/closing-the-cursor.md).  
  
 Il riutilizzo di istruzioni impone inoltre all'applicazione di evitare una limitazione in alcuni driver del numero di istruzioni che possono essere attive alla volta. La definizione esatta di "Active" è specifica del driver, ma si riferisce spesso a qualsiasi istruzione preparata o eseguita e con risultati ancora disponibili. Ad esempio, dopo che un'istruzione **Insert** è stata preparata, viene in genere considerata attiva. dopo l'esecuzione di un'istruzione **Select** e il cursore è ancora aperto, in genere viene considerato attivo; dopo l'esecuzione di un'istruzione **Create Table** , non viene in genere considerata attiva.  
  
 Un'applicazione determina il numero di istruzioni che possono essere attive in una singola connessione alla volta chiamando **SQLGetInfo** con l'opzione SQL_MAX_CONCURRENT_ACTIVITIES. Un'applicazione può utilizzare più istruzioni attive rispetto a questo limite aprendo più connessioni all'origine dati. Poiché le connessioni possono essere costose, tuttavia, è necessario considerare l'effetto sulle prestazioni.  
  
 Le applicazioni possono limitare la quantità di tempo assegnata per l'esecuzione di un'istruzione con l'attributo dell'istruzione SQL_ATTR_QUERY_TIMEOUT. Se il periodo di timeout scade prima che l'origine dati restituisca il set di risultati, la funzione che esegue l'istruzione SQL restituisce SQLSTATE HYT00 (timeout scaduto). Per impostazione predefinita, non è previsto alcun timeout.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Esecuzione diretta](../../../odbc/reference/develop-app/direct-execution-odbc.md)  
  
-   [Esecuzione preparata](../../../odbc/reference/develop-app/prepared-execution-odbc.md)  
  
-   [Procedure](../../../odbc/reference/develop-app/procedures-odbc.md)  
  
-   [Batch di istruzioni SQL](../../../odbc/reference/develop-app/batches-of-sql-statements.md)  
  
-   [Esecuzione delle funzioni di catalogo](../../../odbc/reference/develop-app/executing-catalog-functions.md)
