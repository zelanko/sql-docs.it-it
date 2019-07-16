---
title: Chiamate di funzioni scalari | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- escape sequences [ODBC], scalar function calls
ms.assetid: 10cb4dcf-4cd8-4a56-8725-d080bd3ffe47
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 37209a75c03a051e3def4d26fa0d4e7f85d0e91d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67897744"
---
# <a name="scalar-function-calls"></a>Chiamate di funzioni scalari
Funzioni scalari restituiscono un valore per ogni riga. Ad esempio, la funzione scalare del valore assoluto accetta una colonna numerica come argomento e restituisce il valore assoluto di ogni valore nella colonna. La sequenza di escape per chiamare una funzione scalare  
  
 **{fn**_funzione-scalare_ **}**  
  
 in cui *funzione-scalare* è una delle funzioni elencate [appendice e: Funzioni scalari](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md). Per altre informazioni sulla sequenza di escape di funzione scalare, vedere [sequenza di Escape di funzione scalare](../../../odbc/reference/appendixes/scalar-function-escape-sequence.md) nell'appendice c: Grammatica SQL.  
  
 Le istruzioni SQL seguenti, ad esempio, creano lo stesso set di risultati di lettere maiuscole dei clienti nomi. La prima istruzione Usa la sintassi di escape-sequence. La seconda istruzione viene utilizzata la sintassi nativa per Ingres per il sistema operativo/2 e non è interoperativa.  
  
```  
SELECT {fn UCASE(Name)} FROM Customers  
  
SELECT uppercase(Name) FROM Customers  
```  
  
 Un'applicazione può combinare le chiamate alle funzioni scalari che utilizzano la sintassi nativa e le chiamate a funzioni scalari che usano la sintassi ODBC. Ad esempio, si supponga che i nomi nella tabella dipendente vengono archiviati come un cognome, virgola e un nome. L'istruzione SQL seguente crea un set di risultati dei cognomi dei dipendenti nella tabella Employee. L'istruzione utilizza la funzione scalare ODBC **SOTTOSTRINGA** e la funzione scalare di SQL Server **CHARINDEX** e verrà eseguita correttamente solo in SQL Server.  
  
```  
SELECT {fn SUBSTRING(Name, 1, CHARINDEX(',', Name) - 1)} FROM Customers  
```  
  
 Per garantire la massima interoperabilità, le applicazioni devono usare la **CONVERTIRE** funzione scalare per assicurarsi che l'output di una funzione scalare sia il tipo richiesto. Il **CONVERTIRE** funzione converte i dati da un tipo di dati SQL per il tipo di dati SQL specificato. La sintassi del **CONVERTIRE** è (funzione)  
  
 **CONVERTIRE (** _value_exp_ **,** _data_type_ **)**  
  
 in cui *value_exp* è un nome di colonna, il risultato di un'altra funzione scalare o un valore letterale, e *data_type* è una parola chiave che corrisponde alla **#define** nome utilizzato da un Identificatore del tipo di dati SQL come definito in [appendice d: Tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md). Ad esempio, l'istruzione SQL seguente usa il **CONVERTIRE** funzione per assicurarsi che l'output delle **CURDATE** funzione è una data, invece di un timestamp o un carattere di dati:  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, {fn CONVERT({fn CURDATE()}, SQL_DATE)}, ?, ?)  
```  
  
 Per determinare quali funzioni scalari sono supportate da un'origine dati, un'applicazione chiama **SQLGetInfo** con SQL_CONVERT_FUNCTIONS, SQL_NUMERIC_FUNCTIONS, SQL_STRING_FUNCTIONS, SQL_SYSTEM_FUNCTIONS e SQL_TIMEDATE_ Opzioni di funzioni. Per determinare quali operazioni di conversione supportate dai **CONVERTIRE** funzione, un'applicazione chiama **SQLGetInfo** con una qualsiasi delle opzioni che iniziano con SQL_CONVERT.
