---
title: Dati della colonna | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- column data [ODBC]
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: 0425818c-9469-493f-9e3c-fc03d9411c5c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 95f80c82d3804e31d5ea29d55af0fbedd4184e6c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63213847"
---
# <a name="column-data"></a>Dati della colonna
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Microsoft consiglia di usare le funzionalità del driver del cursore.  
  
 La libreria di cursori consente di creare un buffer per ogni buffer di dati associato al set di risultati nella cache **SQLBindCol**. Usa i valori in questi buffer per costruire una **in cui** clausola quando che emula un posizionati istruzione update o delete. Aggiorna tali buffer dai buffer di set di righe durante il recupero dei dati dall'origine dei dati e quando esegue le istruzioni update posizionate.  
  
 Quando la libreria di cursori Aggiorna la propria cache dai buffer di set di righe, di trasferire i dati in base al tipo di dati C specificato nella **SQLBindCol**. Ad esempio, se il tipo di dati C di un buffer di righe è SQL_C_SLONG, la libreria di cursori trasferisce i quattro byte di dati. Se si tratta di SQL_C_CHAR e *BufferLength* è 10, la libreria di cursori trasferimenti di dati a 10 byte. La libreria di cursori non esegue alcun controllo dei tipi o le conversioni dei dati che viene trasferita l'esecuzione.  
  
> [!NOTE]  
>  La libreria di cursori non aggiorna la cache per una colonna se **StrLen_or_IndPtr* nel set di righe corrispondente buffer è il risultato della macro SQL_LEN_DATA_AT_EXEC o SQL_DATA_AT_EXEC.  
  
 Quando aggiorna una colonna, una dati di carattere a lunghezza fissa vuoto riquadri origine e dati binari da zero, fino a lunghezza fissa in base alle esigenze. Ad esempio, un'origine dati memorizza "Smith" in una colonna char (10) come "Smith". La libreria di cursori non non aggiungerebbero blank o zero-riquadro dei dati nei buffer di set di righe durante la copia i dati nella cache dopo l'esecuzione di un'istruzione per gli aggiornamenti posizionati. Pertanto, se un'applicazione richiede che i valori nella cache della libreria di cursori sono riempiti con degli zero o zeri, deve aggiungerebbero blank o zero-pad i valori nei buffer di set di righe prima di eseguire un'istruzione per gli aggiornamenti posizionati.
