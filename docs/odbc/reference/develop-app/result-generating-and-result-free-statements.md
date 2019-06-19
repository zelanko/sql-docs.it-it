---
title: Le istruzioni di generazione di risultati e senza risultati | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: f357576e9e7510ae581b41a50976a34981f35109
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62861521"
---
# <a name="result-generating-and-result-free-statements"></a>Istruzioni per la generazione di risultati e senza risultati
Istruzioni SQL possono essere suddivisi nelle categorie seguenti cinque a regime di controllo libero:  
  
-   **Generare istruzioni che generano Set** si tratta di istruzioni SQL che generano un set di risultati. Ad esempio, un **seleziona** istruzione.  
  
-   **Le istruzioni per la generazione di conteggio di righe** si tratta di istruzioni SQL che generano un conteggio delle righe interessate. Ad esempio, un' **UPDATE** oppure **eliminare** istruzione.  
  
-   **Istruzioni Data Definition Language (DDL)** si tratta di istruzioni SQL che modificano la struttura del database. Ad esempio, **CREATE TABLE** oppure **DROP INDEX**.  
  
-   **Le istruzioni di modifica del contesto** si tratta di istruzioni SQL che modificano il contesto di un database. Ad esempio, il **utilizzo** e **impostare** le istruzioni in SQL Server.  
  
-   **Istruzioni amministrative** si tratta di istruzioni SQL utilizzate per scopi amministrativi in un database. Ad esempio, **concessione** e **REVOKE**.  
  
 Le istruzioni SQL nelle prime due categorie sono noti collettivamente come *istruzioni che generano risultati*. Istruzioni SQL in quest'ultime tre categorie sono noti collettivamente come *senza risultati istruzioni*. ODBC definisce la semantica di batch che includono istruzioni solo generazione di risultati. Questa semantica varia notevolmente e pertanto è specifiche dell'origine dati. Ad esempio, il driver SQL Server non supporta il trascinamento di un oggetto e quindi si fa riferimento a o ricreare lo stesso oggetto nello stesso batch. Pertanto, il termine *batch* quando usata in questo manuale si riferisce solo ai batch di generazione di risultati le istruzioni.
