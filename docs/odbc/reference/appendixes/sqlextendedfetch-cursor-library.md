---
title: SQLExtendedFetch (libreria di cursori) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLExtendedFetch function [ODBC], Cursor Library
ms.assetid: 06fbf06f-127b-475c-b636-7b784918475d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fe39b2d2cbbaf72ce3844c35187040589d1dac58
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302062"
---
# <a name="sqlextendedfetch-cursor-library"></a>SQLExtendedFetch (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità del cursore del driver.  
  
 In questo argomento viene illustrato l'utilizzo della funzione **SQLExtendedFetch** nella libreria di cursori. Per informazioni generali su **SQLExtendedFetch**, vedere [Funzione SQLExtendedFetch](../../../odbc/reference/syntax/sqlextendedfetch-function.md).  
  
 La libreria di cursori implementa **SQLExtendedFetch** chiamando ripetutamente **SQLFetch** nel driver.  
  
 La libreria di cursori supporta la chiamata **SQLExtendedFetch** con un *FetchOrientation* di SQL_FETCH_BOOKMARK.  
  
 Quando viene utilizzata la libreria di cursori , le chiamate a **SQLExtendedFetch** non possono essere mescolate con chiamate a **SQLFetchScroll** o **SQLFetch .**
