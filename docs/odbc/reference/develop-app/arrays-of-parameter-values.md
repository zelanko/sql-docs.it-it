---
title: Le matrici di valori di parametro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arrays of parameter values [ODBC]
- parameter arrays [ODBC]
ms.assetid: 9b572c5b-1dfe-40af-bebd-051548ab6d90
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 03479a0187c7720a595b550290a8f5ac8197fa9c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63288405"
---
# <a name="arrays-of-parameter-values"></a>Matrici di valori di parametro
È spesso utile per le applicazioni passare le matrici di parametri. Ad esempio, utilizzando le matrici di parametri e una con parametri **Inserisci** istruzione, un'applicazione può inserire un numero di righe in una sola volta. Esistono diversi vantaggi nell'uso delle matrici. Prima di tutto il traffico di rete viene ridotto perché i dati per numerose istruzioni vengono inviati in un singolo pacchetto (se l'origine dati supporta matrici di parametri in modo nativo). In secondo luogo, alcune origini dati possono eseguire istruzioni SQL con le matrici più velocemente rispetto all'esecuzione lo stesso numero di istruzioni SQL separate. Infine, quando i dati vengono archiviati in una matrice, come spesso accade per i dati della schermata, l'applicazione può associare tutte le righe in una particolare colonna con una singola chiamata a **SQLBindParameter** e aggiornarle tramite l'esecuzione di una singola istruzione.  
  
 Sfortunatamente, non molte origini dati supportano le matrici di parametri. Tuttavia, un driver in grado di emulare le matrici di parametri tramite l'esecuzione di un'istruzione SQL una volta per ogni set di valori di parametro. Questo può causare un aumento di velocità perché il driver può quindi preparare l'istruzione che l'azienda pianifica di eseguire una sola volta per ogni set di parametri. Può anche comportare per semplificare il codice dell'applicazione.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Associazione delle matrici di parametri](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)  
  
-   [Utilizzo delle matrici di parametri](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)
