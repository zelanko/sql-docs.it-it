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
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9b7fbc3754121418ea2059ea511f3b247dcff8dd
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706096"
---
# <a name="sqlfreestmt"></a>SQLFreeStmt
  **SQLFreeStmt** non è consigliato in ODBC 3,0 e versioni successive. Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC di Native Client supporta tutti i valori di *opzione* definiti per **SQLFreeStmt**. Tuttavia, [SQLCloseCursor](sqlclosecursor.md), [SQLBindParameter](sqlbindparameter.md), [SQLBindCol](sqlbindcol.md), **SQLSetDescField**e [SQLFreeHandle](sqlfreehandle.md) sostituiscono o duplicano la funzione di **SQLFreeStmt** e devono essere usati in alternativa.  
  
## <a name="see-also"></a>Vedere anche  
 [SQLFreeStmt (funzione)](https://go.microsoft.com/fwlink/?LinkId=59346)   
 [Dettagli di implementazione dell'API ODBC](odbc-api-implementation-details.md)  
  
  
