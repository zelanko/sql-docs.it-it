---
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
ms.openlocfilehash: e151e3abc4032ea3180e46360c501d9fbea9ae30
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301462"
---
# <a name="sqlsetpos-desktop-database-drivers"></a>SQLSetPos (driver di database desktop)
Sono supportate la semantica del modello bulk per le chiamate **SQLSetPos** con l'argomento *IRow* uguale a 0.  
  
 SQL_LOCK_NO_CHANGE è supportato per *Flock*. SQL_LOCK_EXCLUSIVE e SQL_LOCK_UNLOCK non sono supportati.  
  
 **SQLSetPos** supporta i join aggiornabili. Per ulteriori informazioni, vedere la *Guida per programmatori Microsoft Jet motore di database*.
