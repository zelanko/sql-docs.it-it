---
title: Utilizzo di cursori a blocchi | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68135543"
---
# <a name="using-block-cursors"></a>Uso di cursori rettangolari
Il supporto per i cursori a blocchi è incorporato in ODBC 3. *x*. **SQLFetch** può essere utilizzato solo per le operazioni di recupero più righe quando viene chiamato in ODBC 3. *x*; Se ODBC 2. *x* l'applicazione chiama **SQLFetch**. verrà aperto solo un cursore di sola riga e di sola trasmissione. Quando ODBC 3. *x* l'applicazione chiama **SQLFetch** in ODBC 2. *x* driver restituisce una singola riga, a meno che il driver non supporti **SQLExtendedFetch**. Per ulteriori informazioni, vedere [cursori a blocchi, cursori scorrevoli e compatibilità con le versioni precedenti](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) in Appendice G: linee guida per la compatibilità con le versioni precedenti.  
  
 Per utilizzare i cursori a blocchi, l'applicazione imposta le dimensioni del set di righe, associa i buffer del set di righe (come descritto nella sezione precedente), imposta facoltativamente gli attributi SQL_ATTR_ROWS_FETCHED_PTR e SQL_ATTR_ROW_STATUS_PTR istruzione e chiama **SQLFetch** o **SQLFetchScroll** per recuperare un blocco di righe. L'applicazione può modificare le dimensioni del set di righe e associare nuovi buffer del set di righe (chiamando **SQLBindCol** o specificando un offset di binding) anche dopo il recupero delle righe.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Dimensione del set di righe](../../../odbc/reference/develop-app/rowset-size.md)  
  
-   [Numero di righe recuperate e stato](../../../odbc/reference/develop-app/number-of-rows-fetched-and-status.md)  
  
-   [SQLGetData e cursori a blocchi; blocca Curso](../../../odbc/reference/develop-app/sqlgetdata-and-block-cursors.md)
