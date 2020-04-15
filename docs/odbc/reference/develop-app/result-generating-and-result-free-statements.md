---
title: Dichiarazioni di generazione dei risultati e non- dei risultati Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- result-generating statements [ODBC]
- batches [ODBC], result-generating statements
- batches [ODBC], result-free statements
- SQL statements [ODBC], batches
- result-free statements [ODBC]
ms.assetid: 2f3475d1-3999-4dd8-aba2-a6e1299c95f8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fc94aabd7982fba5879519573980db03b1857ef6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300091"
---
# <a name="result-generating-and-result-free-statements"></a>Istruzioni per la generazione di risultati e senza risultati
Le istruzioni SQL possono essere suddivise liberamente nelle cinque categorie seguenti:SQL statements can be loosely divided into the following five categories:  
  
-   Istruzioni di **generazione set di risultatiResult Set-Generating Statements** Si tratta di istruzioni SQL che generano un set di risultati. Ad esempio, un'istruzione **SELECT.**  
  
-   **Istruzioni per la generazione di conteggi delle righeRow Count-Generating Statements** Si tratta di istruzioni SQL che generano un conteggio delle righe interessate. Ad esempio, **un'istruzione UPDATE** o **DELETE.**  
  
-   **Istruzioni DDL (Data Definition Language)** Si tratta di istruzioni SQL che modificano la struttura del database. Ad esempio, **CREATE TABLE** o **DROP INDEX**.  
  
-   **Istruzioni di modifica del contestoContext-Changing Statements** Si tratta di istruzioni SQL che modificano il contesto di un database. Ad esempio, le istruzioni **USE** e **SET** in SQL Server.  
  
-   **Dichiarazioni amministrative** Si tratta di istruzioni SQL utilizzate per scopi amministrativi in un database. Ad esempio, **GRANT** e **REVOKE**.  
  
 Le istruzioni SQL nelle prime due categorie sono note collettivamente come istruzioni che *generano risultati.* Le istruzioni SQL nelle ultime tre categorie sono collettivamente note come *istruzioni senza risultati*. ODBC definisce la semantica dei batch che includono solo istruzioni che generano risultati. Queste semantiche variano ampiamente e sono pertanto specifiche dell'origine dati. Ad esempio, il driver di SQL Server non supporta l'eliminazione di un oggetto e quindi fa riferimento o ricreare lo stesso oggetto nello stesso batch. Pertanto, il termine *batch* utilizzato in questo manuale si riferisce solo ai batch di istruzioni di generazione di risultati.
