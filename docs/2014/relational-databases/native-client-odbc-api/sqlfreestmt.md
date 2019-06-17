---
title: SQLFreeStmt | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLFreeStmt function
ms.assetid: d9666d0b-3446-480e-bf1a-10b01213e411
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4aa7e597bcfa80d7d45064c844986018d64617d5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63190313"
---
# <a name="sqlfreestmt"></a>SQLFreeStmt
  **SQLFreeStmt** non è consigliabile in ODBC 3.0 e versioni successive. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC supportate tutte definite *opzione* i valori per **SQLFreeStmt**. Tuttavia [SQLCloseCursor](sqlclosecursor.md), [SQLBindParameter](sqlbindparameter.md), [SQLBindCol](sqlbindcol.md), **SQLSetDescField**, e [SQLFreeHandle ](sqlfreehandle.md) sostituiscono o duplicano la funzione del **SQLFreeStmt** e deve essere usato invece.  
  
## <a name="see-also"></a>Vedere anche  
 [SQLFreeStmt-funzione](https://go.microsoft.com/fwlink/?LinkId=59346)   
 [Dettagli di implementazione dell'API ODBC](odbc-api-implementation-details.md)  
  
  
