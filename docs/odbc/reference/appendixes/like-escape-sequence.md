---
title: Sequenza di escape LIKE | Microsoft Docs
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
ms.openlocfilehash: 629ceaf666ae732d0838a216272c308dcb5b5658
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68041707"
---
# <a name="like-escape-sequence"></a>Sequenza di escape LIKE
ODBC utilizza sequenze di escape per la clausola LIKE. La sintassi di questa sequenza di escape è la seguente:  
  
```  
{'escape-character'}  
```  
  
## <a name="remarks"></a>Osservazioni  
 Nella notazione BNF la sintassi è la seguente:  
  
 *ODBC-like-Escape* :: =  
  
 *ODBC-ESC-initiator* escape '*Escape-Character*' *ODBC-ESC-Terminator*  
  
 carattere *di escape* :: = *carattere*  
  
 *ODBC-ESC-initiator* :: = {  
  
 *ODBC-ESC-Terminator* :: =}  
  
 Per determinare se il driver supporta la sequenza di escape LIKE, un'applicazione può chiamare **SQLGetInfo** con il tipo di informazioni SQL_LIKE_ESCAPE_CLAUSE.
