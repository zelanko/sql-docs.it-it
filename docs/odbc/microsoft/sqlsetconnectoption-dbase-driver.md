---
title: SQLSetConnectOption (Driver dBASE) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBase driver [ODBC], SQLSetConnectOption
- SQLSetConnectOption function [ODBC], dBASE Driver
ms.assetid: b1924c33-6820-4566-b716-6897807edd0f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d9f2fc32287df9da61d8eabc1b22445d19a0f027
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68090863"
---
# <a name="sqlsetconnectoption-dbase-driver"></a>SQLSetConnectOption (driver dBASE)
> [!NOTE]  
>  In questo argomento fornisce informazioni specifiche del Driver dBASE. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|fOption|Commento|  
|-------------|-------------|  
|SQL_ACCESS_MODE|Il fOption SQL_ACCESS_MODE può essere impostato su SQL_MODE_READ_ONLY o SQL_MODE_READ_WRITE. Tuttavia, il driver non impedisce gli aggiornamenti se SQL_ACCESS_MODE è impostato su SQL_MODE_READ_ONLY.|  
|SQL_AUTOCOMMIT|Il driver dBASE supporta solo SQL_AUTOCOMMIT che viene impostato su (stato predefinito), perché non supporta le transazioni.|  
|SQL_CURRENT_QUALIFIER|Supportato.|  
|SQL_LOGIN_TIMEOUT|Non supportati.|  
|SQL_OPT_TRACE|Supportato.|  
|SQL_OPT_TRACEFILE|Supportato.|  
|SQL_PACKET_SIZE|Non supportati.|  
|SQL_QUIET_MODE|Non supportati.|  
|SQL_TRANSLATE_DLL|Non supportati.|  
|SQL_TRANSLATION_OPTION|Non supportati.|  
|SQL_TXN_ISOLATION|Non supportati.|
