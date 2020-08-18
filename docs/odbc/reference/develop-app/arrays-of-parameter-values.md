---
description: Matrici di valori di parametro
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
ms.openlocfilehash: 230f15f1c9cae0509ba7d616ab61ed5d8d7a370b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483114"
---
# <a name="arrays-of-parameter-values"></a>Matrici di valori di parametro
Spesso è utile per le applicazioni passare matrici di parametri. Usando, ad esempio, matrici di parametri e un'istruzione **Insert** con parametri, un'applicazione può inserire un numero di righe in una sola volta. L'uso delle matrici presenta diversi vantaggi. In primo luogo, il traffico di rete viene ridotto perché i dati per molte istruzioni vengono inviati in un singolo pacchetto (se l'origine dati supporta le matrici di parametri in modo nativo). In secondo luogo, alcune origini dati possono eseguire istruzioni SQL utilizzando matrici più velocemente rispetto all'esecuzione dello stesso numero di istruzioni SQL separate. Infine, quando i dati vengono archiviati in una matrice, come spesso accade per i dati dello schermo, l'applicazione può associare tutte le righe di una determinata colonna con una singola chiamata a **SQLBindParameter** e aggiornarle eseguendo una singola istruzione.  
  
 Sfortunatamente, non molte origini dati supportano le matrici di parametri. Un driver può tuttavia emulare le matrici di parametri eseguendo un'istruzione SQL una volta per ogni set di valori di parametro. Ciò può comportare un aumento della velocità, perché il driver può quindi preparare l'istruzione che prevede di eseguire una volta per ogni set di parametri. Potrebbe anche risultare più semplice codice dell'applicazione.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Associazione delle matrici di parametri](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md)  
  
-   [Uso delle matrici di parametri](../../../odbc/reference/develop-app/using-arrays-of-parameters.md)
