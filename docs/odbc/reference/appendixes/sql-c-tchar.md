---
title: SQL_C_TCHAR | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- sql_c_tchar [ODBC]
- pseudo-type identifiers [ODBC], SQL_C_TCHAR
- data types [ODBC], pseudo-type identifiers
ms.assetid: 9e27c8bd-ee15-4ce9-b70a-34cf1bf16f4c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 68a03de54a8a5f63a994578d64c6bce5a1279138
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057041"
---
# <a name="sqlctchar"></a>SQL_C_TCHAR
L'identificatore del tipo SQL_C_TCHAR non identificare effettivamente un tipo di dati. è una macro che esiste all'interno del file di intestazione per la conversione Unicode. A seconda dell'impostazione di UNICODE viene sostituito con SQL_C_CHAR o SQL_C_WCHAR **#define**. È utile per un'applicazione di trasferimento dei dati di tipo carattere che viene compilati come un'applicazione Unicode e ANSI.
