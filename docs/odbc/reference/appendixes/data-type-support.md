---
description: Supporto dei tipi di dati
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9ab0fd163713a7f6657d8ce446336f5c35a3dd00
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88456638"
---
# <a name="data-type-support"></a>Supporto dei tipi di dati
I driver ODBC devono supportare almeno uno dei SQL_CHAR e SQL_VARCHAR. Il supporto per altri tipi di dati è determinato dal livello di conformità SQL-92 del driver o dell'origine dati. Un'applicazione deve chiamare **SQLGetTypeInfo** per determinare i tipi di dati supportati dal driver.  
  
 Per ulteriori informazioni sui tipi di dati, vedere [Appendice D: tipi di dati](../../../odbc/reference/appendixes/appendix-d-data-types.md).
