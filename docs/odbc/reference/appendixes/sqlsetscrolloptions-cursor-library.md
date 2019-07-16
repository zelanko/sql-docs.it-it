---
title: SQLSetScrollOptions (libreria di cursori) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetScrollOptions function [ODBC], Cursor Library
ms.assetid: c5c0ac6d-a6c1-4077-8186-1644df1944f8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 18a0bc111f6b4e8d82d0ed353837b499f920479e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68023364"
---
# <a name="sqlsetscrolloptions-cursor-library"></a>SQLSetScrollOptions (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Microsoft consiglia di usare le funzionalità del driver del cursore.  
  
 In questo argomento viene illustrato l'utilizzo dei **SQLSetScrollOptions** funzione nella libreria di cursori. Per informazioni generali sul **SQLSetScrollOptions**, vedere [funzione SQLSetScrollOptions](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md).  
  
 Supporta la libreria di cursori **SQLSetScrollOptions** solo per compatibilità con le versioni precedenti; le applicazioni devono usare invece gli attributi di istruzione SQL_ATTR_CURSOR_TYPE, SQL_ATTR_CONCURRENCY e SQL_ATTR_ROW_ARRAY_SIZE.
