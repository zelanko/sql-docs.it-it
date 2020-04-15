---
title: Utilizzo delle funzioni concise Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 63313e3dfaec8dbcd91f3bb084bbaab46da40c6e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306782"
---
# <a name="using-concise-functions"></a>Uso di funzioni concise
Alcune funzioni ODBC ottengono l'accesso implicito ai descrittori. I writer di applicazioni possono trovarli più pratici rispetto alla chiamata di **SQLSetDescField** o **SQLGetDescField**. Queste funzioni sono chiamate funzioni *concise* perché eseguono una serie di funzioni, tra cui l'impostazione o il recupero dei campi descrittore. Alcune funzioni concise consentono a un'applicazione di impostare o recuperare diversi campi descrittore correlati in una singola chiamata di funzione.  
  
 Le funzioni concise possono essere chiamate senza prima recuperare un handle di descrittore da utilizzare come argomento. Queste funzioni funzionano con i campi del descrittore associati all'handle di istruzione su cui vengono chiamati.  
  
 Le funzioni concise **SQLBindCol** e **SQLBindParameter** associano una colonna o un parametro impostando i campi del descrittore che corrispondono ai relativi argomenti. Ognuna di queste funzioni esegue più attività rispetto alla semplice impostazione di descrittori. **SQLBindCol** e **SQLBindParameter** forniscono una specifica completa dell'associazione di una colonna di dati o di un parametro dinamico. Un'applicazione può, tuttavia, modificare singoli dettagli di un'associazione chiamando **SQLSetDescField** o **SQLSetDescRec** e può associare completamente una colonna o un parametro effettuando una serie di chiamate adatte a queste funzioni.  
  
 Le funzioni concise **SQLColAttribute**, **SQLDescribeCol**, **SQLDescribeParam**, **SQLNumParams**e **SQLNumResultCols recuperano i** valori nei campi del descrittore.  
  
 **SQLSetDescRec** e **SQLGetDescRec** sono funzioni concise che, con una sola chiamata, impostano o ottengono più campi descrittore che influiscono sul tipo di dati e sull'archiviazione dei dati di colonna o parametro. **SQLSetDescRec** è un modo efficace per modificare l'associazione dei dati di colonna o parametro in un unico passaggio.  
  
 **SQLSetStmtAttr** e **SQLGetStmtAttr** fungono in alcuni casi come funzioni concise. (Vedere [Campi descrittore](../../../odbc/reference/develop-app/descriptor-fields.md).)
