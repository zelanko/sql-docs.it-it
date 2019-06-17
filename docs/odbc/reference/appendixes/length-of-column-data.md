---
title: Lunghezza dei dati della colonna | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- column data [ODBC]
- length of column data [ODBC]
- ODBC cursor library [ODBC], cache
- cursor library [ODBC], cache
- cache [ODBC]
ms.assetid: c762c881-ebe0-4eac-84d5-f30281fc3eca
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6d14fa4303dd1f67a77bf14dcebeeb933ccce9e1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188831"
---
# <a name="length-of-column-data"></a>Lunghezza dei dati di colonna
> [!IMPORTANT]  
>  Questa funzionalità verrà rimossa in una versione futura di Windows. Evitare di utilizzarla nelle nuove attività di sviluppo e pianificare la modifica delle applicazioni che utilizzano attualmente questa funzionalità. Microsoft consiglia di usare le funzionalità del driver del cursore.  
  
 La libreria di cursori consente di creare un buffer per ogni buffer di lunghezza/indicatore associato al set di risultati nella cache **SQLBindCol**. Usa i valori in questi buffer per costruire una **in cui** clausola quando emula per gli aggiornamenti posizionati o eliminare le istruzioni. Aggiorna tali buffer dai buffer di set di righe durante il recupero dei dati dall'origine dei dati e quando esegue le istruzioni update posizionate.  
  
 Se il tipo C di un buffer di dati è SQL_C_CHAR o SQL_C_BINARY e il valore di lunghezza/indicatore è SQL_NTS, la lunghezza della stringa di dati viene inserita nel buffer di lunghezza/indicatore.  
  
> [!NOTE]  
>  La libreria di cursori non aggiorna la cache per una colonna se **StrLen_or_IndPtr* nel set di righe corrispondente buffer è il risultato della macro SQL_LEN_DATA_AT_EXEC o SQL_DATA_AT_EXEC.
