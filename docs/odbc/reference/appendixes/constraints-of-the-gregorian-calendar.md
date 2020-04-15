---
title: Vincoli del calendario gregoriano Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], Gregorian calendar
- Gregorian calendar [ODBC]
ms.assetid: 70667410-c582-4369-8e06-9d98e21cd2bf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f88842c7426e17af1fdc0533b8b97e2c559de237
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81284761"
---
# <a name="constraints-of-the-gregorian-calendar"></a>Vincoli del calendario gregoriano
I tipi di dati date e datetime e i campi finali dei tipi di dati intervallo devono essere conformi ai vincoli del calendario gregoriano. Questi vincoli sono i seguenti:  
  
-   Il valore del campo del mese deve essere compreso tra 1 e 12 inclusi.  
  
-   Il valore del campo giorno deve essere compreso nell'intervallo compreso tra 1 e il numero di giorni del mese. Il numero di giorni del mese è determinato dai valori dei campi anno e mesi e può essere 28, 29, 30 o 31. (Il numero di giorni nel mese può anche dipendere se si tratta di un anno bisestile.)  
  
-   Il valore del campo dell'ora deve essere compreso tra 0 e 23, inclusi.  
  
-   Il valore del campo dei minuti deve essere compreso tra 0 e 59, inclusi.  
  
-   Per il campo dei secondi finali dei tipi di dati intervallo, il valore del campo secondi deve essere compreso tra 0 e 59,9(*n*), inclusi, dove *n* è il numero di cifre nella precisione dei secondi frazionari.  
  
-   Per il campo dei secondi finali dei tipi di dati datetime, il valore del campo secondi deve essere compreso tra 0 e 61,9(*n*), inclusi, dove *n* specifica il numero di "9" cifre e il valore di *n* è la precisione dei secondi frazionari. (L'intervallo di secondi consente fino a due secondi intercalari per mantenere la sincronizzazione del tempo siderale.)
