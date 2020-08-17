---
description: Tipi di dati supportati
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 349636553112449485d99fed269a43069974fccf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88385827"
---
# <a name="supported-data-types"></a>Tipi di dati supportati
I tipi di dati supportati dai DBMS variano notevolmente. Un'applicazione può determinare i nomi e le caratteristiche dei tipi di dati supportati chiamando **SQLGetTypeInfo**. A causa della variazione ampia nei nomi dei tipi di dati, l'applicazione deve utilizzare i nomi dei tipi di dati restituiti da **SQLGetTypeInfo** nelle istruzioni **Create Table** . Per ulteriori informazioni, vedere [tipi di dati in ODBC](../../../odbc/reference/develop-app/data-types-in-odbc.md).
