---
title: 'Appendice e: Funzioni scalari | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 71c80efdb2f4a87537d472ee4b6dc6bdc65af70f
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52540514"
---
# <a name="appendix-e-scalar-functions"></a>Appendice e: Funzioni scalari
ODBC specifica i tipi seguenti di funzioni scalari, con informazioni dettagliate su ognuno di questi tipi funzione forniti nelle sezioni corrispondenti di questa appendice. Descrizioni delle funzioni includono sintassi associata.  
  
 In questa appendice contiene gli argomenti seguenti.  
  
-   [Funzioni per i valori stringa](../../../odbc/reference/appendixes/string-functions.md)  
  
-   [Funzioni numeriche](../../../odbc/reference/appendixes/numeric-functions.md)  
  
-   [Funzioni di data, ora e intervallo](../../../odbc/reference/appendixes/time-date-and-interval-functions.md)  
  
-   [Funzioni di sistema](../../../odbc/reference/appendixes/system-functions.md)  
  
-   [Funzione di conversione esplicita del tipo di dati](../../../odbc/reference/appendixes/explicit-data-type-conversion-function.md)  
  
-   [Funzione SQL-92 CAST](../../../odbc/reference/appendixes/sql-92-cast-function.md)  
  
 ODBC non obbliga a usare un tipo di dati per i valori restituiti dalle funzioni scalari in quanto le funzioni sono spesso specifici dell'origine dati. Le applicazioni devono usare la funzione scalare CONVERT ogni volta che è possibile forzare una conversione tipo di dati.  
  
## <a name="odbc-and-sql-92-scalar-functions"></a>Funzioni scalari ODBC e SQL-92  
 Le tabelle in questa appendice includono funzioni che sono stati aggiunti nella versione 3.0 di ODBC per la compatibilità con SQL-92. Tali funzioni aggiunte per un particolare tipo di funzione scalare, come definito in ODBC sono indicati in ogni sezione.  
  
 ODBC e SQL-92 classificare le funzioni scalari in modo diverso. ODBC classifica le funzioni scalari dal tipo di argomento. SQL-92 li classifica dal valore restituito. Ad esempio, la funzione di estrazione viene classificata come funzione timedate da ODBC, perché l'argomento di estrazione-campo è una parola chiave Data/ora e l'argomento di origine di estrazione è un'espressione datetime o intervallo. SQL-92, d'altra parte, classifica EXTRACT come una funzione scalare di tipo numerica, perché il valore restituito è un valore numerico.  
  
 Un'applicazione può determinare che un driver supporta chiamando le funzioni scalari **SQLGetInfo**. Sono inclusi sia per ODBC per SQL-92 classificazioni delle funzioni scalari per i tipi di informazioni. Poiché queste classificazioni sono diverse, il supporto per alcune funzioni scalari possa essere indicato in tipi di informazioni che non corrispondono a ODBC e SQL-92. Ad esempio, il supporto per l'estrazione in ODBC è indicato dal tipo di informazioni SQL_TIMEDATE_FUNCTIONS; supporto per l'estrazione in SQL-92, d'altra parte, è indicato dal tipo di informazioni SQL_SQL92_NUMERIC_VALUE_FUNCTIONS.
