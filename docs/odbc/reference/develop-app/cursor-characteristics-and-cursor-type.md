---
title: Caratteristiche del cursore e tipo di cursore Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
- cursors [ODBC], creating
ms.assetid: 6f67edd2-ae71-4ca0-9b2d-abf4c20dc17b
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8354fdabf6830780ec2d128492c86cc1edd582ac
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301628"
---
# <a name="cursor-characteristics-and-cursor-type"></a>Caratteristiche e tipo di cursore
Un'applicazione può specificare le caratteristiche di un cursore anziché specificare il tipo di cursore (forward-only, static, keyset-driven o dynamic). A tale scopo, l'applicazione seleziona la scorrevolezza del cursore (impostando l'attributo di istruzione SQL_ATTR_CURSOR_SCROLLABLE) e la sensibilità (impostando l'attributo di istruzione SQL_ATTR_CURSOR_SENSITIVITY) prima di aprire il cursore sull'handle dell'istruzione. Il driver sceglie quindi il tipo di cursore che fornisce in modo più efficiente le caratteristiche richieste dall'applicazione.  
  
 Ogni volta che un'applicazione imposta uno degli attributi dell'istruzione SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_SCROLLABLE, SQL_ATTR_CURSOR_SENSITIVITY o SQL_ATTR_CURSOR_TYPE, il driver apporta qualsiasi modifica necessaria agli altri attributi dell'istruzione in questo set di quattro attributi in modo che i relativi valori rimangano coerenti. Di conseguenza, quando l'applicazione specifica una caratteristica del cursore, il driver può modificare l'attributo che indica il tipo di cursore in base a questa selezione implicita; Quando l'applicazione specifica un tipo, il driver può modificare qualsiasi altro attributo in modo che sia coerente con le caratteristiche del tipo selezionato. Per altre informazioni su questi attributi dell'istruzione, vedere la descrizione della funzione [SQLSetStmtAttr.For](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) more information about these statement attributes, see the SQLSetStmtAttr function description.  
  
 Un'applicazione che imposta gli attributi dell'istruzione per specificare sia il tipo di cursore che le caratteristiche del cursore corre il rischio di ottenere un cursore che non è il metodo più efficiente disponibile su tale driver per soddisfare i requisiti dell'applicazione.  
  
 L'impostazione implicita degli attributi di istruzione è definita dal driver, ad eccezione del fatto che deve seguire queste regole:The implicit setting of statement attributes is driver-defined driver-defined except that it must follow these rules:  
  
-   I cursori forward-only non sono mai scorrevoli; vedere la definizione di SQL_ATTR_CURSOR_SCROLLABLE in [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
-   I cursori non sensibili non sono mai aggiornabili e pertanto la concorrenza è di sola lettura. questo si basa sulla loro definizione di cursori insensibili nello standard ISO SQL.  
  
 Di conseguenza, l'impostazione implicita degli attributi di istruzione si verifica nei casi descritti nella tabella seguente.  
  
|Attributo set di applicazioni su|Altri attributi impostati in modo implicito|  
|-----------------------------------|-------------------------------------|  
|SQL_ATTR_CONCURRENCY per SQL_CONCUR_READ_ONLY|SQL_ATTR_CURSOR_SENSITIVITY to SQL_INSENSITIVE.|  
|SQL_ATTR_CONCURRENCY a SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER o SQL_CONCUR_VALUES|SQL_ATTR_CURSOR_SENSITIVITY per SQL_UNSPECIFIED o SQL_SENSITIVE, come definito dal driver. Non può mai essere impostato su SQL_INSENSITIVE, perché i cursori insensibili sono sempre di sola lettura.|  
|SQL_ATTR_CURSOR_SCROLLABLE a SQL_NONSCROLLABLE|SQL_ATTR_CURSOR_TYPE per SQL_CURSOR_FORWARD_ONLY|  
|SQL_ATTR_CURSOR_SCROLLABLE a SQL_SCROLLABLE|SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN o SQL_CURSOR_DYNAMIC, come specificato dal driver. Non è mai impostato per SQL_CURSOR_FORWARD_ONLY.|  
|SQL_ATTR_CURSOR_SENSITIVITY a SQL_INSENSITIVE|SQL_ATTR_CONCURRENCY a SQL_CONCUR_READ_ONLY.<br /><br /> SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_STATIC.|  
|SQL_ATTR_CURSOR_SENSITIVITY a SQL_SENSITIVE|SQL_ATTR_CONCURRENCY per SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER o SQL_CONCUR_VALUES, come specificato dal driver. Non è mai impostato per SQL_CONCUR_READ_ONLY.<br /><br /> SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_FORWARD_ONLY, SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN o SQL_CURSOR_DYNAMIC, come specificato dal driver.|  
|SQL_ATTR_CURSOR_SENSITIVITY per SQL_UNSPECIFIED|SQL_ATTR_CONCURRENCY a SQL_CONCUR_READ_ONLY, SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER o SQL_CONCUR_VALUES, come specificato dal driver.<br /><br /> SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_FORWARD_ONLY, SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN o SQL_CURSOR_DYNAMIC, come specificato dal driver.|  
|SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_DYNAMIC|SQL_ATTR_SCROLLABLE a SQL_SCROLLABLE.<br /><br /> da SQL_ATTR_CURSOR_SENSITIVITY a SQL_SENSITIVE. (Ma solo se SQL_ATTR_CONCURRENCY non è uguale a SQL_CONCUR_READ_ONLY. I cursori dinamici aggiornabili sono sempre sensibili alle modifiche apportate nella propria transazione.)|  
|SQL_ATTR_CURSOR_TYPE per SQL_CURSOR_FORWARD_ONLY|SQL_ATTR_CURSOR_SCROLLABLE di SQL_NONSCROLLABLE.|  
|SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_KEYSET_DRIVEN|SQL_ATTR_SCROLLABLE a SQL_SCROLLABLE.<br /><br /> SQL_ATTR_SENSITIVITY SQL_UNSPECIFIED o SQL_SENSITIVE (in base a criteri definiti dal driver, se non SQL_ATTR_CONCURRENCY è SQL_CONCUR_READ_ONLY).|  
|SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_STATIC|SQL_ATTR_SCROLLABLE a SQL_SCROLLABLE.<br /><br /> SQL_ATTR_SENSITIVITY a SQL_INSENSITIVE (se SQL_ATTR_CONCURRENCY è SQL_CONCUR_READ_ONLY).<br /><br /> SQL_ATTR_SENSITIVITY a SQL_UNSPECIFIED o SQL_SENSITIVE (se SQL_ATTR_CONCURRENCY non è SQL_CONCUR_READ_ONLY).|
