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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 245bd007f070a94689283830ba7a1362e31353e6
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306252"
---
# <a name="catalog-and-schema-usage"></a>Utilizzo del catalogo e dello schema
Le origini dati non supportano necessariamente i nomi di catalogo e di schema come identificatori del nome di oggetto in tutte le istruzioni SQL. È possibile che le origini dati supportino i nomi di catalogo e di schema in una o più delle seguenti classi di istruzioni SQL: istruzioni DML (Data Manipulation Language), chiamate di procedure, istruzioni di definizione della tabella, istruzioni per la definizione dell'indice e istruzioni di definizione dei privilegi. Per determinare le classi di istruzioni SQL in cui è possibile utilizzare i nomi di catalogo e di schema, un'applicazione chiama **SQLGetInfo** con le opzioni SQL_CATALOG_USAGE e SQL_SCHEMA_USAGE.
