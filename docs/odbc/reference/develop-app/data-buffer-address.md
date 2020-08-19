---
description: Indirizzo del buffer dei dati
title: Indirizzo buffer dei dati | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- address of data buffers [ODBC]
- buffers [ODBC], data
- data buffers [ODBC], address
ms.assetid: f2426d68-71bc-4ef7-a5cb-ee9d6c1c9671
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 301202933ae9cb0206100b6bbf10dda305495be1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429383"
---
# <a name="data-buffer-address"></a>Indirizzo del buffer dei dati
L'applicazione passa l'indirizzo del buffer di dati al driver in un argomento, spesso denominato *ValuePtr* o un nome simile. Ad esempio, nella chiamata seguente a **SQLBindCol**, l'applicazione specifica l'indirizzo della variabile *date* :  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER DateInd;  
SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &dsDate, 0, &DateInd);  
```  
  
 Come indicato nella sezione [allocazione e liberazione dei buffer](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md) , l'indirizzo di un buffer posticipato deve rimanere valido finché il buffer non è associato.  
  
 A meno che non sia esplicitamente vietato, l'indirizzo di un buffer dei dati può essere un puntatore null. Per i buffer utilizzati per inviare dati al driver, il driver ignora le informazioni normalmente contenute nel buffer. Per i buffer utilizzati per recuperare i dati dal driver, il driver non restituisce alcun valore. In entrambi i casi, il driver ignora l'argomento della lunghezza del buffer di dati corrispondente.
