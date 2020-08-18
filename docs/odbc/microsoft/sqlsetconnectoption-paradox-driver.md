---
description: SQLSetConnectOption (driver Paradox)
title: SQLSetConnectOption (driver Paradox) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 650c23ac038c3dd937bd25731499fa75127e696c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88411637"
---
# <a name="sqlsetconnectoption-paradox-driver"></a>SQLSetConnectOption (driver Paradox)
> [!NOTE]  
>  In questo argomento vengono fornite informazioni specifiche del driver Paradox. Per informazioni generali su questa funzione, vedere l'argomento appropriato in informazioni di [riferimento sulle API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|fOption|Commento|  
|-------------|-------------|  
|SQL_ACCESS_MODE|Il SQL_ACCESS_MODE fOption può essere impostato su SQL_MODE_READ_ONLY o SQL_MODE_READ_WRITE. Tuttavia, il driver non impedisce gli aggiornamenti se SQL_ACCESS_MODE è impostato su SQL_MODE_READ_ONLY.|  
|SQL_AUTOCOMMIT|Il driver Paradox supporta solo SQL_AUTOCOMMIT sia impostato su ON (stato predefinito), perché non supportano le transazioni.|  
|SQL_CURRENT_QUALIFIER|Supportata.|  
|SQL_LOGIN_TIMEOUT|Non supportato.|  
|SQL_OPT_TRACE|Supportata.|  
|SQL_OPT_TRACEFILE|Supportata.|  
|SQL_PACKET_SIZE|Non supportato.|  
|SQL_QUIET_MODE|Non supportato.|  
|SQL_TRANSLATE_DLL|Non supportato.|  
|SQL_TRANSLATION_OPTION|Non supportato.|  
|SQL_TXN_ISOLATION|Non supportato.|
