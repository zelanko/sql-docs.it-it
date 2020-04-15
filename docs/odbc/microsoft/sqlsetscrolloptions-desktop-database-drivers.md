---
title: Proprietà SQLSetScrollOptions (Driver di database desktop) Documenti Microsoft
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299436"
---
# <a name="sqlsetscrolloptions-desktop-database-drivers"></a>SQLSetScrollOptions (driver di database desktop)
I cursori avanti e statici sono supportati per SQL_CONCUR_READ_ONLY.  
  
 Solo i cursori basati su keyset sono supportati per un argomento *fConcurrency* di SQL_CONCUR_LOCK.  
  
 Un argomento *fConcurrency* di SQL_CONCUR_ROWVER non è supportato.  
  
 I cursori dinamici e i cursori misti non sono supportati.
