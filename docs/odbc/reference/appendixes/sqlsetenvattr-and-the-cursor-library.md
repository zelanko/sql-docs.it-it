---
title: SQLSetEnvAttr e la libreria di cursori | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetEnvAttr function [ODBC], Cursor Library
ms.assetid: 59cc8eae-09ae-4796-869a-c5806488ae83
author: MightyPen
ms.author: genemi
ms.openlocfilehash: db1608415ae74bcaafd89f4afe01393cfb700379
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125561"
---
# <a name="sqlsetenvattr-and-the-cursor-library"></a>SQLSetEnvAttr e la libreria di cursori
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Microsoft consiglia di usare le funzionalità del driver del cursore.  
  
 In questo argomento viene illustrato l'utilizzo dei **SQLSetEnvAttr** funzione con la libreria di cursori. Per informazioni generali sul **SQLSetEnvAttr**, vedere [SQLSetEnvAttr-funzione](../../../odbc/reference/syntax/sqlsetenvattr-function.md).  
  
 La libreria di cursori non è interessata dall'impostazione dell'attributo environment SQL_ATTR_ODBC_VERSION, indipendentemente dalla versione dell'applicazione o versione del driver.
