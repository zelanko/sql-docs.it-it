---
title: Dimensione colonna, Cifre decimali, Trasferimento Lunghezza ottetto, Dimensione visualizzazione Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 55b8e9dd305764a89601e9ffd5a337e42a8d8db3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306572"
---
# <a name="column-size-decimal-digits-transfer-octet-length-and-display-size---odbc"></a>Dimensioni colonna, cifre decimali, lunghezza dell'ottetto di trasferimento e dimensione di visualizzazione - ODBCColumn Size, Decimal Digits, Transfer Octet Length, and Display Size - ODBC
I tipi di dati sono caratterizzati dalla dimensione della colonna (o del parametro), dalle cifre decimali, dalla lunghezza e dalle dimensioni di visualizzazione. Le funzioni ODBC seguenti restituiscono questi attributi per un parametro in un'istruzione SQL o per un tipo di dati SQL in un'origine dati. Ogni funzione ODBC restituisce un set diverso di questi attributi, come indicato di seguito:Each ODBC function returns a different set of these attributes, as follows:  
  
-   **SQLDescribeCol** restituisce la dimensione della colonna e le cifre decimali delle colonne che descrive.  
  
-   **SQLDescribeParam** restituisce la dimensione del parametro e le cifre decimali dei parametri che descrive. **SQLBindParameter** imposta la dimensione del parametro e le cifre decimali per un parametro in un'istruzione SQL.  
  
-   Le funzioni di catalogo **SQLColumns**, **SQLProcedureColumns**e **SQLGetTypeInfo** restituiscono attributi per una colonna in una tabella, set di risultati o un parametro di routine e gli attributi di catalogo dei tipi di dati nell'origine dati. **SQLColumns** restituisce la dimensione della colonna, le cifre decimali e la lunghezza di una colonna nelle tabelle specificate (ad esempio la tabella di base, la vista o una tabella di sistema). **SQLProcedureColumns** restituisce la dimensione della colonna, cifre decimali e la lunghezza di una colonna in una procedura. **SQLGetTypeInfo** restituisce la dimensione massima della colonna e le cifre decimali minime e massime di un tipo di dati SQL in un'origine dati.  
  
 I valori restituiti da queste funzioni per la dimensione della colonna o del parametro corrispondono a "precisione" come definito in ODBC 2. *x*. Tuttavia, i valori non corrispondono necessariamente ai valori restituiti in SQL_DESC_PRECISION o in qualsiasi altro campo descrittore. Lo stesso vale per le cifre decimali, che corrispondono alla "scala" come definito in ODBC 2. *x*. Non corrisponde necessariamente ai valori restituiti in SQL_DESC_SCALE o in qualsiasi altro campo descrittore, ma proviene da campi del descrittore diversi a seconda del tipo di dati. Per ulteriori informazioni, vedere [Dimensioni delle colonne](../../../odbc/reference/appendixes/column-size.md) e [Cifre decimali](../../../odbc/reference/appendixes/decimal-digits.md).  
  
 Analogamente, i valori per la lunghezza dell'ottetto di trasferimento non provengono da SQL_DESC_LENGTH. Provengono dalla SQL_DESC_OCTET_LENGTH di un campo di un descrittore per tutti i tipi di caratteri e binari. Non esiste un campo descrittore che contiene queste informazioni per altri tipi.  
  
 Il valore della dimensione di visualizzazione per tutti i tipi di dati corrisponde al valore in un singolo campo descrittore, SQL_DESC_DISPLAY_SIZE.  
  
 I campi del descrittore descrivono le caratteristiche di un set di risultati. I campi del descrittore non contengono valori validi sui dati prima dell'esecuzione dell'istruzione. I valori per le dimensioni della colonna, le cifre decimali e le dimensioni di visualizzazione restituite da **SQLColumns**, **SQLProcedureColumns**e **SQLGetTypeInfo**, d'altra parte, restituiscono caratteristiche degli oggetti di database, ad esempio le colonne della tabella e i tipi di dati, presenti nel catalogo dell'origine dati. Analogamente, nel set di risultati, **SQLColAttribute** restituisce la dimensione della colonna, le cifre decimali e la lunghezza dell'ottetto di trasferimento delle colonne nell'origine dati. questi valori non sono necessariamente gli stessi dei campi del SQL_DESC_PRECISION, della SQL_DESC_SCALE e del descrittore SQL_DESC_OCTET_LENGTH.  
  
 Per ulteriori informazioni su questi campi descrittore, vedere [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 Argomenti correlati:  
  
-   [Dimensioni della colonna](../../../odbc/reference/appendixes/column-size.md)  
-   [Cifre decimali](../../../odbc/reference/appendixes/decimal-digits.md)  
-   [Lunghezza dell'ottetto di trasferimento](../../../odbc/reference/appendixes/transfer-octet-length.md)  
-   [Dimensioni di visualizzazione](../../../odbc/reference/appendixes/display-size.md)
