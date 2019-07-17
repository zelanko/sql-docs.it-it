---
title: Utilizzo di cursori rettangolari | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], block
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 2aad7d6b-216e-47e7-b3cb-f95ad096f21a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 529b71540b4abde5fce868975fcbf2749e31dc8e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68135543"
---
# <a name="using-block-cursors"></a>Uso di cursori rettangolari
Supporto per cursori a blocchi è incorporato in ODBC 3. *x*. **SQLFetch** può essere usato solo per operazioni di recupero con più righe quando viene chiamato in ODBC 3. *x*; se un database ODBC 2. *x* applicazione chiama **SQLFetch**, verrà aperta solo un singola riga-cursore forward only. Quando un'applicazione ODBC 3. *x* applicazione chiama **SQLFetch** in un'API ODBC 2. *x* driver, restituisce una singola riga, a meno che il driver supporta **SQLExtendedFetch**. Per altre informazioni, vedere [cursori rettangolari, cursori scorrevoli e compatibilità con le versioni precedenti](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) nell'appendice g: Driver linee guida per la compatibilità con le versioni precedenti.  
  
 Per utilizzare cursori a blocchi, l'applicazione imposta le dimensioni del set di righe, associa il buffer di righe (come descritto nella sezione precedente), facoltativamente, imposta gli attributi di istruzione vengono impostati SQL_ATTR_ROW_STATUS_PTR e SQL_ATTR_ROWS_FETCHED_PTR e chiamate **SQLFetch**  oppure **SQLFetchScroll** per recuperare un blocco di righe. L'applicazione può modificare le dimensioni del set di righe e associare nuovi buffer di set di righe (chiamando **SQLBindCol** o specificando un offset di bind) anche dopo le righe recuperate.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Dimensione del set di righe](../../../odbc/reference/develop-app/rowset-size.md)  
  
-   [Numero di righe recuperate e stato](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)  
  
-   [SQLGetData e cursori a blocchi; bloccare un cursore](../../../odbc/reference/develop-app/sqlgetdata-and-block-cursors.md)
