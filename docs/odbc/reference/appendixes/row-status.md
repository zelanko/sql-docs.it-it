---
description: Stato riga
title: Stato riga | Microsoft Docs
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
ms.openlocfilehash: 8970e78d523ca86a50edb1e27b159ef15a1a1747
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424963"
---
# <a name="row-status"></a>Stato riga
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità di cursore del driver.  
  
 La libreria di cursori crea un buffer nella cache per lo stato della riga. La libreria di cursori recupera i valori per la matrice di stato della riga (specificata con l'attributo dell'istruzione SQL_ATTR_ROW_STATUS_PTR) dal buffer. Per ogni riga, la libreria di cursori imposta questo buffer su:  
  
-   SQL_ROW_DELETED quando viene eseguita un'istruzione DELETE posizionata sulla riga.  
  
-   SQL_ROW_ERROR quando viene rilevato un errore durante il recupero della riga dall'origine dati con **SQLFetch**.  
  
-   SQL_ROW_SUCCESS quando recupera correttamente la riga dall'origine dati con **SQLFetch**.  
  
-   SQL_ROW_UPDATED quando viene eseguita un'istruzione UPDATE posizionata sulla riga.
