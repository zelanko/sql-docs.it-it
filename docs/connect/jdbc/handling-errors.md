---
title: Gestione degli errori | Microsoft Docs
ms.custom: ''
ms.date: 08/12/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8fd5b5ef-d939-4b78-b900-5b7b6ddb3eb9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6277b3ecf0160078fa47bc79994d31f64519d9b7
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "69028033"
---
# <a name="handling-errors"></a>Gestione degli errori
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Quando si usa [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], tutte le condizioni di errore del database vengono restituite all'applicazione Java come eccezioni tramite la classe [SQLServerException](../../connect/jdbc/reference/sqlserverexception-class.md). I metodi seguenti della classe SQLServerException sono ereditati da java.sql.SQLException e java.lang.Throwable. Possono essere usati per restituire informazioni specifiche sull'errore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che si è verificato:  
  
-   `getSQLState()` restituisce il codice di stato standard X/Open o SQL99 dell'eccezione.
  
-   `getErrorCode()` restituisce il numero di errore del database specifico.
  
-   `getMessage()` restituisce il testo completo dell'eccezione. Nel testo del messaggio di errore viene descritto il problema e spesso sono inclusi i segnaposto per le informazioni, ad esempio i nomi degli oggetti, che sono inseriti nel messaggio di errore quando viene visualizzato.
  
-   `getNextException()` restituisce l'oggetto `SQLServerException` successivo o Null se non sono più disponibili oggetti eccezione da restituire.

-   `getSQLServerError()` restituisce l'oggetto `SQLServerError` contenente informazioni dettagliate sull'eccezione ricevute da SQL Server. Questo metodo restituisce null se non si è verificato nessun errore del server.

Per ottenere ulteriori dettagli sull'errore generato dal server, è possibile usare i metodi seguenti della classe `SQLServerError`.

-   `SQLServerError.getErrorMessage()` restituisce il messaggio di errore ricevuto dal server.

-   `SQLServerError.getErrorNumber()` restituisce un numero che identifica il tipo di errore.

-   `SQLServerError.getErrorState()` restituisce un codice di errore numerico di SQL Server che rappresenta un messaggio di errore, un avviso o "Impossibile trovare dati".

-   `SQLServerError.getErrorSeverity()` restituisce il livello di gravità dell'errore.

-   `SQLServerError.getServerName()` restituisce il nome del computer in cui è in esecuzione un'istanza di SQL Server che ha generato l'errore.

-   `SQLServerError.getProcedureName()` Restituisce il nome della stored procedure o della chiamata di procedura remota (RPC) che ha generato l'errore.

-   `SQLServerError.getLineNumber()` restituisce il numero di riga nel batch dei comandi Transact-SQL o nella stored procedure che ha generato l'errore.
  
 Nell'esempio seguente viene passata alla funzione una connessione aperta al database di esempio [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e viene costruita un'istruzione SQL in formato non corretto che non contiene la clausola FROM. L'istruzione viene quindi eseguita con conseguente elaborazione di un'eccezione SQL.  
  
 [!code[JDBC#HandlingErrors1](../../connect/jdbc/codesnippet/Java/handling-errors_1.java)]  
  
## <a name="see-also"></a>Vedere anche  
 [Diagnosi dei problemi relativi al driver JDBC](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
