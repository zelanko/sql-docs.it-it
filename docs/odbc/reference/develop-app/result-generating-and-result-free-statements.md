---
title: Istruzioni per la generazione di risultati e senza risultato | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 55b2ff4d428f02b59883b675fde95531366f0b4d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020597"
---
# <a name="result-generating-and-result-free-statements"></a>Istruzioni per la generazione di risultati e senza risultati
Le istruzioni SQL possono essere suddivise in categorie separate nelle cinque categorie seguenti:  
  
-   **Set di risultati-generazione di istruzioni** Si tratta di istruzioni SQL che generano un set di risultati. Ad esempio, un'istruzione **Select** .  
  
-   **Conteggio righe-generazione di istruzioni** Si tratta di istruzioni SQL che generano un conteggio delle righe interessate. Ad esempio, un'istruzione **Update** o **Delete** .  
  
-   **Istruzioni DDL (Data Definition Language)** Si tratta di istruzioni SQL che modificano la struttura del database. Ad esempio, **Create Table** o **Drop index**.  
  
-   **Istruzioni** per la modifica del contesto Si tratta di istruzioni SQL che modificano il contesto di un database. Ad esempio, le istruzioni **use** e **set** in SQL Server.  
  
-   **Istruzioni amministrative** Si tratta di istruzioni SQL utilizzate per scopi amministrativi in un database. Ad esempio, **Grant** e **Revoke**.  
  
 Le istruzioni SQL nelle prime due categorie sono note collettivamente come *istruzioni di generazione dei risultati*. Le istruzioni SQL nelle ultime tre categorie sono note collettivamente come *istruzioni senza risultato*. ODBC definisce la semantica dei batch che includono solo istruzioni per la generazione di risultati. Queste semantiche variano notevolmente e sono pertanto specifiche dell'origine dati. Il driver SQL Server, ad esempio, non supporta l'eliminazione di un oggetto e quindi il riferimento o la ricreazione dello stesso oggetto nello stesso batch. Il termine *batch* usato in questo manuale si riferisce quindi solo ai batch di istruzioni di generazione dei risultati.
