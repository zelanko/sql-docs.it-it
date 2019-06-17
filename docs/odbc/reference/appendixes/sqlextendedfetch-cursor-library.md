---
title: SQLExtendedFetch (libreria di cursori) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 600d90c14ae8b08a4860f3cff49c1615a9587063
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199522"
---
# <a name="sqlextendedfetch-cursor-library"></a>SQLExtendedFetch (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Microsoft consiglia di usare le funzionalità del driver del cursore.  
  
 In questo argomento viene illustrato l'utilizzo dei **SQLExtendedFetch** funzione nella libreria di cursori. Per informazioni generali sul **SQLExtendedFetch**, vedere [funzione SQLExtendedFetch](../../../odbc/reference/syntax/sqlextendedfetch-function.md).  
  
 La libreria di cursori implementa **SQLExtendedFetch** chiamando ripetutamente **SQLFetch** nel driver.  
  
 La libreria di cursori supporta la chiamata **SQLExtendedFetch** con un *FetchOrientation* impostato su sql_fetch_bookmark.  
  
 Quando viene usata la libreria di cursori, le chiamate a **SQLExtendedFetch** ReadContentAsBase64 e ReadContentAsBinHex con chiamate a uno **SQLFetchScroll** oppure **SQLFetch**.
