---
title: Supporto dei tipi di dati | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- minimum SQL syntax supported [ODBC]
- ODBC drivers [ODBC], minimum SQL syntax supported
- data types [ODBC], ODBC drivers
- ODBC drivers [ODBC], data types
ms.assetid: 782b4490-372b-4366-aad7-a486fb8a07c8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c9a3d63f0bf1923905c5281655aff2af294b8284
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63241329"
---
# <a name="data-type-support"></a>Supporto dei tipi di dati
Driver ODBC devono supportare almeno uno dei SQL_CHAR e SQL_VARCHAR. Supporto per altri tipi di dati è determinato dal livello di conformità SQL-92 dell'origine dati o del driver. Un'applicazione deve chiamare **SQLGetTypeInfo** per determinare i tipi di dati supportati dal driver.  
  
 Per altre informazioni sui tipi di dati, vedere [appendice d: Tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md).
