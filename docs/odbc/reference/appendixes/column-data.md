---
title: Dati di colonna - Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ff89566efa65c88325d98422fe17788f27d2c8ca
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306592"
---
# <a name="column-data"></a>Dati della colonna
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzare questa funzionalità nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che attualmente utilizzano questa funzionalità. Microsoft consiglia di utilizzare la funzionalità del cursore del driver.  
  
 La libreria di cursori crea un buffer nella cache per ogni buffer di dati associato al set di risultati con **SQLBindCol**. Utilizza i valori in questi buffer per costruire una clausola **WHERE** quando emula un'istruzione update o delete posizionata. Aggiorna questi buffer dai buffer del set di righe quando recupera i dati dall'origine dati e quando esegue istruzioni di aggiornamento posizionate.  
  
 Quando la libreria di cursori aggiorna la cache dai buffer del set di righe, trasferisce i dati in base al tipo di dati C specificato in **SQLBindCol**. Ad esempio, se il tipo di dati C di un buffer di set di righe è SQL_C_SLONG, la libreria di cursori trasferisce quattro byte di dati; se è SQL_C_CHAR e *BufferLength* è 10, la libreria di cursori trasferisce 10 byte di dati. La libreria di cursori non esegue alcun controllo del tipo o conversioni sui dati trasferiti.  
  
> [!NOTE]  
>  La libreria di cursori non aggiorna la cache per una colonna*StrLen_or_IndPtr* se nel buffer del set di righe corrispondente è SQL_DATA_AT_EXEC o il risultato della macro SQL_LEN_DATA_AT_EXEC.  
  
 Quando aggiorna una colonna, un'origine dati vuota riempie i dati di tipo carattere a lunghezza fissa e zero pad dati binari a lunghezza fissa in base alle esigenze. Ad esempio, un'origine dati archivia "Rossi" in una colonna CHAR(10) come "Rossi". La libreria di cursori non i dati blank-pad o zero-pad nei buffer del set di righe quando copia questi dati nella cache dopo l'esecuzione di un'istruzione di aggiornamento posizionato. Pertanto, se un'applicazione richiede che i valori nella cache della libreria di cursori siano riempiti in bianco o senza spaziatura, deve riempire i valori nei buffer del set di righe prima di eseguire un'istruzione di aggiornamento posizionata.
