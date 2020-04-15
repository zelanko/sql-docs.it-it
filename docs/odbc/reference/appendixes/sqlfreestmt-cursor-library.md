---
title: SQLFreeStmt (Libreria cursore) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLFreeStmt function [ODBC], Cursor Library
ms.assetid: 47bfbd4d-9453-4609-958d-1e05794cb223
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d78075593926c15dbaeb1904603b08e990f64983
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302022"
---
# <a name="sqlfreestmt-cursor-library"></a>SQLFreeStmt (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità del cursore del driver.  
  
 In questo argomento viene illustrato l'utilizzo della funzione **SQLFreeStmt** nella libreria di cursori. Per informazioni generali su **SQLFreeStmt**, vedere [Funzione SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md).  
  
 Se un'applicazione chiama **SQLFreeStmt** con l'opzione SQL_UNBIND dopo aver chiamato **SQLExtendedFetch**, **SQLFetch**o **SQLFetchScroll**, la libreria di cursori restituisce un errore. Prima di poter annullare l'associazione delle colonne del set di risultati, un'applicazione deve chiamare **SQLCloseCursor** o **SQLFreeStmt** con l'opzione SQL_CLOSE.
