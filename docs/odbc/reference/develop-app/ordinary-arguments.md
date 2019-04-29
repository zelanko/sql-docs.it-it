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
manager: craigg
ms.openlocfilehash: 31d83b00fd70cd54587a19ebfea7310154167493
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62999279"
---
# <a name="ordinary-arguments"></a>Argomenti ordinari
Quando un argomento di stringa di funzione di catalogo è un normale argomento, si viene considerato come una stringa letterale. Un normale argomento accetta un criterio di ricerca stringa né un elenco di valori. Nel caso di un normale argomento è significativo e le virgolette nella stringa vengono considerate in modo letterale. Questi argomenti vengono trattati come argomenti ordinari se l'attributo di istruzione SQL_ATTR_METADATA_ID è impostato su SQL_FALSE; vengono considerate come argomenti di tipo identificatore invece se questo attributo è impostato su SQL_TRUE.  
  
 Se un argomento ordinario è impostato su un puntatore null e l'argomento è un argomento obbligatorio, la funzione restituisce SQL_ERROR e SQLSTATE HY009 (utilizzo non valido del puntatore null). Se un argomento ordinario è impostato su un puntatore null e l'argomento non è un argomento obbligatorio, il comportamento dell'argomento dipende dal driver. Nella tabella seguente sono elencati gli argomenti obbligatori.  
  
|Funzione|Argomenti obbligatori|  
|--------------|------------------------|  
|**SQLColumnPrivileges**|*TableName*|  
|**SQLForeignKeys**|*PKTableName*, *FKTableName*|  
|**SQLPrimaryKeys**|*TableName*|  
|**SQLSpecialColumns**|*TableName*|  
|**SQLStatistics**|*TableName*|
