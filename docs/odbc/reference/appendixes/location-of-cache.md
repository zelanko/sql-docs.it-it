---
title: Posizione della cache Documenti Microsoft
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
ms.openlocfilehash: 13510332ae8bfab07a13d7831f9f74a048551214
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288619"
---
# <a name="location-of-cache"></a>Percorso della cache
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità del cursore del driver.  
  
 La libreria di cursori memorizza i dati nella cache e nei file temporanei di Windows®. Questo limita le dimensioni del set di risultati che la libreria di cursori può gestire solo in base allo spazio disponibile su disco. Un file temporaneo viene utilizzato quando i dati da memorizzare nella cache attraverserebbero il limite del segmento se inseriti alla fine della cache della libreria di cursori. Al contrario, i dati da memorizzare nella cache vengono aggiunti al posto dell'ultimo blocco di dati salvato nella cache. L'ultimo blocco di dati salvato viene salvato in un file temporaneo. Se la libreria di cursori termina in modo anomalo, ad esempio quando si verifica un errore di alimentazione, può lasciare i file temporanei di Windows sul disco. Questi elementi sono denominati CTT*nnnn*.tmp e vengono creati nella directory corrente.  
  
> [!NOTE]  
>  Se la libreria di cursori in Microsoft® WindowsNT®/Windows2000 tenta di memorizzare i dati nella cache in un file temporaneo nella directory corrente mentre l'applicazione è in esecuzione da una condivisione di sola lettura o da un disco compatto (ad esempio un esempio di libreria Microsoft Foundation Class), verrà restituito SQLSTATE HY000 (errore generale-Impossibile creare un buffer di file).
