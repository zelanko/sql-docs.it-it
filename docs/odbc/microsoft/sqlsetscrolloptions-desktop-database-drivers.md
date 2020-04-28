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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5c47255b455354c49133d61c3546be63ab2380a1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299436"
---
# <a name="sqlsetscrolloptions-desktop-database-drivers"></a>SQLSetScrollOptions (driver di database desktop)
I cursori statici e di avanzamento sono supportati per SQL_CONCUR_READ_ONLY.  
  
 Solo i cursori gestiti da keyset sono supportati per un argomento *fConcurrency* di SQL_CONCUR_LOCK.  
  
 Un argomento *fConcurrency* di SQL_CONCUR_ROWVER non è supportato.  
  
 I cursori dinamici e i cursori misti non sono supportati.
