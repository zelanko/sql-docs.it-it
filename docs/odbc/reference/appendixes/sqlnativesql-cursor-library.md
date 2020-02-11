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
ms.openlocfilehash: 0a8c42efbd87296cf7157d75d1848e4655247818
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68125707"
---
# <a name="sqlnativesql-cursor-library"></a>SQLNativeSql (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità di cursore del driver.  
  
 In questo argomento viene illustrato l'utilizzo della funzione **SQLNativeSql** nella libreria di cursori. Per informazioni generali su **SQLNativeSql**, vedere [funzione SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md).  
  
 Se il driver supporta questa funzione, la libreria di cursori chiama **SQLNativeSql** nel driver e la passa all'istruzione SQL. Per gli aggiornamenti posizionati, le istruzioni DELETE posizionate e **Select for Update** , la libreria di cursori modifica l'istruzione prima di passarla al driver.  
  
> [!NOTE]  
>  La libreria di cursori restituisce erroneamente SQLSTATE 34000 (nome di cursore non valido) se il nome del cursore non è valido in un'istruzione Update o DELETE posizionata passata nell'argomento *InStatementText* di **SQLNativeSql**. **SQLNativeSql** non è progettato per restituire errori di sintassi, che vengono restituiti solo dopo la preparazione o l'esecuzione di istruzioni.
