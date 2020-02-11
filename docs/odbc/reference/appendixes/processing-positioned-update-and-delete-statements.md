---
title: Elaborazione delle istruzioni Update e Delete posizionate | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- positioned deletes [ODBC]
- ODBC cursor library [ODBC], statement processing
- cursor library [ODBC], positioned update or delete
- positioned updates [ODBC]
- SQL statements [ODBC], cursor library
- ODBC cursor library [ODBC], positioned update or delete
- cursor library [ODBC], statement processing
ms.assetid: 2975dd97-48e6-4d0a-a9c7-40759a7d94c8
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 41b4fe248f815e63c48a8da70edc88a1cc173667
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68028431"
---
# <a name="processing-positioned-update-and-delete-statements"></a>Elaborazione di istruzioni di eliminazione e aggiornamento posizionato
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità di cursore del driver.  
  
 La libreria di cursori supporta le istruzioni Update e Delete posizionate sostituendo la clausola **where current of** in tali istruzioni con una clausola **where** che enumera i valori archiviati nella cache per ogni colonna associata. La libreria di cursori passa le istruzioni **Update** e **Delete** appena costruite al driver per l'esecuzione. Per le istruzioni UPDATE posizionate, la libreria di cursori aggiorna la cache dai valori nei buffer dei set di righe e imposta il valore corrispondente nella matrice di stato della riga su SQL_ROW_UPDATED. Per le istruzioni DELETE posizionate, imposta il valore corrispondente nella matrice di stato della riga su SQL_ROW_DELETED.  
  
> [!CAUTION]  
>  La clausola **where** costruita dalla libreria di cursori per identificare la riga corrente può non essere in grado di identificare le righe, identificare una riga diversa o identificare più di una riga. Per ulteriori informazioni, vedere [creazione di istruzioni ricercate](../../../odbc/reference/appendixes/constructing-searched-statements.md), più avanti in questa appendice.  
  
 Le istruzioni Update e Delete posizionate sono soggette alle restrizioni seguenti:  
  
-   È possibile utilizzare le istruzioni Update e Delete posizionate solo nei casi seguenti: quando un'istruzione **Select** genera il set di risultati; Quando l'istruzione **Select** non contiene un join, una clausola **Union** o una clausola **Group by** ; e quando le colonne che usavano un alias o un'espressione nell'elenco di selezione non erano associate a **SQLBindCol**.  
  
-   Se un'applicazione prepara un'istruzione Update o DELETE posizionata, questa operazione deve essere eseguita dopo la chiamata a **SQLFetch** o **SQLFetchScroll**. Sebbene la libreria di cursori invii l'istruzione al driver per la preparazione, chiude l'istruzione e la esegue direttamente quando l'applicazione chiama **SQLExecute**.  
  
-   Se il driver supporta una sola istruzione attiva, tramite la libreria di cursori viene recuperato il resto del set di risultati, quindi il set di righe corrente viene recuperato dalla cache prima di eseguire un'istruzione Update o DELETE posizionata. Se l'applicazione chiama una funzione che restituisce metadati in un set di risultati, ad esempio **SQLNumResultCols** o **SQLDescribeCol**, la libreria di cursori restituisce un errore.  
  
-   Se un'istruzione Update o DELETE posizionata viene eseguita su una colonna di una tabella che include una colonna timestamp che viene aggiornata automaticamente ogni volta che viene eseguito un aggiornamento, tutte le istruzioni Update o DELETE posizionate successivamente avranno esito negativo se la colonna timestamp è associato. Questo problema si verifica perché l'istruzione di aggiornamento o eliminazione ricercata creata dalla libreria di cursori non identifica in modo accurato la riga da aggiornare. Il valore nell'istruzione cercato per la colonna timestamp non corrisponderà al valore aggiornato automaticamente della colonna timestamp.
