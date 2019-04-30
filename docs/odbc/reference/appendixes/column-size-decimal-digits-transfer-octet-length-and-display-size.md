---
title: Le dimensioni di colonna, cifre decimali, lunghezza dell'ottetto di trasferimento, dimensioni di visualizzazione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- display size of data types [ODBC]
- data types [ODBC], column size
- transfer octet length of data types [ODBC]
- size of data types [ODBC]
- data types [ODBC], display size
- decimal digits of data types [ODBC]
- data types [ODBC], decimal digits
- SQL data types [ODBC], column characteristics
- column size of data types [ODBC]
- data types [ODBC], transfer octet length
ms.assetid: 723107a1-be08-4ea3-a8c0-b2c45d38d1aa
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ba21e2a13b755c938c8b1bdc321a5f23bf87c29f
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63213310"
---
# <a name="column-size-decimal-digits-transfer-octet-length-and-display-size---odbc"></a>Le dimensioni di colonna, cifre decimali, lunghezza trasferimento in ottetti e visualizzare le dimensioni - ODBC
Tipi di dati sono caratterizzati dalle loro dimensioni di colonna (o parametro), cifre decimali, lunghezza e dimensioni di visualizzazione. Le funzioni ODBC seguenti restituiscono questi attributi per un parametro in un'istruzione SQL o per un tipo di dati SQL in un'origine dati. Ogni funzione ODBC restituisce un set diverso di questi attributi, come indicato di seguito:  
  
-   **SQLDescribeCol** restituisce cifre decimali e dimensione delle colonne vengono descritte la colonna.  
  
-   **SQLDescribeParam** restituisce il parametro di cifre decimali e le dimensioni dei parametri viene descritto. **SQLBindParameter** imposta il parametro di cifre decimali e dimensioni per un parametro in un'istruzione SQL.  
  
-   Le funzioni di catalogo **SQLColumns**, **SQLProcedureColumns**, e **SQLGetTypeInfo** restituisce gli attributi per una colonna in una tabella, set di risultati o un parametro di routine e gli attributi di catalogo di tipi di dati nell'origine dati. **SQLColumns** restituisce le dimensioni della colonna, cifre decimali e lunghezza di una colonna nelle tabelle specificate (ad esempio, la tabella di base, vista o tabella di sistema). **SQLProcedureColumns** restituisce le dimensioni della colonna, cifre decimali e lunghezza di una colonna in una procedura. **SQLGetTypeInfo** restituisce la dimensione massima delle colonne e le cifre decimali minime e massime di un tipo di dati SQL in un'origine dati.  
  
 I valori restituiti da queste funzioni per la colonna o parametro di dimensione corrispondenti alla "precisione" come definita in ODBC 2. *x*. Tuttavia, i valori non corrispondono necessariamente ai valori restituiti in SQL_DESC_PRECISION o qualsiasi altro campo del descrittore uno. Lo stesso vale per le cifre decimali, che corrispondono a "scalabilità" come definita in ODBC 2. *x*. Ma non necessariamente corrispondono ai valori restituiti in SQL_DESC_SCALE o qualsiasi altro campo del descrittore uno proviene da campi di descrizione diversi a seconda del tipo di dati. Per altre informazioni, vedere [dimensione della colonna](../../../odbc/reference/appendixes/column-size.md) e [cifre decimali](../../../odbc/reference/appendixes/decimal-digits.md).  
  
 Analogamente, i valori per la lunghezza dell'ottetto di trasferimento non sono concessi da SQL_DESC_LENGTH. Provengano da SQL_DESC_OCTET_LENGTH di un campo di un descrittore per tutti i tipi carattere e binario. Non c'è alcun campo descrittore che contiene queste informazioni per altri tipi.  
  
 Il valore delle dimensioni di visualizzazione per tutti i tipi di dati corrisponde al valore in un campo del descrittore single, SQL_DESC_DISPLAY_SIZE.  
  
 I campi di descrizione vengono descritte le caratteristiche di un set di risultati. I campi di descrizione non contengono i valori validi sui dati prima dell'esecuzione dell'istruzione. I valori della colonna dimensione, cifre decimali e la visualizzazione di dimensioni restituite dal **SQLColumns**, **SQLProcedureColumns**, e **SQLGetTypeInfo**, da altra parte, restituire caratteristiche degli oggetti di database, ad esempio le colonne della tabella e tipi di dati, che esiste nel catalogo dell'origine dati. Analogamente, nel relativo set di risultati **SQLColAttribute** restituisce le dimensioni della colonna, cifre decimali e lunghezza dell'ottetto di trasferimento delle colonne nell'origine dati; questi valori non sono necessariamente lo stesso come i valori di SQL_DESC_PRECISION, SQL _ DESC_SCALE e campi di descrizione SQL_DESC_OCTET_LENGTH.  
  
 Per altre informazioni su questi campi di descrizione, vedere [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 Argomenti correlati:  
  
-   [Dimensione colonna](../../../odbc/reference/appendixes/column-size.md)  
-   [Cifre decimali](../../../odbc/reference/appendixes/decimal-digits.md)  
-   [Lunghezza dell'ottetto di trasferimento](../../../odbc/reference/appendixes/transfer-octet-length.md)  
-   [Dimensioni di visualizzazione](../../../odbc/reference/appendixes/display-size.md)
