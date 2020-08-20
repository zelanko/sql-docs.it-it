---
description: Livelli di conformità SQL
title: Livelli di conformità SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- conformance levels [ODBC], SQL
- SQL conformance levels [ODBC]
- data sources [ODBC], conformance levels
- ODBC drivers [ODBC], conformance levels
ms.assetid: 3529df2c-a09b-4c16-9c60-eae7a06d903a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 525cda9094213e6decf30643c23a7db623511e14
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499804"
---
# <a name="sql-conformance-levels"></a>Livelli di conformità SQL
Il livello della grammatica SQL-92 supportato da un driver è indicato dal valore restituito da una chiamata a **SQLGetInfo** con il tipo di informazioni SQL_SQL_CONFORMANCE. Indica se il driver è conforme alla voce, a livello di transizione FIPS, intermedio o completo definito in SQL-92.  
  
 Tutti i driver ODBC devono supportare la grammatica SQL minima descritta in [grammatica minima SQL](../../../odbc/reference/appendixes/sql-minimum-grammar.md) nell'Appendice C: grammatica SQL. Questa grammatica è un subset del livello di ingresso di SQL-92. I driver possono supportare SQL aggiuntivo e essere conformi alla voce SQL-92, intermedia o completa o al livello di transizione FIPS 127-2. I driver conformi a un determinato livello di SQL-92 o FIPS 127-2 possono supportare funzionalità aggiuntive in qualsiasi livello superiore, ma non sono completamente conformi a tale livello. Per determinare se una funzionalità è supportata, un'applicazione deve chiamare **SQLGetInfo** con il tipo di informazioni appropriato. Il livello di conformità di una funzionalità SQL è descritto nel tipo di informazioni corrispondente. (Vedere la descrizione della funzione [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) ).
