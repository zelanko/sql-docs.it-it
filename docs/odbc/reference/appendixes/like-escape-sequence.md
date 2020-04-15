---
title: Sequenza di fuga LIKE Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 517c21f7b64fa7ceb662af9839a9fed1a1e6eff6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304922"
---
# <a name="like-escape-sequence"></a>Sequenza di escape LIKE
ODBC utilizza sequenze di escape per la clausola LIKE. La sintassi di questa sequenza di escape è la seguente:The syntax of this escape sequence is as follows:  
  
```  
{'escape-character'}  
```  
  
## <a name="remarks"></a>Osservazioni  
 Nella notazione BNF, la sintassi è la seguente:  
  
 *Odbc-like-escape* ::  
  
 *ODBC-esc-initiator* escape '*escape-character*' *ODBC-esc-terminator*  
  
 *carattere di escape* :: *: carattere*  
  
 *ODBC-esc-initiator* ::  
  
 *Carattere di terminazione ODBC-esc::: *  
  
 Per determinare se il driver supporta la sequenza di escape LIKE, un'applicazione può chiamare **SQLGetInfo** con il tipo di informazioni SQL_LIKE_ESCAPE_CLAUSE.
