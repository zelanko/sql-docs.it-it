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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8bd21010908473e4216a02a504b2de25578d5c84
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299761"
---
# <a name="sqldescribecol-and-sqlcolattribute"></a>SQLDescribeCol e SQLColAttribute
**SQLDescribeCol** e **SQLColAttribute** vengono utilizzati per recuperare i metadati del set di risultati. La differenza tra queste due funzioni è che **SQLDescribeCol** restituisce sempre le stesse cinque informazioni (nome, tipo di dati, precisione, scala e supporto di valori null della colonna), mentre **SQLColAttribute** restituisce una singola informazione richiesta dall'applicazione. Tuttavia, **SQLColAttribute** può restituire una selezione molto più dettagliata dei metadati, incluse la distinzione tra maiuscole e minuscole di una colonna, le dimensioni di visualizzazione, la aggiornabilità e la ricerca.  
  
 Molte applicazioni, in particolare quelle che visualizzano solo i dati, richiedono solo i metadati restituiti da **SQLDescribeCol**. Per queste applicazioni, è più veloce usare **SQLDescribeCol** di **SQLColAttribute** perché le informazioni vengono restituite in una singola chiamata. Altre applicazioni, in particolare quelle che aggiornano i dati, richiedono i metadati aggiuntivi restituiti da **SQLColAttribute** e quindi usano entrambe le funzioni. Inoltre, **SQLColAttribute** supporta i metadati specifici del driver; Per ulteriori informazioni, vedere [tipi di dati specifici del driver, tipi di descrittori, tipi di informazioni, tipi di diagnostica e attributi](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
 Un'applicazione può recuperare i metadati del set di risultati in qualsiasi momento dopo la preparazione o l'esecuzione di un'istruzione e prima della chiusura del cursore sul set di risultati. Pochissime applicazioni richiedono i metadati del set di risultati dopo che l'istruzione è stata preparata e prima di essere eseguita. Se possibile, le applicazioni devono attendere per recuperare i metadati fino a dopo l'esecuzione dell'istruzione, perché alcune origini dati non possono restituire metadati per le istruzioni preparate e l'emulazione di questa funzionalità nel driver è spesso un processo lento. Il driver, ad esempio, potrebbe generare un set di risultati di riga zero sostituendo la clausola **where** di un'istruzione **Select** con la clausola **WHERE 1 = 2** ed eseguendo l'istruzione risultante.  
  
 I metadati sono spesso costosi da recuperare dall'origine dati. Per questo motivo, è necessario memorizzare nella cache i metadati recuperati dal server e mantenerli per tutto il tempo in cui il cursore sul set di risultati è aperto. Inoltre, le applicazioni devono richiedere solo i metadati necessari.
