---
title: Gestione degli errori | Microsoft Docs
ms.custom: ''
ms.date: 01/21/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 8fd5b5ef-d939-4b78-b900-5b7b6ddb3eb9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 535881ed3ece30996390af6c9a22568d49bc6d3e
ms.sourcegitcommit: 879a5c6eca99e0e9cc946c653d4ced165905d9c6
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 02/05/2019
ms.locfileid: "55736967"
---
# <a name="handling-errors"></a>Gestione degli errori
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  Quando si usa [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)], tutte le condizioni di errore del database vengono restituite all'applicazione Java come eccezioni tramite la classe [SQLServerException](../../connect/jdbc/reference/sqlserverexception-class.md). I metodi seguenti della classe SQLServerException sono ereditati da java.sql.SQLException e java.lang.Throwable. Possono essere usati per restituire informazioni specifiche sull'errore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] che si è verificato:  
  
-   `getSQLState()` restituisce il codice di stato standard X/Open o SQL99 dell'eccezione.
  
-   `getErrorCode()` restituisce il numero di errore del database specifico.
  
-   `getMessage()` restituisce il testo completo dell'eccezione. Nel testo del messaggio di errore viene descritto il problema e spesso sono inclusi i segnaposto per le informazioni, ad esempio i nomi degli oggetti, che sono inseriti nel messaggio di errore quando viene visualizzato.
  
-   `getNextException()` restituisce l'oggetto `SQLServerException` successivo o Null se non sono più disponibili oggetti eccezione da restituire.

-   `getSQLServerError()` Restituisce il `SQLServerError` oggetto contenente informazioni dettagliate relative all'eccezione così come viene ricevuto da SQL Server. Questo metodo restituisce null se si è verificato alcun errore del server.

I metodi seguenti del `SQLServerError` classe può essere utilizzata per ottenere ulteriori dettagli sull'errore generato dal server.

-   `SQLServerError.getErrorMessage()` Restituisce il messaggio di errore ricevuto dal server.

-   `SQLServerError.getErrorNumber()` Restituisce un numero che identifica il tipo dell'errore.

-   `SQLServerError.getErrorState()` Restituisce un codice di errore numerico da SQL Server che rappresenta un errore, avviso o messaggio di "dati non trovati".

-   `SQLServerError.getErrorSeverity()` Restituisce il livello di gravità dell'errore ricevuto.

-   `SQLServerError.getServerName()` Restituisce il nome del computer in cui è in esecuzione un'istanza di SQL Server che ha generato l'errore.

-   `SQLServerError.getProcedureName()` Restituisce il nome della stored procedure o della chiamata di procedura remota (RPC) che ha generato l'errore.

-   `SQLServerError.getLineNumber()` Restituisce il numero di riga all'interno del batch di comandi Transact-SQL o stored procedure che ha generato l'errore.
  
 Nell'esempio seguente viene passata alla funzione una connessione aperta al database di esempio [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal_md.md)] di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e viene costruita un'istruzione SQL in formato non corretto che non contiene la clausola FROM. L'istruzione viene quindi eseguita con conseguente elaborazione di un'eccezione SQL.  
  
 [!code[JDBC#HandlingErrors1](../../connect/jdbc/codesnippet/Java/handling-errors_1.java)]  
  
## <a name="see-also"></a>Vedere anche  
 [Diagnosi dei problemi relativi al driver JDBC](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  
