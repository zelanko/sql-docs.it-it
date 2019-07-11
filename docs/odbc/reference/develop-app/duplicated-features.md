---
title: Duplicate funzionalità | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d7b4e3991331e1a6f9dd731466cc2f514f75bbc9
ms.sourcegitcommit: 56b963446965f3a4bb0fa1446f49578dbff382e0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2019
ms.locfileid: "67793330"
---
# <a name="duplicated-features"></a>Funzionalità duplicate
ODBC seguenti *2.x* le funzioni hanno state duplicate da ODBC *3.x* funzioni. Di conseguenza, ODBC *2.x* le funzioni sono deprecate in ODBC *3.x*. ODBC *3.x* funzioni vengono dette funzioni di sostituzione.  
  
 Quando un'applicazione usa un ODBC deprecate *2.x* funzione e il driver sottostante è un database ODBC *3.x* driver, Driver Manager viene eseguito il mapping di chiamata di funzione alla funzione di sostituzione corrispondente. L'unica eccezione a questa regola viene **SQLExtendedFetch**. (Vedere la nota alla fine della tabella riportata di seguito). Per altre informazioni su tali mapping, vedere [Mapping di funzioni deprecate](../../../odbc/reference/appendixes/mapping-deprecated-functions.md) nell'appendice g: Driver linee guida per la compatibilità con le versioni precedenti.  
  
 Quando un'applicazione utilizza una funzione di sostituzione e il driver sottostante è un database ODBC *2.x* driver, Driver Manager viene eseguito il mapping la chiamata di funzione per la corrispondente funzione deprecata.  
  
|ODBC *2.x* (funzione)|ODBC *3.x* (funzione)|  
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
  
 [1] la funzione **SQLExtendedFetch** è una funzionalità duplicate; **SQLFetchScroll** offre le stesse funzionalità in ODBC *3.x*. Tuttavia, gestione Driver non esegue il mapping **SQLExtendedFetch** al **SQLFetchScroll** quando si passa da un database ODBC *3.x* driver. Per altre informazioni, vedere [the Driver Manager cosa](../../../odbc/reference/appendixes/what-the-driver-manager-does.md) nell'appendice g: Driver linee guida per la compatibilità con le versioni precedenti. Esegue il mapping di gestione Driver **SQLFetchScroll** al **SQLExtendedFetch** quando si passa da un database ODBC *2.x* driver.  
  
> [!NOTE]
>  La funzione **SQLBindParam** è un caso speciale. **SQLBindParam** è una funzionalità duplicate. Non si tratta di un database ODBC *2.x* funzione, ma una funzione che è presente negli standard Open Group e ISO. La funzionalità fornita da questa funzione è completamente sostituita da quello del **SQLBindParameter**. Di conseguenza, gestione Driver esegue il mapping di una chiamata a **SQLBindParam** al **SQLBindParameter** quando il driver sottostante è un database ODBC *3.x* driver. Tuttavia, quando il driver sottostante è un database ODBC *2.x* driver, gestione Driver non esegue il mapping.
