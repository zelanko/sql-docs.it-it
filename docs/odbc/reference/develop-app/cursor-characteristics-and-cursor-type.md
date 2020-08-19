---
description: Caratteristiche e tipo di cursore
title: Caratteristiche del cursore e tipo di cursore | Microsoft Docs
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
ms.openlocfilehash: 10ec9c7fc42ad20ce0a5a6d70ef4a2a692afbec3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429423"
---
# <a name="cursor-characteristics-and-cursor-type"></a>Caratteristiche e tipo di cursore
Un'applicazione può specificare le caratteristiche di un cursore invece di specificare il tipo di cursore (di tipo solo di tipo di cursore, statico, gestito da keyset o dinamico). A tale scopo, l'applicazione seleziona lo scorrimento del cursore (impostando l'attributo dell'istruzione SQL_ATTR_CURSOR_SCROLLABLE) e la sensibilità (impostando l'attributo dell'istruzione SQL_ATTR_CURSOR_SENSITIVITY) prima di aprire il cursore nell'handle dell'istruzione. Il driver sceglie quindi il tipo di cursore che fornisce in modo più efficiente le caratteristiche richieste dall'applicazione.  
  
 Ogni volta che un'applicazione imposta uno degli attributi di istruzione SQL_ATTR_CONCURRENCY, SQL_ATTR_CURSOR_SCROLLABLE, SQL_ATTR_CURSOR_SENSITIVITY o SQL_ATTR_CURSOR_TYPE, il driver apporta tutte le modifiche necessarie agli altri attributi di istruzione in questo set di quattro attributi, in modo che i relativi valori rimangano coerenti. Di conseguenza, quando l'applicazione specifica una caratteristica del cursore, il driver può modificare l'attributo che indica il tipo di cursore in base a questa selezione implicita; Quando l'applicazione specifica un tipo, il driver può modificare gli altri attributi in modo che siano coerenti con le caratteristiche del tipo selezionato. Per ulteriori informazioni su questi attributi di istruzione, vedere la descrizione della funzione [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md) .  
  
 Un'applicazione che imposta gli attributi dell'istruzione per specificare sia un tipo di cursore che le caratteristiche del cursore esegue il rischio di ottenere un cursore che non è il metodo più efficiente disponibile su tale driver per soddisfare i requisiti dell'applicazione.  
  
 L'impostazione implicita degli attributi di istruzione è definita dal driver, ad eccezione del fatto che deve rispettare le regole seguenti:  
  
-   I cursori di sola trasmissione non sono mai scorrevoli; vedere la definizione di SQL_ATTR_CURSOR_SCROLLABLE in [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
-   I cursori non sensibili non sono mai aggiornabili e pertanto la loro concorrenza è di sola lettura. Questa operazione si basa sulla definizione di cursori non sensibili nello standard ISO SQL.  
  
 Di conseguenza, l'impostazione implicita degli attributi di istruzione si verifica nei casi descritti nella tabella seguente.  
  
|L'applicazione imposta l'attributo su|Altri attributi impostati in modo implicito|  
|-----------------------------------|-------------------------------------|  
|SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY|SQL_ATTR_CURSOR_SENSITIVITY SQL_INSENSITIVE.|  
|SQL_ATTR_CONCURRENCY SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER o SQL_CONCUR_VALUES|SQL_ATTR_CURSOR_SENSITIVITY SQL_UNSPECIFIED o SQL_SENSITIVE, in base a quanto definito dal driver. Non può mai essere impostato su SQL_INSENSITIVE, perché i cursori non sensibili sono sempre di sola lettura.|  
|SQL_ATTR_CURSOR_SCROLLABLE SQL_NONSCROLLABLE|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY|  
|SQL_ATTR_CURSOR_SCROLLABLE SQL_SCROLLABLE|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN o SQL_CURSOR_DYNAMIC, come specificato dal driver. Non viene mai impostata su SQL_CURSOR_FORWARD_ONLY.|  
|SQL_ATTR_CURSOR_SENSITIVITY SQL_INSENSITIVE|SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY.<br /><br /> SQL_ATTR_CURSOR_TYPE SQL_CURSOR_STATIC.|  
|SQL_ATTR_CURSOR_SENSITIVITY SQL_SENSITIVE|SQL_ATTR_CONCURRENCY SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER o SQL_CONCUR_VALUES, come specificato dal driver. Non viene mai impostata su SQL_CONCUR_READ_ONLY.<br /><br /> SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY, SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN o SQL_CURSOR_DYNAMIC, come specificato dal driver.|  
|SQL_ATTR_CURSOR_SENSITIVITY SQL_UNSPECIFIED|SQL_ATTR_CONCURRENCY SQL_CONCUR_READ_ONLY, SQL_CONCUR_LOCK, SQL_CONCUR_ROWVER o SQL_CONCUR_VALUES, come specificato dal driver.<br /><br /> SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY, SQL_CURSOR_STATIC, SQL_CURSOR_KEYSET_DRIVEN o SQL_CURSOR_DYNAMIC, come specificato dal driver.|  
|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_DYNAMIC|SQL_ATTR_SCROLLABLE SQL_SCROLLABLE.<br /><br /> SQL_ATTR_CURSOR_SENSITIVITY SQL_SENSITIVE. (Ma solo se SQL_ATTR_CONCURRENCY non è uguale a SQL_CONCUR_READ_ONLY. I cursori dinamici aggiornabili sono sempre sensibili alle modifiche apportate alla propria transazione.|  
|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_FORWARD_ONLY|SQL_ATTR_CURSOR_SCROLLABLE SQL_NONSCROLLABLE.|  
|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_KEYSET_DRIVEN|SQL_ATTR_SCROLLABLE SQL_SCROLLABLE.<br /><br /> SQL_ATTR_SENSITIVITY SQL_UNSPECIFIED o SQL_SENSITIVE (in base ai criteri definiti dal driver, se SQL_ATTR_CONCURRENCY non è SQL_CONCUR_READ_ONLY).|  
|SQL_ATTR_CURSOR_TYPE SQL_CURSOR_STATIC|SQL_ATTR_SCROLLABLE SQL_SCROLLABLE.<br /><br /> SQL_ATTR_SENSITIVITY SQL_INSENSITIVE (se SQL_ATTR_CONCURRENCY è SQL_CONCUR_READ_ONLY).<br /><br /> SQL_ATTR_SENSITIVITY SQL_UNSPECIFIED o SQL_SENSITIVE (se SQL_ATTR_CONCURRENCY non è SQL_CONCUR_READ_ONLY).|
