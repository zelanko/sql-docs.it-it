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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67897744"
---
# <a name="scalar-function-calls"></a>Chiamate di funzioni scalari
Le funzioni scalari restituiscono un valore per ogni riga. Ad esempio, la funzione scalare del valore assoluto accetta una colonna numerica come argomento e restituisce il valore assoluto di ogni valore nella colonna. La sequenza di escape per la chiamata di una funzione scalare è  
  
 **{FN**  _-funzione scalare_ **}**  
  
 dove *Scalar-Function* è una delle funzioni elencate in [Appendice E: funzioni scalari](../../../odbc/reference/appendixes/appendix-e-scalar-functions.md). Per ulteriori informazioni sulla sequenza di escape della funzione scalare, vedere [sequenza di escape della funzione scalare](../../../odbc/reference/appendixes/scalar-function-escape-sequence.md) nell'Appendice C: grammatica SQL.  
  
 Le istruzioni SQL seguenti, ad esempio, creano lo stesso set di risultati di nomi di clienti in maiuscolo. La prima istruzione usa la sintassi della sequenza di escape. La seconda istruzione usa la sintassi nativa per Ingres per OS/2 e non è interoperativa.  
  
```  
SELECT {fn UCASE(Name)} FROM Customers  
  
SELECT uppercase(Name) FROM Customers  
```  
  
 Un'applicazione può combinare le chiamate a funzioni scalari che usano la sintassi nativa e le chiamate a funzioni scalari che usano la sintassi ODBC. Si supponga, ad esempio, che i nomi nella tabella Employee siano archiviati come cognome, virgola e nome. Nell'istruzione SQL seguente viene creato un set di risultati con i cognomi dei dipendenti della tabella Employee. L'istruzione utilizza la **SOTTOstringa** della funzione scalare ODBC e la SQL Server funzione scalare **CharIndex** e verrà eseguita correttamente solo su SQL Server.  
  
```  
SELECT {fn SUBSTRING(Name, 1, CHARINDEX(',', Name) - 1)} FROM Customers  
```  
  
 Per garantire la massima interoperabilità, le applicazioni devono utilizzare la funzione **Convert** Scalar per assicurarsi che l'output di una funzione scalare sia il tipo richiesto. La funzione **Convert** converte i dati da un tipo di dati SQL al tipo di dati SQL specificato. La sintassi della funzione **Convert** è  
  
 **Convert (** _value_exp_ **,** _data_type_**)**  
  
 dove *value_exp* è un nome di colonna, il risultato di un'altra funzione scalare o un valore letterale e *data_type* è una parola chiave che corrisponde al nome **#define** utilizzato da un identificatore del tipo di dati SQL come definito nei [tipi di dati Appendice D](../../../odbc/reference/appendixes/appendix-d-data-types.md). Nell'istruzione SQL seguente, ad esempio, viene utilizzata la funzione **Convert** per assicurarsi che l'output della funzione **cagliate** sia una data, anziché un timestamp o dati di tipo carattere:  
  
```  
INSERT INTO Orders (OrderID, CustID, OpenDate, SalesPerson, Status)  
   VALUES (?, ?, {fn CONVERT({fn CURDATE()}, SQL_DATE)}, ?, ?)  
```  
  
 Per determinare quali funzioni scalari sono supportate da un'origine dati, un'applicazione chiama **SQLGetInfo** con le opzioni SQL_CONVERT_FUNCTIONS, SQL_NUMERIC_FUNCTIONS, SQL_STRING_FUNCTIONS, SQL_SYSTEM_FUNCTIONS e SQL_TIMEDATE_FUNCTIONS. Per determinare quali operazioni di conversione sono supportate dalla funzione **Convert** , un'applicazione chiama **SQLGetInfo** con una qualsiasi delle opzioni che iniziano con SQL_CONVERT.
