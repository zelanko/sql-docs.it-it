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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68064502"
---
# <a name="sqlendtran-cursor-library"></a>SQLEndTran (libreria di cursori)
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità di cursore del driver.  
  
 In questo argomento viene illustrato l'utilizzo della funzione **SQLEndTran** nella libreria di cursori. Per informazioni generali su **SQLEndTran**, vedere [funzione SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).  
  
 La libreria di cursori non supporta le transazioni e passa le chiamate a **SQLEndTran** direttamente al driver. Tuttavia, la libreria di cursori supporta i comportamenti di commit e rollback del cursore restituiti dall'origine dati con i tipi di informazioni SQL_CURSOR_ROLLBACK_BEHAVIOR e SQL_CURSOR_COMMIT_BEHAVIOR:  
  
-   Per le origini dati che conservano cursori tra le transazioni, non viene eseguito il rollback delle modifiche di cui viene eseguito il rollback nell'origine dati nella cache della libreria di cursori. Per fare in modo che la cache corrisponda ai dati nell'origine dati, l'applicazione deve chiudere e riaprire il cursore.  
  
-   Per le origini dati che chiudono i cursori ai limiti delle transazioni, la libreria di cursori chiude i cursori ed Elimina le cache per tutte le istruzioni della connessione.  
  
-   Per le origini dati che eliminano le istruzioni preparate ai limiti delle transazioni, l'applicazione deve ripreparare tutte le istruzioni preparate per la connessione prima di eseguirle nuovamente.
