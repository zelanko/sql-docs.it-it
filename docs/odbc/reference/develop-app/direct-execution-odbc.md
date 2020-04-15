---
title: 'ODBC esecuzione diretta : Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], direct execution
- direct execution [ODBC]
- SQL statements [ODBC], executing
ms.assetid: dd00a535-b136-494f-913b-410838e3de7e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bc5d942ac0c2af54168248d8e416ca233b2c69e6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305162"
---
# <a name="direct-execution-odbc"></a>Esecuzione diretta ODBC
L'esecuzione diretta è il modo più semplice per eseguire un'istruzione. Quando l'istruzione viene inviata per l'esecuzione, l'origine dati la compila in un piano di accesso e quindi esegue tale piano di accesso.  
  
 L'esecuzione diretta viene comunemente utilizzata dalle applicazioni generiche che compilano ed eseguono istruzioni in fase di esecuzione. Ad esempio, il codice seguente compila un'istruzione SQL e la esegue una sola volta:For example, the following code builds an SQL statement and executes it a single time:  
  
```  
SQLCHAR *SQLStatement;  
  
// Build an SQL statement.  
BuildStatement(SQLStatement);  
  
// Execute the statement.  
SQLExecDirect(hstmt, SQLStatement, SQL_NTS);  
```  
  
 L'esecuzione diretta funziona meglio per le istruzioni che verranno eseguite una sola volta. Il suo principale inconveniente è che l'istruzione SQL viene analizzata ogni volta che viene eseguita. Inoltre, l'applicazione non può recuperare informazioni sul set di risultati creato dall'istruzione (se presente) fino a dopo l'esecuzione dell'istruzione; Ciò è possibile se l'istruzione viene preparata ed eseguita in due passaggi separati.  
  
 Per eseguire direttamente un'istruzione, l'applicazione esegue le azioni seguenti:To execute a statement directly, the application performs the following actions:  
  
1.  Imposta i valori di tutti i parametri. Per ulteriori informazioni, vedere [Parametri dell'istruzione](../../../odbc/reference/develop-app/statement-parameters.md)più avanti in questa sezione.  
  
2.  Chiama **SQLExecDirect** e passa una stringa contenente l'istruzione SQL.  
  
3.  Quando **SQLExecDirect** viene chiamato, il driver:  
  
    -   Modifica l'istruzione SQL per utilizzare la grammatica SQL dell'origine dati senza analizzare l'istruzione. ciò include la sostituzione delle sequenze di escape descritte in Sequenze di [escape in ODBC.](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md) L'applicazione può recuperare il formato modificato di un'istruzione SQL chiamando **SQLNativeSql**. Le sequenze di escape non vengono sostituite se è impostato l'attributo dell'istruzione SQL_ATTR_NOSCAN.  
  
    -   Recupera i valori dei parametri correnti e li converte in base alle esigenze. Per ulteriori informazioni, vedere [Parametri dell'istruzione](../../../odbc/reference/develop-app/statement-parameters.md)più avanti in questa sezione.  
  
    -   Invia l'istruzione e i valori dei parametri convertiti all'origine dati per l'esecuzione.  
  
    -   Restituisce eventuali errori. Questi includono la sequenza o la diagnostica dello stato, ad esempio SQLSTATE 24000 (stato del cursore non valido), errori sintattici come SQLSTATE 42000 (errore di sintassi o violazione di accesso) e gli errori semantici come SQLSTATE 42S02 (tabella di base o vista non trovata).
