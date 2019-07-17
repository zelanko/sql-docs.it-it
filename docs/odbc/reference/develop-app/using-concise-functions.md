---
title: Utilizzo di funzioni Concise | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- concise functions [ODBC]
- functions [ODBC], concise functions
- descriptors [ODBC], concise functions
ms.assetid: 31ac070f-8c59-4fd5-bd5a-466bb27dbca0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 43004601845d3032d404c308b7b1fa4850f694ee
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022197"
---
# <a name="using-concise-functions"></a>Uso di funzioni concise
Alcune funzioni ODBC accedono in modo implicito a descrittori. Gli autori di applicazioni possono trovarle più conveniente rispetto alla chiamata **SQLSetDescField** oppure **SQLGetDescField**. Queste funzioni vengono chiamate *concisa* funzioni poiché eseguono una serie di funzioni, tra cui l'impostazione o recupero di campi di descrizione. Alcune funzioni concise modo un'applicazione può impostare o recuperare diversi campi di descrizione correlati in una singola chiamata di funzione.  
  
 Funzioni concise possono essere chiamate senza prima recuperare un handle descrittore per l'uso come argomento. Queste funzioni usano i campi di descrizione associati all'handle di istruzione che vengono chiamate su.  
  
 Le funzioni concise **SQLBindCol** e **SQLBindParameter** associare una colonna o parametro, impostando i campi di descrizione che corrispondono ai relativi argomenti. Ognuna di queste funzioni esegue più attività rispetto all'impostazione descrittori. **SQLBindCol** e **SQLBindParameter** fornire una specifica completa dell'associazione di una colonna di dati o un parametro dinamico. Un'applicazione può, tuttavia, modificare i singoli dettagli di un'associazione chiamando **SQLSetDescField** oppure **SQLSetDescRec** e può associare completamente effettuando una serie di chiamate adatte per una colonna o parametro Queste funzioni.  
  
 Le funzioni concise **SQLColAttribute**, **SQLDescribeCol**, **SQLDescribeParam**, **SQLNumParams**, e  **SQLNumResultCols** recuperare i valori nei campi del descrittore.  
  
 **SQLSetDescRec** e **SQLGetDescRec** sono funzioni concise che, con una sola chiamata, impostano oppure ottengono più campi di descrizione che determinano il tipo di dati e archiviazione dei dati di colonna o parametro. **SQLSetDescRec** è un metodo efficace per modificare l'associazione di dati di colonna o parametro in un unico passaggio.  
  
 **SQLSetStmtAttr** e **SQLGetStmtAttr** fungono da funzioni concise in alcuni casi. (Vedere [campi di descrizione](../../../odbc/reference/develop-app/descriptor-fields.md).)
