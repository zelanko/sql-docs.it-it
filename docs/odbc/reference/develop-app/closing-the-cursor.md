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
ms.openlocfilehash: de22797bdcf4ff526a8c17aee313567da3114b60
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68036538"
---
# <a name="closing-the-cursor"></a>Chiusura del cursore
Al termine dell'utilizzo di un cursore da parte di un'applicazione, viene chiamato **SQLCloseCursor** per chiudere il cursore. Ad esempio:  
  
```  
SQLCloseCursor(hstmt);  
```  
  
 Fino a quando l'applicazione non chiude il cursore, non è possibile utilizzare l'istruzione in cui è aperto il cursore per la maggior parte delle altre operazioni, ad esempio l'esecuzione di un'altra istruzione SQL. Per un elenco completo di funzioni che possono essere chiamate mentre un cursore è aperto, vedere [Appendice B: tabelle di transizione dello stato ODBC](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md).  
  
> [!NOTE]  
>  Per chiudere un cursore, un'applicazione deve chiamare **SQLCloseCursor**, non **SQLCancel**.  
  
 I cursori rimangono aperti fino a quando non vengono chiusi in modo esplicito, tranne quando viene eseguito il commit o il rollback di una transazione, nel qual caso alcune origini dati chiudono il cursore. In particolare, se si raggiunge la fine del set di risultati, quando **SQLFetch** restituisce SQL_NO_DATA non chiude un cursore. Anche i cursori su set di risultati vuoti (set di risultati creati quando un'istruzione è stata eseguita correttamente ma che non hanno restituito righe) devono essere chiusi in modo esplicito.
