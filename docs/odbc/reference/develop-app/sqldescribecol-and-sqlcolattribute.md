---
title: SQLDescribeCol e SQLColAttribute | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLColAttribute function [ODBC], and SQLDescribeCol
- SQLDescribeCol function [ODBC], and SQLColAttribute
- result sets [ODBC], metadata
- retrieving result set meta data [ODBC]
- metadata [ODBC], result set
ms.assetid: c2ca442c-03a8-4e0f-9e67-b300bb15962f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e569e51540cbaa5612b158abdacac5faae77f940
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63149034"
---
# <a name="sqldescribecol-and-sqlcolattribute"></a>SQLDescribeCol e SQLColAttribute
**SQLDescribeCol** e **SQLColAttribute** vengono utilizzati per recuperare i metadati dei set di risultati. La differenza tra queste due funzioni è che **SQLDescribeCol** restituisce sempre la stesse e cinque le informazioni (di una colonna nome, tipo di dati, precisione, scala e supporto di valori null), mentre **SQLColAttribute** restituisce una singola informazione richiesto dall'applicazione. Tuttavia **SQLColAttribute** può restituire una selezione molto più ampio di metadati, tra cui distinzione maiuscole/minuscole di una colonna, visualizzare le dimensioni, degli aggiornamenti e individuabilità.  
  
 Molte applicazioni, in particolare quelli che consentono di visualizzare solo i dati richiedono soltanto i metadati restituiti da **SQLDescribeCol**. Per queste applicazioni, risulta più veloce usare **SQLDescribeCol** rispetto **SQLColAttribute** perché le informazioni vengono restituite in una singola chiamata. Altre applicazioni, in particolare quelli che aggiornano i dati, richiedono i metadati aggiuntivi restituiti da **SQLColAttribute** e pertanto utilizzare entrambe le funzioni. È inoltre **SQLColAttribute** supporta i metadati specifici del driver; per altre informazioni, vedere [tipi di dati specifici del Driver, tipi di descrittori, tipi di informazioni, tipi di diagnostica e gli attributi](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
 Un'applicazione può recuperare i metadati dei set di risultati in qualsiasi momento dopo che è stata preparata o eseguita un'istruzione e prima del cursore sul risultato del set viene chiuso. Poche applicazioni richiedono metadati del set di risultati dopo l'istruzione viene preparata e prima che venga eseguito. Se possibile, le applicazioni devono attendere per recuperare i metadati fino a dopo l'istruzione viene eseguita, perché alcune origini dati non è possibile restituire i metadati per le istruzioni preparate e questa funzionalità nel driver di emulazione è spesso un processo lenta. Ad esempio, il driver potrebbe generare un risultato a riga zero impostato mediante la sostituzione il **in cui** clausola di un **selezionare** istruzione con la clausola **WHERE 1 = 2** e l'esecuzione il istruzione risultante.  
  
 I metadati sono spesso costosi da recuperare dall'origine dati. Per questo motivo, i driver devono memorizzare nella cache tutti i metadati sono recuperare dal server e tenere premuto che per fino a quando il cursore sul risultato del set è aperto. Inoltre, le applicazioni devono richiedere solo i metadati che sono assolutamente necessario.
