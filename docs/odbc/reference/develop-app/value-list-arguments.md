---
title: Valore elenco argomenti | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a971da68a8f2a35df8fa513e68d1eba127e9c430
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63208557"
---
# <a name="value-list-arguments"></a>Argomenti dell'elenco di valori
Un argomento di valore di elenco è costituito da un elenco con valori delimitati da virgole da utilizzare per la corrispondenza. Argomento specificato non è un solo valore elenco nelle funzioni di catalogo ODBC: il *TableType* nell'argomento **SQLTables**. L'impostazione *TableType* a un puntatore null è lo stesso come se è impostato su SQL_ALL_TABLE_TYPES, che enumera tutti i possibili membri dell'elenco dei valori. Questo argomento non è influenzato l'attributo di istruzione SQL_ATTR_METADATA_ID. Per altre informazioni, vedere la [SQLTables](../../../odbc/reference/syntax/sqltables-function.md) descrizione della funzione.
