---
description: SQLSetEnvAttr e la libreria di cursori
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 97751c4735ed7357b87a3b50df5f116f7bb38c7d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476933"
---
# <a name="sqlsetenvattr-and-the-cursor-library"></a>SQLSetEnvAttr e la libreria di cursori
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità di cursore del driver.  
  
 In questo argomento viene illustrato l'utilizzo della funzione **SQLSetEnvAttr** con la libreria di cursori. Per informazioni generali su **SQLSetEnvAttr**, vedere [funzione SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md).  
  
 La libreria di cursori non è interessata dall'impostazione dell'attributo SQL_ATTR_ODBC_VERSION Environment, indipendentemente dalla versione dell'applicazione o dal driver.
