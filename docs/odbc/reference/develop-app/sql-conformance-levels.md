---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c2e8ce5aeeb94a4f7a33b22054adc8067e0654ac
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62690202"
---
# <a name="sql-conformance-levels"></a>Livelli di conformità SQL
Il livello di grammatica SQL-92 supportata da un driver è indicato dal valore restituito da una chiamata a **SQLGetInfo** con il tipo di informazioni SQL_SQL_CONFORMANCE. Indica se il driver è conforme ai livelli di voce, FIPS transitorio, intermedio o Full definiti in SQL-92.  
  
 Tutti i driver ODBC devono supportare la grammatica SQL minima descritto nella [grammatica SQL](../../../odbc/reference/appendixes/sql-minimum-grammar.md) nell'appendice c: Grammatica SQL. L'espressione è un subset del livello minimo di SQL-92. Driver potrebbe supportare SQL aggiuntive e sia conforme al livello intermedio, voce SQL-92 o Full o per lo standard FIPS 127-2 transitorio livello. Driver conformi a un determinato livello di SQL-92 o FIPS 127-2 può supportare funzionalità aggiuntive in uno dei livelli più elevati ancora non essere completamente conforme a tale livello. Per determinare se una funzionalità è supportata, un'applicazione deve chiamare **SQLGetInfo** con il tipo di informazioni appropriate. Viene descritto il livello di conformità di una funzionalità SQL nel tipo di informazioni corrispondenti. (Vedere la [SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md) descrizione della funzione.)
