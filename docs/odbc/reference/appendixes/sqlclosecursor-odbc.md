---
title: SQLCloseCursor_ODBC . Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLCloseCursor function [ODBC], ODBC
ms.assetid: 5e47e3f7-e1b8-451f-bf75-daa19b7c7271
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e1b61267d093e11bf7ea25158f5dc6a29ccba6a1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296301"
---
# <a name="sqlclosecursor_odbc"></a>SQLCloseCursor_ODBC
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità del cursore del driver.  
  
 In questo argomento viene illustrato l'utilizzo della funzione **SQLCloseCursor** nella libreria di cursori. Per informazioni generali su **SQLCloseCursor**, vedere [Funzione SQLCloseCursor](../../../odbc/reference/syntax/sqlclosecursor-function.md).  
  
 La libreria di cursori non supporta la chiamata **a SQLCloseCursor** senza un cursore aperto. Se si tenta di eseguire questa operazione, verrà restituito SQLSTATE 24000 (stato del cursore non valido). La chiamata a **SQLFreeStmt** con *un'opzione* di SQL_CLOSE quando non è aperto alcun cursore è supportata dalla libreria di cursori.
