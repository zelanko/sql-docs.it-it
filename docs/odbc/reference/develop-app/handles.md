---
title: Gestisce | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- handles [ODBC]
- driver handles [ODBC]
- driver manager [ODBC], handles
- handles [ODBC], about handles
ms.assetid: f663101e-a4cc-402b-b9d7-84d5e975be71
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d31d36f315291d6826712771d0e3b6b1d8fbc496
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139035"
---
# <a name="handles"></a>Selettori
Gli handle sono opachi a 32 bit di valori che identificano un particolare elemento; in ODBC, questo elemento può essere un ambiente, connessione, istruzione o descrittore. Quando l'applicazione chiama **SQLAllocHandle**, il Driver Manager o il driver consente di creare un nuovo elemento del tipo specificato e restituisce il relativo handle all'applicazione. L'applicazione in un secondo momento Usa l'handle per identificare tale elemento quando si chiama funzioni ODBC. Il gestore dei Driver e il driver utilizza l'handle per individuare informazioni sull'elemento.  
  
 Ad esempio, il codice seguente usa due handle di istruzione (*hstmtOrder* e *hstmtLine*) per identificare le istruzioni in cui creare il set di risultati di sales orders e sales ordinare i numeri di riga. In un secondo momento Usa i punti di controllo per identificare il set di risultati per recuperare i dati da.  
  
```  
SQLHSTMT      hstmtOrder, hstmtLine; // Statement handles.  
SQLUINTEGER   OrderID;  
SQLINTEGER    OrderIDInd = 0;  
SQLRETURN     rc;  
  
// Prepare the statement that retrieves line number information.  
SQLPrepare(hstmtLine, "SELECT * FROM Lines WHERE OrderID = ?", SQL_NTS);  
  
// Bind OrderID to the parameter in the preceding statement.  
SQLBindParameter(hstmtLine, 1, SQL_PARAM_INPUT, SQL_C_ULONG, SQL_INTEGER, 5, 0,  
               &OrderID, 0, &OrderIDInd);  
  
// Bind the result sets for the Order table and the Lines table. Bind  
// OrderID to the OrderID column in the Orders table. When each row is  
// fetched, OrderID will contain the current order ID, which will then be  
// passed as a parameter to the statement tofetch line number  
// information. Code not shown.  
  
// Create a result set of sales orders.  
SQLExecDirect(hstmtOrder, "SELECT * FROM Orders", SQL_NTS);  
  
// Fetch and display the sales order data. Code to check if rc equals  
// SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
while ((rc = SQLFetch(hstmtOrder)) != SQL_NO_DATA) {  
   // Display the sales order data. Code not shown.  
  
   // Create a result set of line numbers for the current sales order.  
   SQLExecute(hstmtLine);  
  
   // Fetch and display the sales order line number data. Code to check  
   // if rc equals SQL_ERROR or SQL_SUCCESS_WITH_INFO not shown.  
   while ((rc = SQLFetch(hstmtLine)) != SQL_NO_DATA) {  
      // Display the sales order line number data. Code not shown.  
   }  
  
   // Close the sales order line number result set.  
   SQLCloseCursor(hstmtLine);  
}  
  
// Close the sales order result set.  
SQLCloseCursor(hstmtOrder);  
```  
  
 Gli handle sono significativi solo per il componente ODBC che ha creato. vale a dire, the Driver Manager può interpretare gli handle di gestione Driver e solo un driver in grado di interpretare i proprio handle.  
  
 Si supponga, ad esempio, il driver nell'esempio precedente viene allocata una struttura per archiviare le informazioni su un'istruzione e restituisce il puntatore alla struttura come l'handle di istruzione. Quando l'applicazione chiama **SQLPrepare**, passa un'istruzione SQL e l'handle di istruzione usato per i numeri di riga ordine di vendita. Il driver invia l'istruzione SQL per l'origine dati che prepara e restituisce un identificatore del piano di accesso. Il driver utilizza l'handle per individuare la struttura in cui archiviare questo identificatore.  
  
 Successivamente, quando l'applicazione chiama **SQLExecute** per generare il set di risultati di numeri di riga per un particolare ordine di vendita, passa l'handle stesso. Il driver utilizza l'handle per recuperare l'identificatore del piano di accesso dalla struttura. Invia l'identificatore per l'origine dati per indicare che pianifica l'esecuzione.  
  
 ODBC prevede due livelli di handle: Handle di Gestione driver e gli handle di driver. L'applicazione usa gli handle di gestione Driver quando si chiama funzioni ODBC perché chiama le funzioni di gestione Driver. Gestione Driver Usa questo handle per trovare l'handle di driver corrispondenti e l'handle del driver quando si chiama la funzione nel driver. Per un esempio di come vengono usati driver e gli handle di gestione Driver, vedere [ruolo di gestione Driver nel processo di connessione](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md).  
  
 Che sono disponibili due livelli di handle è un elemento dell'architettura ODBC; Nella maggior parte dei casi, non è rilevante per l'applicazione o driver. Anche se non è in genere necessario eseguire questa operazione, è possibile che l'applicazione per determinare i punti di controllo driver chiamando **SQLGetInfo**.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Handle di ambiente](../../../odbc/reference/develop-app/environment-handles.md)  
  
-   [Handle di connessione](../../../odbc/reference/develop-app/connection-handles.md)  
  
-   [Handle di istruzione](../../../odbc/reference/develop-app/statement-handles.md)  
  
-   [Handle descrittore](../../../odbc/reference/develop-app/descriptor-handles.md)  
  
-   [Transizioni di stato](../../../odbc/reference/develop-app/state-transitions.md)
