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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "63190313"
---
# <a name="sqlfreestmt"></a>SQLFreeStmt
  **SQLFreeStmt** non è consigliato in ODBC 3,0 e versioni successive. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native Client supporta tutti i valori di *opzione* definiti per **SQLFreeStmt**. Tuttavia, [SQLCloseCursor](sqlclosecursor.md), [SQLBindParameter](sqlbindparameter.md), [SQLBindCol](sqlbindcol.md), **SQLSetDescField**e [SQLFreeHandle](sqlfreehandle.md) sostituiscono o duplicano la funzione di **SQLFreeStmt** e devono essere usati in alternativa.  
  
## <a name="see-also"></a>Vedere anche  
 [SQLFreeStmt (funzione)](https://go.microsoft.com/fwlink/?LinkId=59346)   
 [ODBC API Implementation Details](odbc-api-implementation-details.md)  
  
  
