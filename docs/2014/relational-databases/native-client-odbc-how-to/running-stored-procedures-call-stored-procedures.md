---
title: Stored procedure call (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- stored procedures [ODBC], calling
ms.assetid: 31176be8-d40e-4f93-8d44-a46e804a3e2d
author: rothja
ms.author: jroth
ms.openlocfilehash: 18f9e8742fb01ef0bf3b635d0bdc3fda4e428296
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85048163"
---
# <a name="call-stored-procedures-odbc"></a>Chiamare stored procedure (ODBC)
  Quando un'istruzione SQL chiama un stored procedure utilizzando la clausola di escape ODBC CALL, il driver Microsoft SQL Server invia la procedura a SQL Server utilizzando il meccanismo RPC (Remote stored procedure call). Le richieste RPC ignorano la maggior parte dell'analisi delle istruzioni e dell'elaborazione dei parametri in SQL Server e sono più veloci rispetto a un'istruzione Transact-SQL EXECUTE.  
  
 Per un'applicazione di esempio in cui viene illustrata questa funzionalità, vedere [elaborare i codici restituiti e i parametri di Output &#40;&#41;ODBC ](running-stored-procedures-process-return-codes-and-output-parameters.md).  
  
### <a name="to-run-a-procedure-as-an-rpc"></a>Per eseguire una procedura come RPC  
  
1.  Costruire un'istruzione SQL che utilizzi la sequenza di escape ODBC CALL. Nell'istruzione vengono utilizzati marcatori di parametro per ogni parametro di input, input/output e di output e per il valore restituito della procedura, se disponibile:  
  
    ```  
    {? = CALL procname (?,?)}  
    ```  
  
2.  Chiamare [SQLBindParameter](../native-client-odbc-api/sqlbindparameter.md) per ogni parametro di input, di input/output e di output e per il valore restituito della procedura, se disponibile.  
  
3.  Eseguire l'istruzione con [SQLExecDirect](https://go.microsoft.com/fwlink/?LinkId=58399).  
  
> [!NOTE]  
>  Se un'applicazione invia una procedura utilizzando la sintassi Transact-SQL EXECUTE, invece della sequenza di escape ODBC CALL, il driver ODBC di SQL Server passa la chiamata di procedura a SQL Server come istruzione SQL anziché come chiamata RPC. Se viene utilizzata l'istruzione Transact-SQL EXECUTE, inoltre, i parametri di output non vengono restituiti.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure per l'esecuzione di stored procedure &#40;ODBC&#41;](../../database-engine/dev-guide/running-stored-procedures-how-to-topics-odbc.md)   
 [Invio in batch di chiamate a stored procedure](../native-client-odbc-stored-procedures/batching-stored-procedure-calls.md)   
 [Esecuzione di stored procedure](../native-client-odbc-stored-procedures/running-stored-procedures.md)   
 [Chiamata di una stored procedure](../native-client-odbc-stored-procedures/calling-a-stored-procedure.md)   
 [Procedure](../native-client-odbc-queries/executing-statements/procedures.md)  
  
  
