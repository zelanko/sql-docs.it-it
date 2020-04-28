---
title: Argomenti dell'elenco di valori | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306742"
---
# <a name="value-list-arguments"></a>Argomenti dell'elenco di valori
Un argomento dell'elenco di valori è costituito da un elenco di valori delimitati da virgole da utilizzare per la corrispondenza. Nelle funzioni del catalogo ODBC è presente un solo argomento di elenco dei valori: l'argomento *TableType* in **SQLTables**. L'impostazione di *TableType* su un puntatore null è uguale a quella di se è impostata su SQL_ALL_TABLE_TYPES, che enumera tutti i possibili membri dell'elenco di valori. Questo argomento non è influenzato dall'attributo dell'istruzione SQL_ATTR_METADATA_ID. Per ulteriori informazioni, vedere la descrizione della funzione [SQLTables](../../../odbc/reference/syntax/sqltables-function.md) .
