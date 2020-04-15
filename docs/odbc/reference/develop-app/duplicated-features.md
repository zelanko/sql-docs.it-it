---
title: Caratteristiche duplicate Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300481"
---
# <a name="duplicated-features"></a>Funzionalità duplicate
Le seguenti funzioni ODBC *2.x* sono state duplicate dalle funzioni ODBC *3.x.* Di conseguenza, le funzioni ODBC *2.x* sono deprecate in ODBC *3.x*. Le funzioni ODBC *3.x* vengono definite funzioni di sostituzione.  
  
 Quando un'applicazione utilizza una funzione ODBC *2.x* deprecata e il driver sottostante è un driver ODBC *3.x,* Gestione Driver esegue il mapping della chiamata di funzione alla funzione di sostituzione corrispondente. L'unica eccezione a questa regola è **SQLExtendedFetch**. (Vedere la nota a piè di pagina alla fine della tabella seguente.) Per altre informazioni su questi mapping, vedere [Mapping di funzioni deprecate](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) nell'Appendice G: Linee guida per i driver per la compatibilità con le versioni precedenti.  
  
 Quando un'applicazione utilizza una funzione di sostituzione e il driver sottostante è un driver ODBC *2.x,* Gestione Driver esegue il mapping della chiamata di funzione alla funzione deprecata corrispondente.  
  
|ODBC *2.x (funzione)*|ODBC *3.x (funzione)*|  
|-------------------------|-------------------------|  
|**SQLAllocConnect (connessione a questo errore)**|**SQLAllocHandle**|  
|**SQLAllocEnv (informazioni in lingua inglese)**|**SQLAllocHandle**|  
|**Istruzione SQLAllocStmt (informazioni in lingua inglese)**|**SQLAllocHandle**|  
|**ATTRIBUTI SQLCol**|**SQLColAttribute**|  
|**Sqlerror**|**SQLGetDiagRec**|  
|**SQLExtendedFetch**[1]|**SQLFetchScroll**|  
|**SQLFreeConnect (informazioni in lingua inglese)**|**SQLFreeHandle**|  
|**SQLFreeEnv (informazioni in lingua inglese)**|**SQLFreeHandle**|  
|**SQLGetConnectOption (Opzione SQLGetConnectOption)**|**SQLGetConnectAttr**|  
|**Opzione SQLGetStmtOption**|**SQLGetStmtAttr**|  
|**Opzioni SQLParam**|**SQLSetStmtAttr**, **SQLGetStmtAttr**|  
|**Sqlsetconnectoption**|**SQLSetConnectAttr**|  
|**SQLSetParam (informazioni in lingua inglese)**|**SQLBindParameter**|  
|**Opzione SQLSetStmmtOption**|**SQLSetStmtAttr**|  
|**SQLTransact (transazione SQLTransact)**|**SQLEndTran**|  
  
 [1] La funzione **SQLExtendedFetch** è una funzionalità duplicata; **SQLFetchScroll** fornisce la stessa funzionalità in ODBC *3.x*. Tuttavia, Gestione Driver non esegue il mapping di **SQLExtendedFetch** a **SQLFetchScroll** quando si va contro un driver ODBC *3.x.* Per ulteriori informazioni, vedere [Cosa fa Gestione Driver nell'Appendice](../../../odbc/reference/appendixes/what-the-driver-manager-does.md) G: Linee guida del driver per la compatibilità con le versioni precedenti. Gestione Driver esegue il mapping **di SQLFetchScroll** a **SQLExtendedFetch** quando si va contro un driver ODBC *2.x.*  
  
> [!NOTE]
>  La funzione **SQLBindParam** è un caso speciale. **SQLBindParam** è una funzionalità duplicata. Non si tratta di una funzione ODBC *2.x,* ma di una funzione presente negli standard Open Group e ISO. La funzionalità fornita da questa funzione è completamente sommessa da quella di **SQLBindParameter**. Di conseguenza, Gestione Driver esegue il mapping di una chiamata a **SQLBindParam** a **SQLBindParameter** quando il driver sottostante è un driver ODBC *3.x.* Tuttavia, quando il driver sottostante è un driver ODBC *2.x,* Gestione Driver non esegue questo mapping.
