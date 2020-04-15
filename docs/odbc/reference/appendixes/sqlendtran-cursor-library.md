---
title: SQLEndTran (Libreria cursore) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLEndTran function [ODBC], Cursor Library
ms.assetid: 92340b87-9084-4838-a509-e9ca22d5fd5c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c2277a67cd5410ea3c2a5d5b03b16d4533ed6ee1
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304772"
---
# <a name="sqlendtran-cursor-library"></a>SQLEndTran (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità del cursore del driver.  
  
 In questo argomento viene illustrato l'utilizzo della funzione **SQLEndTran** nella libreria di cursori. Per informazioni generali su **SQLEndTran**, vedere [Funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
 La libreria di cursori non supporta le transazioni e passa le chiamate a **SQLEndTran** direttamente al driver. Tuttavia, la libreria di cursori supporta i comportamenti di commit e rollback del cursore restituiti dall'origine dati con i tipi di informazioni SQL_CURSOR_ROLLBACK_BEHAVIOR e SQL_CURSOR_COMMIT_BEHAVIOR:  
  
-   Per le origini dati che mantengono i cursori tra le transazioni, le modifiche di cui viene eseguito il rollback nell'origine dati non vengono annullate nella cache della libreria di cursori. Per fare in modo che la cache corrisponda ai dati nell'origine dati, l'applicazione deve chiudere e riaprire il cursore.  
  
-   Per le origini dati che chiudono i cursori in corrispondenza dei limiti delle transazioni, la libreria di cursori chiude i cursori ed elimina le cache per tutte le istruzioni sulla connessione.  
  
-   Per le origini dati che eliminano le istruzioni preparate ai limiti delle transazioni, l'applicazione deve ripreparare tutte le istruzioni preparate nella connessione prima di rieseguire.
