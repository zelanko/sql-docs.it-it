---
title: ODBC di esecuzione diretta | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305162"
---
# <a name="direct-execution-odbc"></a>Esecuzione diretta ODBC
L'esecuzione diretta è il modo più semplice per eseguire un'istruzione. Quando l'istruzione viene inviata per l'esecuzione, l'origine dati la compila in un piano di accesso e quindi esegue tale piano di accesso.  
  
 L'esecuzione diretta è comunemente utilizzata dalle applicazioni generiche che compilano ed eseguono istruzioni in fase di esecuzione. Nel codice seguente, ad esempio, viene compilata un'istruzione SQL che viene eseguita una sola volta:  
  
```  
SQLCHAR *SQLStatement;  
  
// Build an SQL statement.  
BuildStatement(SQLStatement);  
  
// Execute the statement.  
SQLExecDirect(hstmt, SQLStatement, SQL_NTS);  
```  
  
 L'esecuzione diretta funziona meglio per le istruzioni che verranno eseguite una sola volta. Il suo svantaggio principale è che l'istruzione SQL viene analizzata ogni volta che viene eseguita. Inoltre, l'applicazione non è in grado di recuperare informazioni sul set di risultati creato dall'istruzione, se presente, fino a dopo l'esecuzione dell'istruzione. Questo è possibile se l'istruzione viene preparata ed eseguita in due passaggi distinti.  
  
 Per eseguire direttamente un'istruzione, l'applicazione esegue le azioni seguenti:  
  
1.  Imposta i valori di tutti i parametri. Per ulteriori informazioni, vedere [parametri di istruzione](../../../odbc/reference/develop-app/statement-parameters.md), più avanti in questa sezione.  
  
2.  Chiama **SQLExecDirect** e la passa a una stringa contenente l'istruzione SQL.  
  
3.  Quando viene chiamato **SQLExecDirect** , il driver:  
  
    -   Modifica l'istruzione SQL in modo che utilizzi la grammatica SQL dell'origine dati senza analizzare l'istruzione; Ciò include la sostituzione delle sequenze di escape descritte in [sequenze di escape in ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md). L'applicazione può recuperare il formato modificato di un'istruzione SQL chiamando **SQLNativeSql**. Le sequenze di escape non vengono sostituite se è impostato l'attributo dell'istruzione SQL_ATTR_NOSCAN.  
  
    -   Recupera i valori di parametro correnti e li converte secondo necessità. Per ulteriori informazioni, vedere [parametri di istruzione](../../../odbc/reference/develop-app/statement-parameters.md), più avanti in questa sezione.  
  
    -   Invia l'istruzione e i valori dei parametri convertiti all'origine dati per l'esecuzione.  
  
    -   Restituisce eventuali errori. Sono incluse la sequenziazione o la diagnostica dello stato, ad esempio SQLSTATE 24000 (stato del cursore non valido), errori sintattici come SQLSTATE 42000 (errore di sintassi o violazione di accesso) ed errori semantici come SQLSTATE 42S02 (tabella di base o vista non trovata).
