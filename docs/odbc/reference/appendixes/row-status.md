---
title: Proprietà Row Status (Stato della riga) Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- row status [ODBC]
- cache [ODBC]
ms.assetid: 0f0b1fb6-f697-4ced-811c-2908e210bc71
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d4ae4169dc3f2a491663f4a86c564cfee5c2f4d6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305100"
---
# <a name="row-status"></a>Stato riga
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità del cursore del driver.  
  
 La libreria di cursori crea un buffer nella cache per lo stato della riga. La libreria di cursori recupera i valori per la matrice di stato della riga (specificata con l'attributo di istruzione SQL_ATTR_ROW_STATUS_PTR) da questo buffer. Per ogni riga, la libreria di cursori imposta questo buffer su:For each row, the cursor library sets this buffer to:  
  
-   SQL_ROW_DELETED quando viene eseguita un'istruzione delete posizionata sulla riga.  
  
-   SQL_ROW_ERROR quando viene rilevato un errore durante il recupero della riga dall'origine dati con **SQLFetch**.  
  
-   SQL_ROW_SUCCESS quando viene recuperata correttamente la riga dall'origine dati con **SQLFetch**.  
  
-   SQL_ROW_UPDATED quando viene eseguita un'istruzione di aggiornamento posizionata sulla riga.
