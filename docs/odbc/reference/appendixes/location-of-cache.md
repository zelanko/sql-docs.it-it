---
description: Percorso della cache
title: Percorso della cache | Microsoft Docs
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
- cache [ODBC]
ms.assetid: 240d6162-4da6-4b1f-96c7-f379f4ecb16f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 29a0c5507c1b8f581d85b0524784f8ccf1695a5f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429623"
---
# <a name="location-of-cache"></a>Percorso della cache
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità di cursore del driver.  
  
 La libreria di cursori memorizza nella cache i dati in memoria e in Windows® file temporanei. Questo limita le dimensioni del set di risultati che la libreria di cursori può gestire solo dallo spazio disponibile su disco. Un file temporaneo viene utilizzato quando i dati da memorizzare nella cache superano il limite del segmento se inserito alla fine della cache della libreria di cursori. Al contrario, i dati da memorizzare nella cache vengono aggiunti al posto dell'ultimo blocco di dati salvato nella cache. L'ultimo blocco di dati salvato viene salvato in un file temporaneo. Se la libreria di cursori termina in modo anomalo, ad esempio in caso di errore di alimentazione, può lasciare i file temporanei di Windows sul disco. Questi sono denominati ~ CTT*nnnn*. tmp e vengono creati nella directory corrente.  
  
> [!NOTE]  
>  Se la libreria di cursori in Microsoft® WindowsNT®/Windows2000 tenta di memorizzare nella cache i dati di un file temporaneo nella directory corrente mentre l'applicazione è in esecuzione da una condivisione di sola lettura o da un disco compatto, ad esempio un libreria Microsoft Foundation Class esempio, viene restituito SQLSTATE HY000 (errore generale-Impossibile creare un buffer di file).
