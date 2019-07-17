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
ms.openlocfilehash: 646d2724489140080a673f31e22429cc7ca39d4e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022112"
---
# <a name="value-list-arguments"></a>Argomenti dell'elenco di valori
Un argomento di valore di elenco è costituito da un elenco con valori delimitati da virgole da utilizzare per la corrispondenza. Argomento specificato non è un solo valore elenco nelle funzioni di catalogo ODBC: il *TableType* nell'argomento **SQLTables**. L'impostazione *TableType* a un puntatore null è lo stesso come se è impostato su SQL_ALL_TABLE_TYPES, che enumera tutti i possibili membri dell'elenco dei valori. Questo argomento non è influenzato l'attributo di istruzione SQL_ATTR_METADATA_ID. Per altre informazioni, vedere la [SQLTables](../../../odbc/reference/syntax/sqltables-function.md) descrizione della funzione.
