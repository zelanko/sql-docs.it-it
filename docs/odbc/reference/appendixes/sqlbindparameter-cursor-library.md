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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7943987d52554e0f5cd7723e8c9ae8a0e3afddd2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093032"
---
# <a name="sqlbindparameter-cursor-library"></a>SQLBindParameter (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Microsoft consiglia di usare le funzionalità del driver del cursore.  
  
 In questo argomento viene illustrato l'utilizzo dei **SQLBindParameter** funzione nella libreria di cursori. Per informazioni generali sul **SQLBindParameter**, vedere [funzione SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md).  
  
 Un'applicazione può chiamare **SQLBindParameter** per riassociare i parametri, purché il tipo di dati C, le dimensioni di colonna e cifre decimali della colonna associata rimangono invariati.  
  
 La libreria di cursori supporta l'impostazione dell'attributo di istruzione SQL_ATTR_ROW_BIND_OFFSET_PTR usare gli offset di associazione. (**SQLBindParameter** non deve essere chiamato per questo che si verifichi la riassociazione.)  
  
 La libreria di cursori supporta i parametri data-at-execution di associazione.
