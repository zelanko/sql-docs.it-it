---
title: SQLSetScrollOptions (driver di Database Desktop) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Desktop Database Drivers
ms.assetid: 51d643ed-015b-4639-969a-9491d9875aca
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0adedfb69cd4a7b5cf195916747687826805e8bf
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67905395"
---
# <a name="sqlsetscrolloptions-desktop-database-drivers"></a>SQLSetScrollOptions (driver di database desktop)
Sono supportati i cursori statici e forward per SQL_CONCUR_READ_ONLY.  
  
 Solo i cursori gestito da keyset sono supportati per un *fConcurrency* argomento di SQL_CONCUR_LOCK.  
  
 Un' *fConcurrency* argomento di SQL_CONCUR_ROWVER non è supportato.  
  
 I cursori Dynamic e cursori misti non sono supportati.
