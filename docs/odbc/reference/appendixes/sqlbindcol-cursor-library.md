---
title: SQLBindCol (libreria di cursori) Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1c29909a96f147a0f5ebc2140a68072dfe544255
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305472"
---
# <a name="sqlbindcol-cursor-library"></a>SQLBindCol (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità del cursore del driver.  
  
 In questo argomento viene illustrato l'utilizzo della funzione **SQLBindCol** nella libreria di cursori. Per informazioni generali su **SQLBindCol**, vedere [Funzione SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
 Un'applicazione alloca uno o più buffer affinché la libreria di cursori restituisca il set di righe corrente. Chiama **SQLBindCol** una o più volte per associare questi buffer al set di risultati.  
  
 Un'applicazione può chiamare **SQLBindCol** per riassociare le colonne del set di risultati dopo aver chiamato **SQLExtendedFetch**, **SQLFetch**o **SQLFetchScroll**, purché il tipo di dati C, le dimensioni della colonna e le cifre decimali della colonna associata rimangano invariati. L'applicazione non deve chiudere il cursore per riassociare le colonne a indirizzi diversi.  
  
 La libreria di cursori supporta l'impostazione dell'attributo di istruzione SQL_ATTR_ROW_BIND_OFFSET_PTR per l'utilizzo di offset di associazione. **(SQLBindCol** non deve essere chiamato per questa riassociazione). Se la libreria di cursori viene utilizzata con un driver ODBC *3.x,* l'offset di associazione non viene utilizzato quando viene chiamato **SQLFetch.** L'offset di associazione viene utilizzato se **SQLFetch** viene chiamato quando la libreria di cursori viene utilizzata con un driver ODBC *2.x* perché **SQLFetch** viene quindi mappato a **SQLExtendedFetch**.  
  
 La libreria di cursori supporta la chiamata **di SQLBindCol** per associare la colonna del segnalibro.  
  
 Quando si utilizza un driver ODBC *2.x,* la libreria di cursori restituisce SQLSTATE HY090 (stringa non valida o lunghezza del buffer) quando **SQLBindCol** viene chiamato per impostare la lunghezza del buffer per una colonna del segnalibro su un valore diverso da 4. Quando si utilizza un driver ODBC *3.x,* la libreria di cursori consente al buffer di avere qualsiasi dimensione.
