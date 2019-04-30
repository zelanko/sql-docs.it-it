---
title: Funzione SQLRemoveDefaultDataSource | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLRemoveDefaultDataSource
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLRemoveDefaultDataSource
helpviewer_keywords:
- SQLRemoveDefaultDataSource function [ODBC]
ms.assetid: db803266-57df-4864-a41b-901247549c1f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 90270f119b351592348287823c2b9d879a15154b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63262243"
---
# <a name="sqlremovedefaultdatasource-function"></a>Funzione SQLRemoveDefaultDataSource
**Conformità**  
 Versione introdotta: ODBC 1.0, deprecato  
  
 **Riepilogo**  
 In ODBC 3.0, il **SQLRemoveDefaultDataSource** funzione è stata sostituita da una chiamata a [SQLConfigDataSource](../../../odbc/reference/syntax/sqlconfigdatasource-function.md) con un *trattano* argomento di ODBC_REMOVE_DEFAULT_DSN. Se un ODBC 2 *. x* programma di installazione chiama questa funzione, il programma di installazione ODBC verrà mappato al seguente **SQLConfigDataSource** chiamare:  
  
```  
SQLConfigDataSource (NULL, ODBC_REMOVE_DEFAULT_DSN, NULL, NULL)  
```
