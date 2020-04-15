---
title: Proprietà Handles . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 713c2a71ec195b75d682b97239413e98d07b5861
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300211"
---
# <a name="handles"></a>Selettori
Le maniglie sono valori opachi a 32 bit che identificano un particolare elemento; in ODBC, questo elemento può essere un ambiente, una connessione, un'istruzione o un descrittore. Quando l'applicazione chiama **SQLAllocHandle**, Gestione Driver o driver crea un nuovo elemento del tipo specificato e restituisce il relativo handle all'applicazione. L'applicazione in un secondo momento utilizza l'handle per identificare l'elemento quando si chiamano le funzioni ODBC. Gestione Driver e driver utilizzano l'handle per individuare le informazioni sull'elemento.  
  
 Ad esempio, nel codice seguente vengono utilizzati due handle di istruzione (*hstmtOrder* e *hstmtLine*) per identificare le istruzioni in cui creare set di risultati di ordini cliente e numeri di riga ordine cliente. In seguito viene utilizzato questi handle per identificare il set di risultati da cui recuperare i dati.  
  
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
  
 Gli handle sono significativi solo per il componente ODBC che li ha creati; vale a dire, solo Driver Manager in grado di interpretare gli handle di Driver Manager e solo un driver in grado di interpretare i propri handle.  
  
 Si supponga, ad esempio, che il driver nell'esempio precedente allochi una struttura per archiviare le informazioni su un'istruzione e restituisca il puntatore a questa struttura come handle dell'istruzione. Quando l'applicazione chiama **SQLPrepare**, passa un'istruzione SQL e l'handle dell'istruzione utilizzata per i numeri di riga dell'ordine cliente. Il driver invia l'istruzione SQL all'origine dati, che la prepara e restituisce un identificatore del piano di accesso. Il driver utilizza l'handle per trovare la struttura in cui archiviare questo identificatore.  
  
 Successivamente, quando l'applicazione chiama **SQLExecute** per generare il set di risultati dei numeri di riga per un determinato ordine cliente, passa lo stesso handle. Il driver utilizza l'handle per recuperare l'identificatore del piano di accesso dalla struttura. Invia l'identificatore all'origine dati per indicare quale piano eseguire.  
  
 ODBC dispone di due livelli di handle: handle di Gestione Driver e handle di driver. L'applicazione utilizza gli handle di Gestione Driver quando si chiamano le funzioni ODBC perché chiama tali funzioni in Gestione Driver. Gestione Driver utilizza questo handle per trovare l'handle del driver corrispondente e utilizza l'handle del driver quando si chiama la funzione nel driver. Per un esempio di utilizzo degli handle di Driver e Gestione Driver, vedere [Gestione Driver nel processo](../../../odbc/reference/develop-app/driver-manager-s-role-in-the-connection-process.md)di connessione .  
  
 Che esistono due livelli di handle è un elemento dell'architettura ODBC; nella maggior parte dei casi, non è rilevante né per l'applicazione né per il conducente. Sebbene in genere non vi sia alcun motivo per eseguire questa operazione, è possibile che l'applicazione determini gli handle del driver chiamando **SQLGetInfo**.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Handle di ambiente](../../../odbc/reference/develop-app/environment-handles.md)  
  
-   [Handle di connessione](../../../odbc/reference/develop-app/connection-handles.md)  
  
-   [Handle di istruzione](../../../odbc/reference/develop-app/statement-handles.md)  
  
-   [Handle del descrittore](../../../odbc/reference/develop-app/descriptor-handles.md)  
  
-   [Transizioni di stato](../../../odbc/reference/develop-app/state-transitions.md)
