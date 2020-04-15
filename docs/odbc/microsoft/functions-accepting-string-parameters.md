---
title: Funzioni che accettano parametri di stringa Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- desktop database drivers [ODBC], string parameters
- ODBC desktop database drivers [ODBC], string parameters
- Jet-based ODBC drivers [ODBC], string parameters
- functions [ODBC], string parameters
- string parameters [ODBC]
ms.assetid: 869b8421-f71e-4dfd-adce-691bd3012b16
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 01d0f143c72f57e946f7fe2bf52a50910d4e56aa
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286301"
---
# <a name="functions-accepting-string-parameters"></a>Funzioni che accettano parametri stringa
Tutte le funzioni che accettano parametri di stringa verranno convertite in Unicode.All functions that take string parameters will be converted to Unicode. (La forma "W" della funzione verrà esportata.) Il numero di byte viene convertito nel conteggio dei caratteri per le API ODBC applicabili. Questo vale per le seguenti funzioni:  
  
-   **SQLConnect**  
  
-   **SQLDriverConnect**  
  
-   **ATTRIBUTI SQLCol**  
  
-   **SQLDescribeCol**  
  
-   **SQLError** (sostituito da **SQLGetDiagField**)  
  
-   **SQLExecDirect**  
  
-   **SQLGetCursorName**  
  
-   **SQLSetCursorName (Nome cursore)**  
  
-   **SQLGetStmtAttr**  
  
-   **SQLGetInfo**  
  
-   **SQLGetStmtOption** (diventa **SQLGetStmtAttr**)  
  
-   **SQLSetStmtOption** (diventa **SQLSetStmtAttr**)  
  
-   **SQLGetConnectOption (Opzione SQLGetConnectOption)**  
  
-   **Sqlsetconnectoption**  
  
-   **SQLGetTypeInfo**  
  
-   **SQLStatistics**  
  
-   **SQLTables**  
  
-   **SQLNativeSQL (SQLNativeSQL)**  
  
-   **SQLSpecialColumns**  
  
-   **ConfigDSNEx (informazioni in locale)**  
  
-   **ConfigDSN (informazioni in locale)**
