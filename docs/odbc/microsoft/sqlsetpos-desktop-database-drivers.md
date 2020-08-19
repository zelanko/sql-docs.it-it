---
description: SQLSetPos (driver di database desktop)
title: SQLSetPos (driver di database desktop) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4aa126514bc84f5546e1f4a022d8d3e6235b2e7c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421665"
---
# <a name="sqlsetpos-desktop-database-drivers"></a>SQLSetPos (driver di database desktop)
Sono supportate la semantica del modello bulk per le chiamate **SQLSetPos** con l'argomento *IRow* uguale a 0.  
  
 SQL_LOCK_NO_CHANGE è supportato per *Flock*. SQL_LOCK_EXCLUSIVE e SQL_LOCK_UNLOCK non sono supportati.  
  
 **SQLSetPos** supporta i join aggiornabili. Per ulteriori informazioni, vedere la *Guida per programmatori Microsoft Jet motore di database*.
