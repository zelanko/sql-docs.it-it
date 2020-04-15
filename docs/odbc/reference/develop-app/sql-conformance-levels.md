---
title: Livelli di conformità di SQL Documenti Microsoft
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
ms.openlocfilehash: 875330ac78588566b4b1c212f7a65d2841127a61
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301382"
---
# <a name="sql-conformance-levels"></a>Livelli di conformità SQL
Il livello di grammatica SQL-92 supportato da un driver è indicato dal valore restituito da una chiamata a **SQLGetInfo** con il tipo di informazioni SQL_SQL_CONFORMANCE. Indica se il driver è conforme ai livelli Entry, FIPS Transitional, Intermediate o Full definiti in SQL-92.  
  
 Tutti i driver ODBC devono supportare la grammatica SQL minima descritta in [Grammatica minima SQL](../../../odbc/reference/appendixes/sql-minimum-grammar.md) nell'Appendice C: Grammatica SQL. Questa grammatica è un sottoinsieme del livello di ingresso di SQL-92. I driver possono supportare SQL aggiuntivo ed essere conformi al livello di transizione SQL-92 Entry, Intermediate o Full o al livello di transizione FIPS 127-2. I driver che rispettano un determinato livello di SQL-92 o FIPS 127-2 possono supportare funzionalità aggiuntive in uno qualsiasi dei livelli superiori, ma non sono completamente conformi a tale livello. Per determinare se una funzionalità è supportata, un'applicazione deve chiamare **SQLGetInfo** con il tipo di informazioni appropriato. Il livello di conformità di una funzionalità SQL è descritto nel tipo di informazioni corrispondente. Vedere la descrizione della funzione [SQLGetInfo.](../../../odbc/reference/syntax/sqlgetinfo-function.md)
