---
title: Esecuzione diretta ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 73c061718dc326e43f72be369a28ad12726a3cab
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63242358"
---
# <a name="direct-execution-odbc"></a>Esecuzione diretta ODBC
Esecuzione diretta è il modo più semplice per eseguire un'istruzione. Quando l'istruzione viene inviata per l'esecuzione, l'origine dati lo compila in un piano di accesso e quindi esegue il piano di accesso.  
  
 Esecuzione diretta viene comunemente utilizzata dalle applicazioni generiche che compilano ed eseguono le istruzioni in fase di esecuzione. Ad esempio, il codice seguente compila un'istruzione SQL e viene eseguito una sola volta:  
  
```  
SQLCHAR *SQLStatement;  
  
// Build an SQL statement.  
BuildStatement(SQLStatement);  
  
// Execute the statement.  
SQLExecDirect(hstmt, SQLStatement, SQL_NTS);  
```  
  
 Esecuzione diretta risulta più adatta per le istruzioni che verranno eseguite una sola volta. Il principale svantaggio è che l'istruzione SQL viene analizzata ogni volta che viene eseguita. Inoltre, l'applicazione non è possibile recuperare le informazioni sul set di risultati creati tramite l'istruzione (se presente) fino a quando l'istruzione viene eseguita; Ciò è possibile se l'istruzione viene preparata ed eseguita in due passaggi distinti.  
  
 Per eseguire un'istruzione direttamente, l'applicazione esegue le azioni seguenti:  
  
1.  Imposta i valori dei parametri. Per altre informazioni, vedere [parametri delle istruzioni](../../../odbc/reference/develop-app/statement-parameters.md), più avanti in questa sezione.  
  
2.  Le chiamate **SQLExecDirect** e lo passa a una stringa contenente l'istruzione SQL.  
  
3.  Quando **SQLExecDirect** viene chiamato, il driver:  
  
    -   Modifica l'istruzione SQL per usare la grammatica SQL dell'origine dati senza analizzare l'istruzione. sono inclusi sostituendo le sequenze di escape descritte in [sequenze di Escape in ODBC](../../../odbc/reference/develop-app/escape-sequences-in-odbc.md). L'applicazione può recuperare il modulo di un'istruzione SQL modificato chiamando **SQLNativeSql**. Se è impostato l'attributo di istruzione SQL_ATTR_NOSCAN, le sequenze di escape non vengono sostituite.  
  
    -   Recupera i valori di parametro corrente e li converte in base alle esigenze. Per altre informazioni, vedere [parametri delle istruzioni](../../../odbc/reference/develop-app/statement-parameters.md), più avanti in questa sezione.  
  
    -   Invia l'istruzione e i valori dei parametri convertiti all'origine dati per l'esecuzione.  
  
    -   Restituisce gli eventuali errori. Queste includono la sequenziazione o diagnostica stato ad esempio SQLSTATE 24000 (stato del cursore non valido), errori sintattici, ad esempio SQLSTATE 42000 (sintassi o violazione di accesso) e gli errori semantici, ad esempio SQLSTATE 42S02 (di Base nella tabella o vista non trovato).
