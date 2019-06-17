---
title: Tipi di dati supportati | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2a8848bad9d27dfd9318b725b77203706d3dfd5a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149087"
---
# <a name="supported-data-types"></a>Tipi di dati supportati
Tipi di dati supportati dai sistemi DBMS variano notevolmente. Un'applicazione può determinare i nomi e caratteristiche dei tipi di dati supportati chiamando **SQLGetTypeInfo**. A causa di ampia variazione nei nomi dei tipi di dati, l'applicazione deve utilizzare i nomi dei tipi di dati restituiti da **SQLGetTypeInfo** nelle **CREATE TABLE** istruzioni. Per altre informazioni, vedere [tipi di dati in ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md).
