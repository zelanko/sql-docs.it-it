---
title: 'Indirizzo del buffer di dati : Documenti Microsoft'
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
ms.openlocfilehash: 578e4e37a78818cb640d9f32e2480cec5951df63
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305272"
---
# <a name="data-buffer-address"></a>Indirizzo del buffer dei dati
L'applicazione passa l'indirizzo del buffer di dati al driver in un argomento, spesso denominato *ValuePtr* o un nome simile. Ad esempio, nella seguente chiamata a **SQLBindCol**, l'applicazione specifica l'indirizzo della variabile *Date:*  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER DateInd;  
SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &dsDate, 0, &DateInd);  
```  
  
 Come indicato nella sezione [Allocazione e liberazione di buffer,](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md) l'indirizzo di un buffer posticipato deve rimanere valido fino a quando il buffer non viene associato.  
  
 A meno che non sia specificamente vietato, l'indirizzo di un buffer di dati può essere un puntatore null. Per i buffer utilizzati per inviare dati al driver, in questo modo il driver ignorare le informazioni normalmente contenute nel buffer. Per i buffer utilizzati per recuperare i dati dal driver, in questo modo il driver non restituire un valore. In entrambi i casi, il driver ignora l'argomento di lunghezza del buffer di dati corrispondente.
