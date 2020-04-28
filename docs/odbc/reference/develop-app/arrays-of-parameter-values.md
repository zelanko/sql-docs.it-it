---
title: Matrici di valori di parametri | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298800"
---
# <a name="arrays-of-parameter-values"></a>Matrici di valori di parametro
Spesso è utile per le applicazioni passare matrici di parametri. Usando, ad esempio, matrici di parametri e un'istruzione **Insert** con parametri, un'applicazione può inserire un numero di righe in una sola volta. L'uso delle matrici presenta diversi vantaggi. In primo luogo, il traffico di rete viene ridotto perché i dati per molte istruzioni vengono inviati in un singolo pacchetto (se l'origine dati supporta le matrici di parametri in modo nativo). In secondo luogo, alcune origini dati possono eseguire istruzioni SQL utilizzando matrici più velocemente rispetto all'esecuzione dello stesso numero di istruzioni SQL separate. Infine, quando i dati vengono archiviati in una matrice, come spesso accade per i dati dello schermo, l'applicazione può associare tutte le righe di una determinata colonna con una singola chiamata a **SQLBindParameter** e aggiornarle eseguendo una singola istruzione.  
  
 Sfortunatamente, non molte origini dati supportano le matrici di parametri. Un driver può tuttavia emulare le matrici di parametri eseguendo un'istruzione SQL una volta per ogni set di valori di parametro. Ciò può comportare un aumento della velocità, perché il driver può quindi preparare l'istruzione che prevede di eseguire una volta per ogni set di parametri. Potrebbe anche risultare più semplice codice dell'applicazione.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Associazione delle matrici di parametri](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)  
  
-   [Uso delle matrici di parametri](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)
