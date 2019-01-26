---
title: SQLSetStmtOption (driver di Database Desktop) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetStmtOption function [ODBC], Desktop Database Drivers
ms.assetid: 98db9631-eb9b-4962-abe4-96f495133a5d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 48dc5dff83e942b894548d44e3673c19ca0746c5
ms.sourcegitcommit: 1e28f923cda9436a4395a405ebda5149202f8204
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 01/25/2019
ms.locfileid: "55044874"
---
# <a name="sqlsetstmtoption-desktop-database-drivers"></a>SQLSetStmtOption (driver di database desktop)

|*fOption*|Commenti|  
|---------------|--------------|  
|SQL_ASYNC_ENABLE|L'elaborazione asincrona non è supportata. Il fOption SQL_ASYNC_ENABLE restituiranno SQLSTATE S1C00 (non è in grado di Driver).|  
|SQL_KEYSET_SIZE|La dimensione del keyset solo valido è 0, poiché combinato e cursori dinamici non sono supportati. Se questo valore è impostato su qualsiasi altro numero, verrà modificato su 0 e la chiamata restituisce SQL_SUCCESS_WITH_INFO e SQLSTATE 01S02 (valore dell'opzione modificato).|  
|SQL_MAX_ROWS|Le dimensioni del set di righe solo valido sono 0, poiché i driver di Database Desktop non supportano limitando il numero di righe restituite. Se questo valore è impostato su qualsiasi altro numero, verrà modificato su 0 e la chiamata restituisce SQL_SUCCESS_WITH_INFO e SQLSTATE 01S02 (valore dell'opzione modificato).|  
|SQL_QUERY_TIMEOUT|Non supportato.|  
|SQL_ROW_NUMBER|Non supportato.|  
|SQL_SIMULATE_CURSOR|Non supportato.|
