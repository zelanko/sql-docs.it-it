---
title: Caratteristiche del cursore e il tipo di cursore | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e8803e7827102f564be63454b0387df938064d84
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68002050"
---
# <a name="cursor-characteristics-and-cursor-type"></a>Caratteristiche e tipo di cursore
Un'applicazione può specificare le caratteristiche di un cursore anziché specificare il tipo di cursore (forward-only, statico, gestito da keyset o dinamico). A tale scopo, l'applicazione seleziona scorrimento del cursore (impostando l'attributo di istruzione SQL_ATTR_CURSOR_SCROLLABLE) e sensibilità (impostando l'attributo di istruzione SQL_ATTR_CURSOR_SENSITIVITY) prima dell'apertura del cursore nell'istruzione handle. Il driver quindi sceglie il tipo di cursore in modo più efficiente fornisce le caratteristiche che l'applicazione ha richiesto.  
  
 Ogni volta che un'applicazione imposta uno degli attributi di istruzione SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_SCROLLABLE, SQL_ATTR_CURSOR_SENSITIVITY o SQL_ATTR_CURSOR_TYPE, il driver stabilisce automaticamente qualsiasi modifica necessaria per gli altri attributi di istruzione in questa serie quattro attributi in modo che i relativi valori rimangono coerenti. Di conseguenza, quando l'applicazione specifica una caratteristica di cursore, il driver può modificare l'attributo che indica il tipo di cursore basato su questa selezione implicita; Quando l'applicazione specifica un tipo, il driver può modificare uno degli altri attributi siano coerenti con le caratteristiche del tipo selezionato. Per altre informazioni su questi attributi di istruzione, vedere la [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) descrizione della funzione.  
  
 Il rischio di acquisizione di un cursore che non è il metodo più efficiente disponibile in tale driver di soddisfare i requisiti dell'applicazione viene eseguita un'applicazione che imposta gli attributi di istruzione per specificare un tipo di cursore e delle caratteristiche del cursore.  
  
 L'impostazione implicita di attributi di istruzione è definito dal driver ad eccezione del fatto che devono rispettare queste regole:  
  
-   I cursori forward-only non sono mai supporta lo scorrimento. visualizzare la definizione in SQL_ATTR_CURSOR_SCROLLABLE [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
-   I cursori INSENSITIVE non sono mai aggiornabili (e pertanto la concorrenza è di sola lettura); si basa sulla loro definizione di cursori insensitive in standard SQL ISO.  
  
 Di conseguenza, l'impostazione implicita di attributi di istruzione si verifica nei casi descritti nella tabella seguente.  
  
|Applicazione imposta attributo|Altri attributi impostati in modo implicito|  
|-----------------------------------|-------------------------------------|  
|SQL_ATTR_CONCURRENCY a SQL_CONCUR_READ_ONLY|SQL_ATTR_CURSOR_SENSITIVITY su SQL_INSENSITIVE.|  
|SQL_ATTR_CONCURRENCY agli SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER, SQL_CONCUR_VALUES|SQL_ATTR_CURSOR_SENSITIVITY SQL_UNSPECIFIED o SQL_SENSITIVE, come definito dal driver. Non si può mai essere impostato su SQL_INSENSITIVE, perché indipendenti dalla lingua sono sempre di sola lettura.|  
|SQL_ATTR_CURSOR_SCROLLABLE su SQL_NONSCROLLABLE|SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_FORWARD_ONLY|  
|SQL_ATTR_CURSOR_SCROLLABLE su SQL_SCROLLABLE|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN o SQL_CURSOR_DYNAMIC, come specificato dal driver. Non impostarlo su SQL_CURSOR_FORWARD_ONLY mai.|  
|SQL_ATTR_CURSOR_SENSITIVITY su SQL_INSENSITIVE|SQL_ATTR_CONCURRENCY a SQL_CONCUR_READ_ONLY.<br /><br /> SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_STATIC.|  
|SQL_ATTR_CURSOR_SENSITIVITY su SQL_SENSITIVE|SQL_ATTR_CONCURRENCY SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER o SQL_CONCUR_VALUES, come specificato dal driver. Non impostarlo su SQL_CONCUR_READ_ONLY mai.<br /><br /> SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY, SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN o SQL_CURSOR_DYNAMIC, come specificato dal driver.|  
|SQL_ATTR_CURSOR_SENSITIVITY a SQL_UNSPECIFIED|SQL_ATTR_CONCURRENCY su SQL_CONCUR_READ_ONLY, SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER o SQL_CONCUR_VALUES, come specificato dal driver.<br /><br /> SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY, SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN o SQL_CURSOR_DYNAMIC, come specificato dal driver.|  
|SQL_ATTR_CURSOR_TYPE to SQL_CURSOR_DYNAMIC|SQL_ATTR_SCROLLABLE su SQL_SCROLLABLE.<br /><br /> SQL_ATTR_CURSOR_SENSITIVITY su SQL_SENSITIVE. (Ma solo se non è uguale a SQL_CONCUR_READ_ONLY SQL_ATTR_CONCURRENCY. I cursori dinamici aggiornabili sono sempre sensibili alle modifiche apportate nella propria transazione.)|  
|SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_FORWARD_ONLY|SQL_ATTR_CURSOR_SCROLLABLE su SQL_NONSCROLLABLE.|  
|SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_KEYSET_DRIVEN|SQL_ATTR_SCROLLABLE su SQL_SCROLLABLE.<br /><br /> SQL_ATTR_SENSITIVITY SQL_UNSPECIFIED o SQL_SENSITIVE (in base al driver criteri definiti, se SQL_ATTR_CONCURRENCY non SQL_CONCUR_READ_ONLY).|  
|SQL_ATTR_CURSOR_TYPE a SQL_CURSOR_STATIC|SQL_ATTR_SCROLLABLE su SQL_SCROLLABLE.<br /><br /> SQL_ATTR_SENSITIVITY su SQL_INSENSITIVE (se SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY).<br /><br /> SQL_ATTR_SENSITIVITY SQL_UNSPECIFIED o SQL_SENSITIVE (se SQL_ATTR_CONCURRENCY non SQL_CONCUR_READ_ONLY).|
