---
title: SQLFetch (libreria di cursori) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFetch function [ODBC], Cursor Library
ms.assetid: 35a0d493-778b-4fb1-84ee-a13540e2fe0e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bee83ccb5497888b57a45673599af6b92931a704
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298721"
---
# <a name="sqlfetch-cursor-library"></a>SQLFetch (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità del cursore del driver.  
  
 In questo argomento viene illustrato l'utilizzo della funzione **SQLFetch** nella libreria di cursori. Per informazioni generali su **SQLFetch**, vedere [Funzione SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
 Quando viene utilizzata la libreria di cursori , le chiamate a **SQLFetch** non possono essere mescolate con chiamate a **SQLFetchScroll** o **SQLExtendedFetch**.  
  
 Se **SQLFetch** viene chiamato con SQL_ATTR_ROW_ARRAY_SIZE impostato su un valore maggiore di 1, la libreria di cursori passerà la chiamata al driver. Se il driver è un ODBC 2. *x* driver, la dimensione del set di righe verrà ignorata e la chiamata a **SQLFetch** restituirà una singola riga di dati.  
  
 Se la libreria di cursori viene utilizzata con un ODBC 2. *x* driver, un offset di associazione (come definito dall'attributo di istruzione SQL_ATTR_ROW_BIND_OFFSET_PTR) non viene utilizzato quando **SQLFetch** viene chiamato.  
  
 Quando viene caricata la libreria di cursori, un'applicazione non può chiamare **SQLFetch** per recuperare le colonne del segnalibro. La libreria di cursori passa la chiamata a **SQLFetch** tramite il driver, ma le chiamate di funzione per abilitare i segnalibri e associare la colonna del segnalibro vengono intercettate dalla libreria di cursori.
