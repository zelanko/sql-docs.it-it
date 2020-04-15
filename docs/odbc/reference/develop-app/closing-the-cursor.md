---
title: Chiusura del Cursore Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 723e40e6d83eed84ed93ee1eeab3535622ad5f04
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299141"
---
# <a name="closing-the-cursor"></a>Chiusura del cursore
Quando un'applicazione ha terminato di utilizzare un cursore, chiama **SQLCloseCursor** per chiudere il cursore. Ad esempio:  
  
```  
SQLCloseCursor(hstmt);  
```  
  
 Finché l'applicazione non chiude il cursore, l'istruzione in cui viene aperto il cursore non può essere utilizzata per la maggior parte delle altre operazioni, ad esempio l'esecuzione di un'altra istruzione SQL. Per un elenco completo delle funzioni che possono essere chiamate mentre è aperto un cursore, vedere [Appendice B: Tabelle](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)di transizione dello stato ODBC .  
  
> [!NOTE]  
>  Per chiudere un cursore, un'applicazione deve chiamare **SQLCloseCursor**, non **SQLCancel**.  
  
 I cursori rimangono aperti fino a quando non vengono chiusi in modo esplicito, tranne quando viene eseguito il commit o il rollback di una transazione, nel qual caso alcune origini dati chiudono il cursore. In particolare, il raggiungimento della fine del set di risultati, quando **SQLFetch** restituisce SQL_NO_DATA, non chiude un cursore. Anche i cursori su set di risultati vuoti (set di risultati creati quando un'istruzione eseguita correttamente ma che non ha restituito alcuna riga) devono essere chiusi in modo esplicito.
