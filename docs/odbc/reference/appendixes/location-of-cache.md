---
title: Percorso della Cache | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4b1ffd8c56a6727a892cb518222c961bbb6c794c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63181341"
---
# <a name="location-of-cache"></a>Percorso della cache
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Microsoft consiglia di usare le funzionalità del driver del cursore.  
  
 La libreria di cursori vengono memorizzati nella cache i dati in memoria e nei file temporanei Windows®. Questo limita la dimensione del set di risultati in grado di gestire la libreria di cursori solo dallo spazio su disco disponibile. Un file temporaneo viene utilizzato quando i dati da memorizzare nella cache potrebbero superare il limite di segmento se inserito alla fine della cache della libreria di cursori. Al contrario, i dati da memorizzare nella cache vengono aggiunti al posto del blocco ultimo salvataggio dei dati nella cache. L'ultimo salvataggio del blocco di dati viene salvato in un file temporaneo. Se la libreria di cursori termina in modo anomalo, ad esempio quando la potenza ha esito negativo, è possibile lasciare i file temporanei di Windows sul disco. Queste sono denominate ~ CTT*nnnn*TMP e vengono creati nella directory corrente.  
  
> [!NOTE]  
>  Se la libreria di cursori in Microsoft® WindowsNT®/Windows 2000 tenta di memorizzare i dati in un file temporaneo nella directory corrente mentre l'applicazione è in esecuzione da una condivisione di sola lettura o un CD (ad esempio, un esempio di libreria Microsoft Foundation Class), SQLSTATE HY000 verrà restituito (generale errore-Unable per creare un buffer di file).
