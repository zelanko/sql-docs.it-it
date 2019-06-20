---
title: Catalogo e utilizzo dello Schema | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], catalog names
- catalog names [ODBC]
- interoperability of SQL statements [ODBC], schema names
- schema names in SQL statements [ODBC]
ms.assetid: 84f7ef61-1ef1-46f3-9678-b087aa8e8e34
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9476f4f928890514354f97ce604f871bd8a06d11
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63007889"
---
# <a name="catalog-and-schema-usage"></a>Utilizzo del catalogo e dello schema
Origini dati non supportano necessariamente i nomi di catalogo e lo schema come identificatori di nome di oggetto in tutte le istruzioni SQL. Origini dati potrebbero supportare nomi di catalogo e lo schema in uno o più delle seguenti classi di istruzioni SQL: Istruzioni Data Manipulation Language (DML), le chiamate di procedure, istruzioni di definizione di tabella, istruzioni per la definizione dell'indice e le istruzioni di definizione dei privilegi. Per determinare le classi di istruzioni SQL in quale catalogo e lo schema è possibile usare i nomi, un'applicazione chiama **SQLGetInfo** con le opzioni SQL_CATALOG_USAGE e SQL_SCHEMA_USAGE.
