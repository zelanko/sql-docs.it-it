---
title: Utilizzo del catalogo e dello schema | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68064408"
---
# <a name="catalog-and-schema-usage"></a>Utilizzo del catalogo e dello schema
Le origini dati non supportano necessariamente i nomi di catalogo e di schema come identificatori del nome di oggetto in tutte le istruzioni SQL. È possibile che le origini dati supportino i nomi di catalogo e di schema in una o più delle seguenti classi di istruzioni SQL: istruzioni DML (Data Manipulation Language), chiamate di procedure, istruzioni di definizione della tabella, istruzioni per la definizione dell'indice e definizione dei privilegi istruzioni. Per determinare le classi di istruzioni SQL in cui è possibile utilizzare i nomi di catalogo e di schema, un'applicazione chiama **SQLGetInfo** con le opzioni SQL_CATALOG_USAGE e SQL_SCHEMA_USAGE.
