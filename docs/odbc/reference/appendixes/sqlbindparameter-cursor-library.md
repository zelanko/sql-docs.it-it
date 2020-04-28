---
title: SQLBindParameter (libreria di cursori) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBindParameter function [ODBC], Cursor Library
ms.assetid: 04c53e4c-cd1d-40b2-9997-684ebe43499f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 55708cc5192fb40149d6db7710f6ee638c4880d2
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305429"
---
# <a name="sqlbindparameter-cursor-library"></a>SQLBindParameter (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità di cursore del driver.  
  
 In questo argomento viene illustrato l'utilizzo della funzione **SQLBindParameter** nella libreria di cursori. Per informazioni generali su **SQLBindParameter**, vedere [funzione SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md).  
  
 Un'applicazione può chiamare **SQLBindParameter** per riassociare i parametri, purché il tipo di dati C, le dimensioni della colonna e le cifre decimali della colonna associata rimangano invariati.  
  
 La libreria di cursori supporta l'impostazione dell'attributo SQL_ATTR_ROW_BIND_OFFSET_PTR Statement per l'utilizzo degli offset di binding. Non è necessario chiamare**SQLBindParameter** per eseguire questa operazione di riassociazione.  
  
 La libreria di cursori supporta l'associazione di parametri data-at-execution.
