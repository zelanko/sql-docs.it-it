---
title: Sequenza di Escape LIKE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC escape sequences [ODBC], LIKE
- LIKE escape sequence [ODBC]
- escape sequences [ODBC], LIKE
ms.assetid: 798d75ea-be9d-4bef-b297-318bc327f1ca
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 65447904f32b7e0457ed807f18e942b334ddc236
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188796"
---
# <a name="like-escape-sequence"></a>Sequenza di escape LIKE
ODBC Usa sequenze di escape per la clausola LIKE. La sintassi di questa sequenza di escape è come segue:  
  
```  
{'escape-character'}  
```  
  
## <a name="remarks"></a>Note  
 Nella notazione BNF, la sintassi è come segue:  
  
 *ODBC-like-escape* ::=  
  
 *ODBC-esc-iniziatore* escape '*carattere di escape*' *ODBC-esc-carattere di terminazione*  
  
 *carattere di escape* :: = *carattere*  
  
 *ODBC-esc-iniziatore* :: = {  
  
 *ODBC-esc-carattere di terminazione* :: =}  
  
 Per determinare se il driver supporta il carattere di escape LIKE sequenza, un'applicazione può chiamare **SQLGetInfo** con il tipo di informazioni SQL_LIKE_ESCAPE_CLAUSE.
