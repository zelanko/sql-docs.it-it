---
title: SQLCloseCursor_ODBC | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: a4d0f88d2d9eaba7d95ba887ffbe11e728320b17
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68123376"
---
# <a name="sqlclosecursor_odbc"></a>SQLCloseCursor_ODBC
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità di cursore del driver.  
  
 In questo argomento viene illustrato l'utilizzo della funzione **SQLCloseCursor** nella libreria di cursori. Per informazioni generali su **SQLCloseCursor**, vedere [funzione SQLCloseCursor](../../../odbc/reference/syntax/sqlclosecursor-function.md).  
  
 La libreria di cursori non supporta la chiamata a **SQLCloseCursor** senza un cursore aperto. Il tentativo di eseguire questa operazione restituirà SQLSTATE 24000 (stato del cursore non valido). La chiamata a **SQLFreeStmt** con un' *opzione* di SQL_CLOSE quando non è aperto alcun cursore è supportata dalla libreria di cursori.
