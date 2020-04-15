---
title: Elaborazione di istruzioni di aggiornamento ed eliminazione con posizione Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4b3f20da018bcd4e28e8ffca097fb5a4373d7f42
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81308022"
---
# <a name="processing-positioned-update-and-delete-statements"></a>Elaborazione di istruzioni di eliminazione e aggiornamento posizionato
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità del cursore del driver.  
  
 La libreria di cursori supporta le istruzioni di aggiornamento ed eliminazione posizionate sostituendo la clausola **WHERE CURRENT OF** in tali istruzioni con una clausola **WHERE** che enumera i valori archiviati nella cache per ogni colonna associata. La libreria di cursori passa le istruzioni **UPDATE** e **DELETE** appena costruite al driver per l'esecuzione. Per le istruzioni di aggiornamento posizionate, la libreria di cursori aggiorna quindi la cache dai valori nei buffer del set di righe e imposta il valore corrispondente nella matrice di stato della riga su SQL_ROW_UPDATED. Per le istruzioni delete posizionate, imposta il valore corrispondente nella matrice di stato della riga su SQL_ROW_DELETED.  
  
> [!CAUTION]  
>  La clausola **WHERE** costruita dalla libreria di cursori per identificare la riga corrente può non riuscire a identificare righe, identificare una riga diversa o identificare più di una riga. Per ulteriori informazioni, vedere [Costruzione di istruzioni ricercate](../../../odbc/reference/appendixes/constructing-searched-statements.md)più avanti in questa appendice.  
  
 Le istruzioni di aggiornamento ed eliminazione posizionate sono soggette alle seguenti restrizioni:  
  
-   Le istruzioni di aggiornamento ed eliminazione posizionate possono essere utilizzate solo nei casi seguenti: quando un'istruzione **SELECT** ha generato il set di risultati; quando l'istruzione **SELECT** non contiene un join, una clausola **UNION** o una clausola **GROUP BY;** e quando le colonne che utilizzavano un alias o un'espressione nell'elenco di selezione non sono state associate a **SQLBindCol**.  
  
-   Se un'applicazione prepara un'istruzione di aggiornamento o eliminazione posizionata, deve farlo dopo aver chiamato **SQLFetch** o **SQLFetchScroll**. Sebbene la libreria di cursori invii l'istruzione al driver per la preparazione, chiude l'istruzione e la esegue direttamente quando l'applicazione chiama **SQLExecute**.  
  
-   Se il driver supporta una sola istruzione attiva, la libreria di cursori recupera il resto del set di risultati e quindi recupera nuovamente il set di righe corrente dalla cache prima di eseguire un'istruzione di aggiornamento o eliminazione posizionata. Se l'applicazione chiama quindi una funzione che restituisce metadati in un set di risultati (ad esempio, **SQLNumResultCols** o **SQLDescribeCol**), la libreria di cursori restituisce un errore.  
  
-   Se un'istruzione di aggiornamento o eliminazione posizionata viene eseguita su una colonna di una tabella che include una colonna timestamp che viene aggiornata automaticamente ogni volta che viene eseguito un aggiornamento, tutte le istruzioni di aggiornamento o eliminazione posizionate successive avranno esito negativo se la colonna timestamp è associata. Ciò si verifica perché l'istruzione di aggiornamento o eliminazione ricercata creata dalla libreria di cursori non identificherà in modo accurato la riga da aggiornare. Il valore nell'istruzione cercata per la colonna timestamp non corrisponderà al valore aggiornato automaticamente della colonna timestamp.
