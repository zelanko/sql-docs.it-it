---
title: 'Tipi di dati supportati : Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], DBMS support
- interoperability [ODBC], data types
ms.assetid: a89d4bab-ef3c-45c2-aa72-2639b3e0f856
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d19cde2d531819a60229dd7a780181571e169503
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307782"
---
# <a name="supported-data-types"></a>Tipi di dati supportati
I tipi di dati supportati dai DBSMO variano notevolmente. Un'applicazione può determinare i nomi e le caratteristiche dei tipi di dati supportati chiamando **SQLGetTypeInfo**. A causa di ampie variazioni nei nomi dei tipi di dati, l'applicazione deve utilizzare i nomi dei tipi di dati restituiti da **SQLGetTypeInfo** nelle istruzioni **CREATE TABLE.** Per ulteriori informazioni, vedere [Tipi di dati in ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md).
