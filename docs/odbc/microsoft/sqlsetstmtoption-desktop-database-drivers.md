---
title: SQLSetStmtOption (driver di database desktop) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 69b386aee3f95fd047f72510dce7658130ac7aa5
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299411"
---
# <a name="sqlsetstmtoption-desktop-database-drivers"></a>SQLSetStmtOption (driver di database desktop)

|*fOption*|Commenti|  
|---------------|--------------|  
|SQL_ASYNC_ENABLE|L'elaborazione asincrona non è supportata. Il SQL_ASYNC_ENABLE fOption restituirà SQLSTATE S1C00 (driver non è in grado di supportare).|  
|SQL_KEYSET_SIZE|L'unica dimensione del keyset valida è 0, perché i cursori misti e dinamici non sono supportati. Se questo valore è impostato su un altro numero, verrà modificato in 0 e la chiamata restituirà SQL_SUCCESS_WITH_INFO e SQLSTATE 01S02 (opzione valore modificato).|  
|SQL_MAX_ROWS|L'unica dimensione valida del set di righe è 0, perché i driver del database desktop non supportano la limitazione del numero di righe restituite. Se questo valore è impostato su un altro numero, verrà modificato in 0 e la chiamata restituirà SQL_SUCCESS_WITH_INFO e SQLSTATE 01S02 (opzione valore modificato).|  
|SQL_QUERY_TIMEOUT|Non supportato.|  
|SQL_ROW_NUMBER|Non supportato.|  
|SQL_SIMULATE_CURSOR|Non supportato.|
