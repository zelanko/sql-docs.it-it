---
title: SQLSetScrollOptions (driver di database desktop) | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67905395"
---
# <a name="sqlsetscrolloptions-desktop-database-drivers"></a>SQLSetScrollOptions (driver di database desktop)
I cursori statici e di avanzamento sono supportati per SQL_CONCUR_READ_ONLY.  
  
 Solo i cursori gestiti da keyset sono supportati per un argomento *fConcurrency* di SQL_CONCUR_LOCK.  
  
 Un argomento *fConcurrency* di SQL_CONCUR_ROWVER non è supportato.  
  
 I cursori dinamici e i cursori misti non sono supportati.
