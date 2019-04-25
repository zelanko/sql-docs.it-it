---
title: Indirizzo del Buffer di dati | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f07f835361fcf29143376fe468a55f0bf26e31e3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62471130"
---
# <a name="data-buffer-address"></a>Indirizzo del buffer dei dati
L'applicazione passa l'indirizzo del buffer di dati del driver in un argomento, spesso denominato *ValuePtr* o un nome simile. Ad esempio, nella chiamata seguente a **SQLBindCol**, l'applicazione specifica l'indirizzo del *data* variabile:  
  
```  
SQL_DATE_STRUCT Date;  
SQLINTEGER DateInd;  
SQLBindCol(hstmt, 1, SQL_C_TYPE_DATE, &dsDate, 0, &DateInd);  
```  
  
 Come accennato nella [allocazione e liberazione di buffer](../../../odbc/reference/develop-app/allocating-and-freeing-buffers.md) sezione, indirizzo di un buffer in posticipate deve rimanere valido fino a quando il buffer non è associato.  
  
 A meno che non è specificamente consentito, l'indirizzo di un buffer di dati può essere un puntatore null. Per i buffer usati per inviare dati al driver, in questo modo il driver ignorare le informazioni contenute in genere nel buffer. Per i buffer utilizzati per recuperare dati dal driver, in questo modo, il driver non restituisce alcun valore. In entrambi i casi, il driver ignora l'argomento di lunghezza del buffer di dati corrispondente.
