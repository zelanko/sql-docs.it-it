---
title: Chiusura del cursore | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- cursors [ODBC], closing
- closing cursors [ODBC]
ms.assetid: 4f19bf5e-6d8c-40ae-a975-cfd62a0790ec
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 632a922abb544a379892dfa168f55efd605304c8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63125437"
---
# <a name="closing-the-cursor"></a>Chiusura del cursore
Quando un'applicazione ha terminato di utilizzare un cursore, chiama **SQLCloseCursor** per chiudere il cursore. Ad esempio:  
  
```  
SQLCloseCursor(hstmt);  
```  
  
 Fino a quando l'applicazione chiude il cursore, l'istruzione in cui viene aperto il cursore non è utilizzabile per la maggior parte delle altre operazioni, ad esempio l'esecuzione di un'altra istruzione SQL. Per un elenco completo delle funzioni che possono essere chiamate quando un cursore è aperto, vedere [appendice b: Tabelle della transizione di stato ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
> [!NOTE]  
>  Per chiudere un cursore, un'applicazione deve chiamare **SQLCloseCursor**, non **SQLCancel**.  
  
 I cursori rimangono aperti fino a quando non sono chiuse in modo esplicito, ad eccezione del fatto quando una transazione viene eseguito il commit o rollback, nel qual caso alcune origini dati chiudere il cursore. In particolare, il raggiungimento della fine del risultato impostato, quando **SQLFetch** restituisce SQL_NO_DATA, non si chiude un cursore. I cursori anche nei set di risultati vuoto (set di risultati creati durante un'istruzione eseguita correttamente, ma che non ha restituito righe) devono essere chiuso in modo esplicito.
