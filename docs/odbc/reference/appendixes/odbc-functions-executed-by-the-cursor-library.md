---
title: Funzioni ODBC eseguite dalla libreria di cursori Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursor library [ODBC], functions
- functions [ODBC], cursor library
- ODBC functions [ODBC], cursor library
- ODBC cursor library [ODBC], functions
ms.assetid: 2f1d3386-7e59-4d55-a5b4-3440b61343a3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 70fb48a8764a913ea4c2376c1a44bcd8712e7d29
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298231"
---
# <a name="odbc-functions-executed-by-the-cursor-library"></a>Funzioni ODBC eseguite dalla libreria di cursori
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità del cursore del driver.  
  
 La libreria di cursori esegue le seguenti funzioni. Quando un'applicazione chiama una funzione in questo elenco, Gestione Driver richiama la libreria di cursori, non il driver. Si noti che la libreria di cursori può chiamare il driver durante l'esecuzione della funzione.  
  
|||  
|-|-|  
|**SQLBindCol**|**Opzione SQLGetStmtOption**|  
|**SQLBindParam (informazioni in lingua inglese)**|**SQLNativeSql**|  
|**SQLBindParameter**|**SQLNumParams**|  
|**SQLCloseCursor**|**Opzioni SQLParam**|  
|**SQLEndTran**|**SQLRowCount**|  
|**Sqlextendedfetch**|**SQLSetConnectAttr**|  
|**SQLFetchScroll**|**Sqlsetconnectoption**|  
|**SQLFreeHandle**|**SQLSetDescField**|  
|**SQLFreeStmt**|**SQLSetDescRec**|  
|**SQLGetData**|**SQLSetPos**|  
|**SQLGetDescField**|**Opzioni SQLSetScrollOptions**|  
|**SQLGetDescRec**|**SQLSetStmtAttr**|  
|**SQLGetFunctions**|**Opzione SQLSetStmmtOption**|  
|**SQLGetInfo**|**SQLTransact (transazione SQLTransact)**|  
|**SQLGetStmtAttr**||
