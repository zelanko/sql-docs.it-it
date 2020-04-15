---
title: Proprietà SQLDescribeCol e SQLColAttribute . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8bd21010908473e4216a02a504b2de25578d5c84
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299761"
---
# <a name="sqldescribecol-and-sqlcolattribute"></a>SQLDescribeCol e SQLColAttribute
**SQLDescribeCol** e **SQLColAttribute** vengono utilizzati per recuperare i metadati del set di risultati. La differenza tra queste due funzioni è che **SQLDescribeCol** restituisce sempre le stesse cinque informazioni (nome di una colonna, tipo di dati, precisione, scala e supporto di valori Null), mentre **SQLColAttribute** restituisce una singola informazione richiesta dall'applicazione. Tuttavia, **SQLColAttribute** può restituire una selezione molto più ricca di metadati, tra cui la distinzione tra maiuscole e minuscole di una colonna, le dimensioni di visualizzazione, l'aggiornamento e la ricercabilità.  
  
 Molte applicazioni, in particolare quelle che visualizzano solo i dati, richiedono solo i metadati restituiti da **SQLDescribeCol**. Per queste applicazioni, è più veloce utilizzare **SQLDescribeCol** rispetto a **SQLColAttribute** perché le informazioni vengono restituite in una singola chiamata. Altre applicazioni, in particolare quelle che aggiornano i dati, richiedono i metadati aggiuntivi restituiti da **SQLColAttribute** e pertanto utilizzano entrambe le funzioni. Inoltre, **SQLColAttribute** supporta i metadati specifici del driver; Per ulteriori informazioni, vedere [Tipi di dati specifici del driver, Tipi di descrittore, Tipi di informazioni, Tipi di diagnostica e Attributi](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
 Un'applicazione può recuperare i metadati del set di risultati in qualsiasi momento dopo la preparazione o l'esecuzione di un'istruzione e prima che il cursore sul set di risultati venga chiuso. Pochissime applicazioni richiedono metadati del set di risultati dopo la preparazione dell'istruzione e prima dell'esecuzione. Se possibile, le applicazioni devono attendere di recuperare i metadati fino a dopo l'esecuzione dell'istruzione, perché alcune origini dati non possono restituire metadati per le istruzioni preparate ed emulare questa funzionalità nel driver è spesso un processo lento. Ad esempio, il driver potrebbe generare un set di risultati a riga zero sostituendo la clausola **WHERE** di un'istruzione **SELECT** con la clausola WHERE 1 **e 2** ed eseguendo l'istruzione risultante.  
  
 I metadati sono spesso costosi da recuperare dall'origine dati. Per questo motivo, i driver devono memorizzare nella cache tutti i metadati recuperati dal server e tenerli premuti per tutto il tempo in cui il cursore sul set di risultati è aperto. Inoltre, le applicazioni devono richiedere solo i metadati di cui hanno assolutamente bisogno.
