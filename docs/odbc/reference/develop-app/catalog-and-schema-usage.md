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
ms.openlocfilehash: 4e10460df120451502d798376453d69d111051ec
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064408"
---
# <a name="catalog-and-schema-usage"></a>Utilizzo del catalogo e dello schema
Origini dati non supportano necessariamente i nomi di catalogo e lo schema come identificatori di nome di oggetto in tutte le istruzioni SQL. Origini dati potrebbero supportare nomi di catalogo e lo schema in uno o più delle seguenti classi di istruzioni SQL: Istruzioni Data Manipulation Language (DML), le chiamate di procedure, istruzioni di definizione di tabella, istruzioni per la definizione dell'indice e le istruzioni di definizione dei privilegi. Per determinare le classi di istruzioni SQL in quale catalogo e lo schema è possibile usare i nomi, un'applicazione chiama **SQLGetInfo** con le opzioni SQL_CATALOG_USAGE e SQL_SCHEMA_USAGE.
