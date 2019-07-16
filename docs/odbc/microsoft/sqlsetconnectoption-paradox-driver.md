---
title: SQLSetConnectOption (Driver Paradox) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], Paradox Driver
- Paradox driver [ODBC], SQLSetConnectOption
ms.assetid: 050ee2be-594e-4dbd-af67-8b6aae756cd1
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0cf6d01650b86fca4c782521fe3c368f729e6b42
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67897767"
---
# <a name="sqlsetconnectoption-paradox-driver"></a>SQLSetConnectOption (driver Paradox)
> [!NOTE]  
>  In questo argomento fornisce informazioni specifiche del Driver Paradox. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|fOption|Commento|  
|-------------|-------------|  
|SQL_ACCESS_MODE|Il fOption SQL_ACCESS_MODE può essere impostato su SQL_MODE_READ_ONLY o SQL_MODE_READ_WRITE. Tuttavia, il driver non impedisce gli aggiornamenti se SQL_ACCESS_MODE è impostato su SQL_MODE_READ_ONLY.|  
|SQL_AUTOCOMMIT|Il driver Paradox supporta solo SQL_AUTOCOMMIT che viene impostato su (stato predefinito), perché non supportano transazioni.|  
|SQL_CURRENT_QUALIFIER|Supportato.|  
|SQL_LOGIN_TIMEOUT|Non supportati.|  
|SQL_OPT_TRACE|Supportato.|  
|SQL_OPT_TRACEFILE|Supportato.|  
|SQL_PACKET_SIZE|Non supportati.|  
|SQL_QUIET_MODE|Non supportati.|  
|SQL_TRANSLATE_DLL|Non supportati.|  
|SQL_TRANSLATION_OPTION|Non supportati.|  
|SQL_TXN_ISOLATION|Non supportati.|
