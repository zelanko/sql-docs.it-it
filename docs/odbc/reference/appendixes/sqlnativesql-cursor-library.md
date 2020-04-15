---
title: SQLNativeSql (libreria di cursori) . Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 41f7617530f34d49852ca67db9f47cab94292385
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300571"
---
# <a name="sqlnativesql-cursor-library"></a>SQLNativeSql (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità del cursore del driver.  
  
 In questo argomento viene illustrato l'utilizzo della funzione **SQLNativeSql** nella libreria di cursori. Per informazioni generali su **SQLNativeSql**, vedere [Funzione SQLNativeSql](../../../odbc/reference/syntax/sqlnativesql-function.md).  
  
 Se il driver supporta questa funzione, la libreria di cursori chiama **SQLNativeSql** nel driver e passa l'istruzione SQL. Per le istruzioni positioned update, positioned delete e **SELECT FOR UPDATE,** la libreria di cursori modifica l'istruzione prima di passarla al driver.  
  
> [!NOTE]  
>  La libreria di cursori restituisce erroneamente SQLSTATE 34000 (nome cursore non valido) se il nome del cursore non è valido in un'istruzione di aggiornamento o eliminazione posizionata che viene passata nell'argomento *InStatementText* di **SQLNativeSql**. **SQLNativeSql** non è destinato a restituire errori di sintassi, che vengono restituiti solo al momento della preparazione o dell'esecuzione dell'istruzione.
