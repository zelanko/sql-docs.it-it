---
description: Argomenti ordinari
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b6e4e7a30efe5735aa87665d7d0247bef06390ce
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429173"
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
