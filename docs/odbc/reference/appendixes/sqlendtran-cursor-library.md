---
title: SQLEndTran (libreria di cursori) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f713f9a0c96aaf3798cf160e648404470e3a4363
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68064502"
---
# <a name="sqlendtran-cursor-library"></a>SQLEndTran (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Microsoft consiglia di usare le funzionalità del driver del cursore.  
  
 In questo argomento viene illustrato l'utilizzo dei **SQLEndTran** funzione nella libreria di cursori. Per informazioni generali sul **SQLEndTran**, vedere [SQLEndTran-funzione](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
 La libreria di cursori non supporta le transazioni e passa le chiamate a **SQLEndTran** direttamente al driver. Tuttavia, la libreria di cursori supporta la funzionalità di commit e rollback del cursore come restituiti dall'origine dati con i tipi di informazioni SQL_CURSOR_ROLLBACK_BEHAVIOR e SQL_CURSOR_COMMIT_BEHAVIOR:  
  
-   Per le origini dati che conservano i cursori in più transazioni, le modifiche che vengono eseguito il rollback dell'origine dati non eseguire il rollback nella cache della libreria di cursori. Per rendere la cache corrispondono ai dati nell'origine dati, l'applicazione deve chiudere e riaprire il cursore.  
  
-   Per le origini dati che chiudere i cursori in corrispondenza dei limiti delle transazioni, la libreria di cursori chiude i cursori ed Elimina le cache per tutte le istruzioni per la connessione.  
  
-   Per le origini dati che elimina le istruzioni preparate in base ai limiti delle transazioni, l'applicazione deve reprepare tutte le istruzioni preparate per la connessione prima di rieseguire li.
