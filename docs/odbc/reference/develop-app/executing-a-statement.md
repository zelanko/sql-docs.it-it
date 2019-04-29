---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5660cfe2f264e0971d30cd2eaf1aadf68581321e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63032817"
---
# <a name="executing-a-statement"></a>Esecuzione di un'istruzione
Sono disponibili quattro modi per eseguire un'istruzione, a seconda fase di compilazione (preparazione) dal motore di database e chi li definisce:  
  
-   **Esecuzione diretta** l'applicazione definisce l'istruzione SQL. Viene preparata ed eseguita in fase di esecuzione in un unico passaggio.  
  
-   **Esecuzione preparata** l'applicazione definisce l'istruzione SQL. Viene preparata ed eseguita in fase di esecuzione in due passaggi distinti. L'istruzione può essere una volta preparata ed eseguita più volte.  
  
-   **Le procedure** l'applicazione può definire e compilare uno o più istruzioni SQL in fase di sviluppo tempo e archiviano queste istruzioni per l'origine dati come una procedura. La procedura viene eseguita una o più volte in fase di esecuzione. L'applicazione può enumerare le stored procedure disponibili utilizzando funzioni di catalogo.  
  
-   **Funzioni di catalogo** il writer di driver crea una funzione che restituisce un set di risultati predefiniti. In genere, questa funzione Invia un'istruzione SQL predefinita o richiama una procedura creata per questo scopo. La funzione viene eseguita una o più volte in fase di esecuzione.  
  
 Una particolare istruzione (come identificata dal relativo handle di istruzione) può essere eseguite un numero qualsiasi di volte. L'istruzione può essere eseguita con un'ampia gamma di diverse istruzioni SQL o può essere eseguita più volte con la stessa istruzione SQL. Ad esempio, il codice seguente usa lo stesso handle di istruzione (*hstmt1*) per recuperare e visualizzare le tabelle nel database Sales. Quindi riutilizza l'handle per recuperare le colonne in una tabella selezionata dall'utente.  
  
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
  
 E il codice seguente illustra come usare un singolo handle per eseguire ripetutamente la stessa istruzione per eliminare righe da una tabella.  
  
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
  
 Per molti driver, allocando istruzioni è un'attività costosa, pertanto riutilizza la stessa istruzione in questo modo è in genere più efficiente rispetto a liberare istruzioni esistenti e allocazione di nuovi. Le applicazioni che creano set di risultati in un'istruzione è necessario prestare attenzione chiudere il cursore sul risultato del set prima di rieseguire l'istruzione. per altre informazioni, vedere [chiusura del cursore](../../../odbc/reference/develop-app/closing-the-cursor.md).  
  
 Riutilizzo di istruzioni impone anche l'applicazione per evitare una limitazione in alcuni driver del numero di istruzioni che possono essere attive contemporaneamente. La definizione esatta di "attivo" è specifico del driver, ma fa spesso riferimento a qualsiasi istruzione che è stata preparata o eseguita e ha ancora risultati disponibili. Ad esempio, dopo un' **inserire** istruzione è stata preparata, in genere si ritiene di essere attivi; dopo una **selezionare** istruzione è stata eseguita e il cursore è ancora aperto, in genere considerato essere attivo. Dopo che un **CREATE TABLE** istruzione è stata eseguita, non viene considerato a livello generale come attiva.  
  
 Un'applicazione determina quanti istruzioni possono essere attive in una singola connessione alla volta chiamando **SQLGetInfo** con l'opzione SQL_MAX_CONCURRENT_ACTIVITIES. Un'applicazione può usare le istruzioni più attive rispetto a questo limite, aprire più connessioni all'origine dati; Poiché le connessioni possono essere costose, tuttavia, l'impatto sulle prestazioni da considerare.  
  
 Le applicazioni possono limitare la quantità di tempo consentito per un'istruzione da eseguire con l'attributo di istruzione SQL_ATTR_QUERY_TIMEOUT. Se il periodo di timeout scade prima che l'origine dati restituisce il set di risultati, la funzione esegue l'istruzione SQL restituisce SQLSTATE HYT00 (Timeout scaduto). Per impostazione predefinita, non vi è alcun timeout.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Esecuzione diretta](../../../odbc/reference/develop-app/direct-execution-odbc.md)  
  
-   [Esecuzione preparata](../../../odbc/reference/develop-app/prepared-execution-odbc.md)  
  
-   [Procedure](../../../odbc/reference/develop-app/procedures-odbc.md)  
  
-   [Batch di istruzioni SQL](../../../odbc/reference/develop-app/batches-of-sql-statements.md)  
  
-   [Esecuzione delle funzioni di catalogo](../../../odbc/reference/develop-app/executing-catalog-functions.md)
