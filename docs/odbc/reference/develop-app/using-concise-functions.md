---
title: Uso di funzioni concise | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306782"
---
# <a name="using-concise-functions"></a>Uso di funzioni concise
Alcune funzioni ODBC ottengono l'accesso implicito ai descrittori. I writer di applicazioni possono trovarli più convenienti rispetto alla chiamata a **SQLSetDescField** o **SQLGetDescField**. Queste funzioni sono denominate funzioni *concise* perché eseguono numerose funzioni, tra cui l'impostazione o il recupero dei campi del descrittore. Alcune funzioni concise consentono a un'applicazione di impostare o recuperare diversi campi di descrizione correlati in una singola chiamata di funzione.  
  
 È possibile chiamare funzioni concise senza prima recuperare un handle del descrittore da usare come argomento. Queste funzioni funzionano con i campi di descrizione associati all'handle di istruzione su cui vengono chiamati.  
  
 Le funzioni concise **SQLBindCol** e **SQLBindParameter** associano una colonna o un parametro impostando i campi di descrizione che corrispondono ai rispettivi argomenti. Ognuna di queste funzioni esegue più attività rispetto alla semplice impostazione dei descrittori. **SQLBindCol** e **SQLBindParameter** forniscono una specifica completa dell'associazione di una colonna di dati o di un parametro dinamico. Un'applicazione, tuttavia, può modificare i singoli dettagli di un'associazione chiamando **SQLSetDescField** o **SQLSetDescRec** e può associare completamente una colonna o un parametro effettuando una serie di chiamate appropriate a tali funzioni.  
  
 Le funzioni concise **SQLColAttribute**, **SQLDescribeCol**, **SQLDescribeParam**, **SQLNumParams**e **SQLNumResultCols** recuperano i valori nei campi del descrittore.  
  
 **SQLSetDescRec** e **SQLGetDescRec** sono funzioni concise che, con una chiamata, impostano o ottengono più campi di descrizione che influiscono sul tipo di dati e sull'archiviazione dei dati di colonna o di parametro. **SQLSetDescRec** è un modo efficace per modificare il binding dei dati di colonna o di parametro in un unico passaggio.  
  
 In alcuni casi, **SQLSetStmtAttr** e **SQLGetStmtAttr** vengono usati come funzioni concise. (Vedere [campi del descrittore](../../../odbc/reference/develop-app/descriptor-fields.md)).
