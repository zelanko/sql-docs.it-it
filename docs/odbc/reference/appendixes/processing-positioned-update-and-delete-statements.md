---
title: Elaborazione posizionato istruzioni Update e Delete | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: d898fcc7d1b35230173afa0443219d59c54720ae
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63057074"
---
# <a name="processing-positioned-update-and-delete-statements"></a>Elaborazione di istruzioni di eliminazione e aggiornamento posizionato
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Microsoft consiglia di usare le funzionalità del driver del cursore.  
  
 Supporta la libreria il cursore posizionato istruzioni update e delete, sostituendo il **WHERE CURRENT OF** clausola in queste istruzioni con un **in cui** clausola che enumera i valori memorizzati nella cache per ogni colonna associata. La libreria di cursori passa l'oggetto appena costruito **UPDATE** e **eliminare** istruzioni al driver per l'esecuzione. Per istruzioni update posizionate, la libreria di cursori quindi aggiorna la cache da quelli nei buffer di set di righe e imposta il valore corrispondente nella matrice di stato di riga per SQL_ROW_UPDATED. Per istruzioni delete posizionate, imposta il valore corrispondente nella matrice di stato di riga da SQL_ROW_DELETED.  
  
> [!CAUTION]  
>  Il **in cui** clausola costruito dalla libreria di cursori per identificare la riga corrente può non riuscire a identificare tutte le righe, identificare una riga diversa o per identificare più di una riga. Per altre informazioni, vedere [costruzione di istruzioni di eseguire la ricerca](../../../odbc/reference/appendixes/constructing-searched-statements.md), più avanti in questa appendice.  
  
 Eliminazione e aggiornamento posizionato le istruzioni sono soggette alle restrizioni seguenti:  
  
-   Posizionato update e delete possono essere usate solo nei casi seguenti: quando un **selezionate** istruzione ha generato il set di risultati; quando il **selezionare** istruzione non contiene un join, un  **UNION** clausola, o un **GROUP BY** clausola; e quando non sono associate tutte le colonne utilizzate di un'espressione o un alias nell'elenco di selezione con **SQLBindCol**.  
  
-   Se un'applicazione prepara un'istruzione delete o un aggiornamento posizionato, è necessario eseguire questa operazione dopo aver chiamato **SQLFetch** oppure **SQLFetchScroll**. Anche se la libreria di cursori invia l'istruzione per il driver per la preparazione, la chiusura dell'istruzione e viene eseguito direttamente quando l'applicazione chiama **SQLExecute**.  
  
-   Se il driver supporta solo un'istruzione attiva, le operazioni di recupero libreria cursore il resto del risultato set e recupera quindi nuovamente il set di righe corrente dalla cache prima di eseguire un posizionamento istruzione update o delete. Se l'applicazione quindi chiama una funzione che restituisce i metadati in un set di risultati (ad esempio, **SQLNumResultCols** oppure **SQLDescribeCol**), la libreria di cursori restituisce un errore.  
  
-   Se un aggiornamento posizionato o istruzione delete viene eseguita su una colonna di una tabella che include una colonna timestamp viene aggiornata automaticamente ogni volta che viene eseguito un aggiornamento, tutte le successive per gli aggiornamenti posizionati o istruzioni di eliminazione avrà esito negativo se la colonna timestamp associato. Ciò si verifica perché l'elemento cercato, aggiorna o Elimina istruzione che crea la libreria di cursori non identifica in modo accurato la riga da aggiornare. Il valore nell'istruzione avanzata per la colonna timestamp non corrisponderà al valore di aggiornamento automatico della colonna timestamp.
