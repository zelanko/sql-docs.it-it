---
title: Matrici di valori di parametro Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: eb9389c769e3a7bb0c39959a559531e8051a7bec
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298800"
---
# <a name="arrays-of-parameter-values"></a>Matrici di valori di parametro
È spesso utile per le applicazioni passare matrici di parametri. Ad esempio, utilizzando matrici di parametri e un'istruzione **INSERT** con parametri, un'applicazione può inserire un numero di righe contemporaneamente. L'utilizzo degli array presenta diversi vantaggi. In primo luogo, il traffico di rete viene ridotto perché i dati per molte istruzioni vengono inviati in un singolo pacchetto (se l'origine dati supporta le matrici di parametri in modo nativo). In secondo luogo, alcune origini dati possono eseguire istruzioni SQL utilizzando le matrici più velocemente rispetto all'esecuzione dello stesso numero di istruzioni SQL separate. Infine, quando i dati vengono archiviati in una matrice, come spesso accade per i dati dello schermo, l'applicazione può associare tutte le righe in una determinata colonna con una singola chiamata a **SQLBindParameter** e aggiornarle eseguendo una singola istruzione.  
  
 Sfortunatamente, non molte origini dati supportano matrici di parametri. Tuttavia, un driver può emulare le matrici di parametri eseguendo un'istruzione SQL una volta per ogni set di valori di parametro. Ciò può comportare un aumento della velocità perché il driver può quindi preparare l'istruzione che prevede di eseguire una volta per ogni set di parametri. Potrebbe anche portare a codice dell'applicazione più semplice.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Associazione delle matrici di parametri](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)  
  
-   [Uso delle matrici di parametri](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)
