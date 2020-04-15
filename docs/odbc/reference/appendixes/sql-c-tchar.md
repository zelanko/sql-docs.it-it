---
title: SQL_C_TCHAR . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 973d94b9b47371090a5f54fd3d259854ba78e9c2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304072"
---
# <a name="sql_c_tchar"></a>SQL_C_TCHAR
L'identificatore del tipo SQL_C_TCHAR non identifica effettivamente un tipo di dati. è una macro presente all'interno del file di intestazione per la conversione Unicode. Viene sostituito da SQL_C_CHAR o SQL_C_WCHAR a seconda dell'impostazione del **#define**UNICODE . È utile per un'applicazione che trasferisce dati di tipo carattere che viene compilato come un'applicazione ANSI e un'applicazione Unicode.It is useful for an application transferring character data that is compiled as both an ANSI and a Unicode application.
