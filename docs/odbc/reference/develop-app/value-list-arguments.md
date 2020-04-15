---
title: Argomenti dell'elenco di valori Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], value list
- value list arguments [ODBC]
ms.assetid: 863837be-603b-4c7a-8b96-b71014037ee5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fd655bd745c3bb06923e047d4134b286cf64703e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306742"
---
# <a name="value-list-arguments"></a>Argomenti dell'elenco di valori
Un argomento di elenco di valori è costituito da un elenco di valori delimitati da virgole da utilizzare per la corrispondenza. È presente un solo argomento dell'elenco di valori nelle funzioni di catalogo ODBC: l'argomento *TableType* in **SQLTables**. L'impostazione di *TableType* su un puntatore null è la stessa come se fosse impostata su SQL_ALL_TABLE_TYPES, che enumera tutti i possibili membri dell'elenco di valori. Questo argomento non è interessato dall'attributo di istruzione SQL_ATTR_METADATA_ID. Per altre informazioni, vedere la descrizione della funzione [SQLTables.For](../../../odbc/reference/syntax/sqltables-function.md) more information, see the SQLTables function description.
