---
title: Chiamate di funzione scalari Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 349599a51b2996f419e6c8656a71bc9e30146542
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304262"
---
# <a name="scalar-function-calls"></a>Chiamate di funzioni scalari
Le funzioni scalari restituiscono un valore per ogni riga. Ad esempio, la funzione scalare valore assoluto accetta una colonna numerica come argomento e restituisce il valore assoluto di ogni valore nella colonna. La sequenza di escape per chiamare una funzione scalare è  
  
 Funzione_scalare_ **}** **fn**    
  
 dove *funzione scalare* è una delle funzioni elencate [nell'Appendice E: Funzioni scalari](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md). Per altre informazioni sulla sequenza di escape della funzione scalare, vedere Sequenza di escape delle funzioni [scalari](../../../odbc/reference/appendixes/scalar-function-escape-sequence.md) nell'Appendice C: Grammatica SQL.  
  
 Ad esempio, le istruzioni SQL seguenti creano lo stesso set di risultati di nomi di clienti maiuscoli. La prima istruzione utilizza la sintassi della sequenza di escape. La seconda istruzione utilizza la sintassi nativa per Ingres per OS/2 e non è interoperabile.  
  
```  
SELECT {fn UCASE(Name)} FROM Customers  
  
SELECT uppercase(Name) FROM Customers  
```  
  
 Un'applicazione può combinare chiamate a funzioni scalari che utilizzano la sintassi nativa e chiamate a funzioni scalari che utilizzano la sintassi ODBC. Si supponga, ad esempio, che i nomi nella tabella Employee vengano archiviati come cognome, virgola e nome. L'istruzione SQL seguente crea un set di risultati di cognomi di dipendenti nella tabella Employee. L'istruzione utilizza la funzione scalare ODBC **SUBSTRING** e la funzione scalare di SQL Server **CHARINDEX** e verrà eseguita correttamente solo in SQL Server.  
  
```  
SELECT {fn SUBSTRING(Name, 1, CHARINDEX(',', Name) - 1)} FROM Customers  
```  
  
 Per la massima interoperabilità, le applicazioni devono utilizzare la funzione scalare **CONVERT** per assicurarsi che l'output di una funzione scalare sia il tipo richiesto. La funzione **CONVERTI** converte i dati da un tipo di dati SQL al tipo di dati SQL specificato. La sintassi della funzione **CONVERT** è  
  
 **CONVERT(** _value_exp_ **,** _data_type_**)**  
  
 dove *value_exp* è un nome di colonna, il risultato di un'altra funzione scalare o un valore letterale e *data_type* è una parola chiave che corrisponde al nome **#define** utilizzato da un identificatore del tipo di dati SQL come definito [nell'Appendice D: Tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md). Ad esempio, l'istruzione SQL seguente utilizza la funzione **CONVERT** per assicurarsi che l'output della funzione **CURDATE** sia una data, anziché dati timestamp o di tipo carattere:  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, {fn CONVERT({fn CURDATE()}, SQL_DATE)}, ?, ?)  
```  
  
 Per determinare quali funzioni scalari sono supportate da un'origine dati, un'applicazione chiama **SQLGetInfo** con le opzioni SQL_CONVERT_FUNCTIONS, SQL_NUMERIC_FUNCTIONS, SQL_STRING_FUNCTIONS, SQL_SYSTEM_FUNCTIONS e SQL_TIMEDATE_FUNCTIONS. Per determinare quali operazioni di conversione sono supportate dalla funzione **CONVERT,** un'applicazione chiama **SQLGetInfo** con una delle opzioni che iniziano con SQL_CONVERT.
