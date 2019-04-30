---
title: SQLSetConnectOption (Driver Excel) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], Excel Driver
- Excel driver [ODBC], SQLSetConnectOption
ms.assetid: 528d21d1-4516-4497-9da4-7b87d77e622a
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e04623c42df58f920620299d9dce7094039a406
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63306049"
---
# <a name="sqlsetconnectoption-excel-driver"></a>SQLSetConnectOption (driver Excel)
> [!NOTE]  
>  In questo argomento fornisce informazioni specifiche del Driver Excel. Per informazioni generali su questa funzione, vedere l'argomento appropriato nel [riferimento all'API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
|fOption|Commento|  
|-------------|-------------|  
|SQL_ACCESS_MODE|Il fOption SQL_ACCESS_MODE può essere impostato su SQL_MODE_READ_ONLY o SQL_MODE_READ_WRITE. Tuttavia, il driver non impedisce gli aggiornamenti se SQL_ACCESS_MODE è impostato su SQL_MODE_READ_ONLY.|  
|SQL_AUTOCOMMIT|Il driver di Microsoft Excel supporta solo SQL_AUTOCOMMIT che viene impostato su (stato predefinito), perché non supportano transazioni.|  
|SQL_CURRENT_QUALIFIER|Supportato.|  
|SQL_LOGIN_TIMEOUT|Non supportato.|  
|SQL_OPT_TRACE|Supportato.|  
|SQL_OPT_TRACEFILE|Supportato.|  
|SQL_PACKET_SIZE|Non supportato.|  
|SQL_QUIET_MODE|Non supportato.|  
|SQL_TRANSLATE_DLL|Non supportato.|  
|SQL_TRANSLATION_OPTION|Non supportato.|  
|SQL_TXN_ISOLATION|Non supportato.|
