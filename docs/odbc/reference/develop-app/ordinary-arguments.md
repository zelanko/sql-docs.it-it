---
title: Argomenti ordinari | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arguments in catalog functions [ODBC], ordinary
- catalog functions [ODBC], arguments
- ordinary arguments [ODBC]
ms.assetid: a18cdae1-6b85-41cb-875c-b5a01ec90aeb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 997604b4376656d36d2bc4bc31f1959aa6c8a229
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67987825"
---
# <a name="ordinary-arguments"></a>Argomenti ordinari
Quando un argomento di stringa della funzione di catalogo è un argomento ordinario, viene considerato come una stringa letterale. Un argomento ordinario non accetta né un criterio di ricerca di stringa né un elenco di valori. Il caso di un argomento ordinario è significativo e i caratteri di virgolette nella stringa vengono presi letteralmente. Questi argomenti vengono trattati come argomenti ordinari se l'attributo dell'istruzione SQL_ATTR_METADATA_ID è impostato su SQL_FALSE; vengono considerati invece come argomenti identificatore se questo attributo è impostato su SQL_TRUE.  
  
 Se un argomento ordinario è impostato su un puntatore null e l'argomento è un argomento obbligatorio, la funzione restituisce SQL_ERROR e SQLSTATE HY009 (utilizzo non valido del puntatore null). Se un argomento ordinario è impostato su un puntatore null e l'argomento non è un argomento obbligatorio, il comportamento dell'argomento è dipendente dal driver. Gli argomenti obbligatori sono elencati nella tabella seguente.  
  
|Funzione|Argomenti obbligatori|  
|--------------|------------------------|  
|**SQLColumnPrivileges**|*TableName*|  
|**SQLForeignKeys**|*PKTableName*, *FKTableName*|  
|**SQLPrimaryKeys**|*TableName*|  
|**SQLSpecialColumns**|*TableName*|  
|**SQLStatistics**|*TableName*|
