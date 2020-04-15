---
title: 'Utilizzo del catalogo e dello schema : Documenti Microsoft'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 245bd007f070a94689283830ba7a1362e31353e6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306252"
---
# <a name="catalog-and-schema-usage"></a>Utilizzo del catalogo e dello schema
Le origini dati non supportano necessariamente i nomi di catalogo e schema come identificatori di nomi di oggetto in tutte le istruzioni SQL. Le origini dati possono supportare i nomi di catalogo e schema in una o più delle seguenti classi di istruzioni SQL: istruzioni DML (Data Manipulation Language), chiamate di routine, istruzioni di definizione di tabella, istruzioni di definizione dell'indice e istruzioni di definizione dei privilegi. Per determinare le classi di istruzioni SQL in cui è possibile utilizzare i nomi di catalogo e schema, un'applicazione chiama **SQLGetInfo** con le opzioni SQL_CATALOG_USAGE e SQL_SCHEMA_USAGE.
