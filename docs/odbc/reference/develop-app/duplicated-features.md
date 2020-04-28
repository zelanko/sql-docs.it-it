---
title: Funzionalità duplicate | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- duplicated functions [ODBC]
- compatibility [ODBC], duplicated functions
- ODBC drivers [ODBC], backward compatibility
- functions [ODBC], duplicated functions
- backward compatibility [ODBC], duplicated functions
ms.assetid: 641b16bc-f791-46d8-b093-31736473fe3d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 00f5529cfbfacebcad78a0a4433e84f34034694a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300481"
---
# <a name="duplicated-features"></a>Funzionalità duplicate
Le funzioni ODBC *2. x* seguenti sono state duplicate dalle funzioni ODBC *3. x* . Di conseguenza, le funzioni ODBC *2. x* sono deprecate in ODBC *3. x*. Le funzioni ODBC *3. x* sono definite funzioni di sostituzione.  
  
 Quando in un'applicazione viene utilizzata una funzione ODBC *2. x* deprecata e il driver sottostante è un driver ODBC *3. x* , gestione driver esegue il mapping della chiamata di funzione alla funzione sostitutiva corrispondente. L'unica eccezione a questa regola è **SQLExtendedFetch**. (Vedere la nota a piè di pagina alla fine della tabella seguente). Per ulteriori informazioni su questi mapping, vedere [mapping di funzioni deprecate](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) in Appendice G: linee guida per la compatibilità con le versioni precedenti.  
  
 Quando un'applicazione utilizza una funzione di sostituzione e il driver sottostante è un driver ODBC *2. x* , gestione driver esegue il mapping della chiamata di funzione alla funzione deprecata corrispondente.  
  
|Funzione ODBC *2. x*|Funzione ODBC *3. x*|  
|-------------------------|-------------------------|  
|**SQLAllocConnect**|**SQLAllocHandle**|  
|**SQLAllocEnv**|**SQLAllocHandle**|  
|**SQLAllocStmt**|**SQLAllocHandle**|  
|**SQLColAttributes**|**SQLColAttribute**|  
|**SQLError**|**SQLGetDiagRec**|  
|**SQLExtendedFetch**[1]|**SQLFetchScroll**|  
|**SQLFreeConnect**|**SQLFreeHandle**|  
|**SQLFreeEnv**|**SQLFreeHandle**|  
|**SQLGetConnectOption**|**SQLGetConnectAttr**|  
|**SQLGetStmtOption**|**SQLGetStmtAttr**|  
|**SQLParamOptions**|**SQLSetStmtAttr**, **SQLGetStmtAttr**|  
|**SQLSetConnectOption**|**SQLSetConnectAttr**|  
|**SQLSetParam**|**SQLBindParameter**|  
|**SQLSetStmtOption**|**SQLSetStmtAttr**|  
|**SQLTransact**|**SQLEndTran**|  
  
 [1] la funzione **SQLExtendedFetch** è una funzionalità duplicata; **SQLFetchScroll** fornisce le stesse funzionalità di ODBC *3. x*. Tuttavia, la gestione driver non esegue il mapping di **SQLExtendedFetch** a **SQLFetchScroll** quando si esegue un driver ODBC *3. x* . Per ulteriori informazioni, vedere la pagina relativa alle linee guida per la compatibilità con le versioni precedenti di [Driver Manager](../../../odbc/reference/appendixes/what-the-driver-manager-does.md) . Gestione driver esegue il mapping di **SQLFetchScroll** a **SQLExtendedFetch** quando viene eseguito un driver ODBC *2. x* .  
  
> [!NOTE]
>  La funzione **SQLBindParam** è un caso speciale. **SQLBindParam** è una funzionalità duplicata. Non si tratta di una funzione ODBC *2. x* , ma di una funzione presente negli standard Open Group e ISO. La funzionalità fornita da questa funzione è completamente inglobata da quella di **SQLBindParameter**. Di conseguenza, gestione driver esegue il mapping di una chiamata a **SQLBindParam** a **SQLBindParameter** quando il driver sottostante è un driver ODBC *3. x* . Tuttavia, quando il driver sottostante è un driver ODBC *2. x* , gestione driver non esegue questo mapping.
