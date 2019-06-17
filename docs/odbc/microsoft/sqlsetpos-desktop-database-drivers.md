---
title: SQLSetPos (driver di Database Desktop) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetPos function [ODBC], Desktop Database Drivers
ms.assetid: 8ef027ec-8512-48fe-8fe2-2ff7cd81e331
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 95117c82c213851d2e0600e65d8061ce532d9933
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63200459"
---
# <a name="sqlsetpos-desktop-database-drivers"></a>SQLSetPos (driver di database desktop)
La semantica di blocco-model per **SQLSetPos** chiama con il *irow* argomento uguale a 0 sono supportati.  
  
 SQL_LOCK_NO_CHANGE è supportata per *branco*. SQL_LOCK_EXCLUSIVE e SQL_LOCK_UNLOCK non sono supportati.  
  
 **SQLSetPos** aggiornabile join sono supportati. (Per altre informazioni, vedere la *Guida per programmatori di Microsoft Jet Database Engine*.)
