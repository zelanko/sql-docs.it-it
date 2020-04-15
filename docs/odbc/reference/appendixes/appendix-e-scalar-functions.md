---
title: 'Appendice E: Funzioni scalari Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL-92 functions [ODBC]
- scalar functions [ODBC]
- functions [ODBC], scalar
ms.assetid: 59c7cd5e-32d6-43ab-bac3-7010322d105a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ea354a7f882bd1a75c5f16fb19350d69ca11d375
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81292491"
---
# <a name="appendix-e-scalar-functions"></a>Appendice E: Funzioni scalari
ODBC specifica i seguenti tipi di funzioni scalari, con informazioni dettagliate su ciascuno di questi tipi di funzione forniti nelle sezioni corrispondenti di questa appendice. Le descrizioni delle funzioni includono la sintassi associata.  
  
 Questa appendice contiene i seguenti argomenti.  
  
-   [Funzioni stringa](../../../odbc/reference/appendixes/string-functions.md)  
  
-   [Funzioni numeriche](../../../odbc/reference/appendixes/numeric-functions.md)  
  
-   [Funzioni di data, ora e intervallo](../../../odbc/reference/appendixes/time-date-and-interval-functions.md)  
  
-   [Funzioni di sistema](../../../odbc/reference/appendixes/system-functions.md)  
  
-   [Funzione di conversione esplicita del tipo di dati](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)  
  
-   [Funzione SQL-92 CAST](../../../odbc/reference/appendixes/sql-92-cast-function.md)  
  
 ODBC non impone un tipo di dati per i valori restituiti dalle funzioni scalari perché le funzioni sono spesso specifiche dell'origine dati. Le applicazioni devono utilizzare la funzione scalare CONVERT quando possibile per forzare la conversione del tipo di dati.  
  
## <a name="odbc-and-sql-92-scalar-functions"></a>ODBC and SQL-92 Scalar Functions  
 Le tabelle di questa appendice includono funzioni aggiunte in ODBC 3.0 per l'allineamento con SQL-92. Le funzioni aggiunte per un particolare tipo di funzione scalare, come definito in ODBC, sono indicate in ogni sezione.  
  
 ODBC e SQL-92 classificano le funzioni scalari in modo diverso. ODBC classifica le funzioni scalari in base al tipo di argomento. SQL-92 li classifica in base al valore restituito. Ad esempio, la funzione EXTRACT viene classificata come funzione timedate da ODBC, poiché l'argomento del campo di estrazione è una parola chiave datetime e l'argomento extract-source è un'espressione datetime o interval. SQL-92, d'altra parte, classifica EXTRACT come funzione scalare numerica, perché il valore restituito è un valore numerico.  
  
 Un'applicazione può determinare le funzioni scalari supportate da un driver chiamando **SQLGetInfo**. I tipi di informazioni sono inclusi sia per ODBC che per le classificazioni SQL-92 delle funzioni scalari. Poiché queste classificazioni sono diverse, il supporto per alcune funzioni scalari può essere indicato nei tipi di informazioni che non corrispondono a ODBC e SQL-92. Ad esempio, il supporto per EXTRACT in ODBC è indicato dal tipo di informazioni SQL_TIMEDATE_FUNCTIONS; il supporto per EXTRACT in SQL-92, d'altra parte, è indicato dal tipo di informazioni SQL_SQL92_NUMERIC_VALUE_FUNCTIONS.
