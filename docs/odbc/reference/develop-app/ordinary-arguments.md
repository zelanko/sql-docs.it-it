---
title: Argomenti Ordinari Documenti Microsoft
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
ms.openlocfilehash: 97362f93e91ccd8b592b4c05a0714b7602c1ba94
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282466"
---
# <a name="ordinary-arguments"></a>Argomenti ordinari
Quando un argomento stringa funzione catalogo è un argomento ordinario, viene considerato come una stringa letterale. Un argomento ordinario non accetta né un criterio di ricerca di stringhe né un elenco di valori. Il caso di un argomento ordinario è significativo e le virgolette nella stringa vengono prese letteralmente. Questi argomenti vengono considerati come argomenti ordinari se l'attributo dell'istruzione SQL_ATTR_METADATA_ID è impostato su SQL_FALSE; vengono invece considerati come argomenti di tipo identificatore se questo attributo è impostato su SQL_TRUE.  
  
 Se un argomento ordinario è impostato su un puntatore null e l'argomento è obbligatorio, la funzione restituisce SQL_ERROR e SQLSTATE HY009 (utilizzo non valido del puntatore null). Se un argomento ordinario è impostato su un puntatore null e l'argomento non è un argomento obbligatorio, il comportamento dell'argomento dipende dal driver. Gli argomenti obbligatori sono elencati nella tabella seguente.  
  
|Funzione|Argomenti obbligatori|  
|--------------|------------------------|  
|**SQLColumnPrivileges**|*Tablename*|  
|**SQLForeignKeys**|*PKTableName*, *FKTableName*|  
|**SQLPrimaryKeys**|*Tablename*|  
|**SQLSpecialColumns**|*Tablename*|  
|**SQLStatistics**|*Tablename*|
