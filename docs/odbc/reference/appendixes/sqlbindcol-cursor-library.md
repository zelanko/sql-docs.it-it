---
title: SQLBindCol (libreria di cursori) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLAllocStmt function [ODBC], Cursor Library
ms.assetid: f4dd546a-0a6c-4397-8ee7-fafa6b9da543
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e9e1018754977ee73ecdc21db30b3d8c2aae8b4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63199689"
---
# <a name="sqlbindcol-cursor-library"></a>SQLBindCol (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Microsoft consiglia di usare le funzionalità del driver del cursore.  
  
 In questo argomento viene illustrato l'utilizzo dei **SQLBindCol** funzione nella libreria di cursori. Per informazioni generali sul **SQLBindCol**, vedere [funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
 Un'applicazione alloca i buffer per la libreria di cursori restituire il set di righe corrente in uno o più. Viene chiamato **SQLBindCol** una o più volte per associare tali buffer al set di risultati.  
  
 Un'applicazione può chiamare **SQLBindCol** riassociare risultato set di colonne dopo aver chiamato **SQLExtendedFetch**, **SQLFetch**, o **SQLFetchScroll**, purché il tipo di dati C, le dimensioni di colonna e cifre decimali della colonna associata rimangono invariati. L'applicazione non necessario chiudere il cursore per la riassociazione delle colonne a indirizzi diversi.  
  
 La libreria di cursori supporta l'impostazione dell'attributo di istruzione SQL_ATTR_ROW_BIND_OFFSET_PTR usare gli offset di associazione. (**SQLBindCol** non deve essere chiamato per questo che si verifichi la riassociazione.) Se la libreria di cursori viene usata con un'applicazione ODBC 3 *. x* driver, l'offset di binding non è utilizzato quando **SQLFetch** viene chiamato. L'offset di binding viene usato se **SQLFetch** viene chiamato quando viene usata la libreria di cursori con un'API ODBC 2. *x* driver poiché **SQLFetch** viene quindi mappato a **SQLExtendedFetch**.  
  
 La libreria di cursori supporta la chiamata **SQLBindCol** per associare la colonna del segnalibro.  
  
 Quando si lavora con un'API ODBC 2. *x* driver, la libreria di cursori restituisce SQLSTATE HY090 (stringa di lunghezza o non valida del buffer) quando **SQLBindCol** viene chiamato per impostare la lunghezza del buffer per una colonna del segnalibro a un valore non è uguale a 4. Quando si lavora con un'applicazione ODBC 3*x* driver, la libreria di cursori consente il buffer essere di qualsiasi dimensione.
