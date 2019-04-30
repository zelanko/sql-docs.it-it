---
title: SQLNativeSql (libreria di cursori) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLNativeSql function [ODBC], Cursor Library
ms.assetid: c4459092-1177-4b2a-b7f5-e0083d3bf2b2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c5b87f64963e7b0ad45fbec33e410165cd0c9723
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63298489"
---
# <a name="sqlnativesql-cursor-library"></a>SQLNativeSql (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Microsoft consiglia di usare le funzionalità del driver del cursore.  
  
 In questo argomento viene illustrato l'utilizzo dei **SQLNativeSql** funzione nella libreria di cursori. Per informazioni generali sul **SQLNativeSql**, vedere [funzione SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md).  
  
 Se il driver supporta questa funzione, chiama la libreria di cursori **SQLNativeSql** nel driver e lo passa l'istruzione SQL. Per un aggiornamento posizionato, posizionato delete, e **selezionare per aggiornare** (istruzioni), la libreria di cursori consente di modificare l'istruzione prima di passarlo al driver.  
  
> [!NOTE]  
>  La libreria di cursori restituisce erroneamente SQLSTATE 34000 (nome di cursore non valido) se il nome del cursore non è valido in un'istruzione delete che viene passato in o un aggiornamento posizionato il *InStatementText* argomento di **SQLNativeSql** . **SQLNativeSql** non è progettata per restituire gli errori di sintassi, che vengono restituiti solo al momento di preparazione dell'istruzione o dell'esecuzione.
