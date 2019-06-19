---
title: I vincoli del calendario gregoriano | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 30fbdd17e7ec5eb970948e1c7133020081222614
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63224554"
---
# <a name="constraints-of-the-gregorian-calendar"></a>Vincoli del calendario gregoriano
Tipi di dati date e datetime e i campi finali dei tipi di dati di intervallo, devono essere conforme ai vincoli del calendario gregoriano. Questi vincoli sono i seguenti:  
  
-   Il valore del campo mese deve essere compreso tra 1 e 12 inclusi.  
  
-   Il valore del campo giorno deve essere compreso nell'intervallo compreso tra 1 e il numero di giorni del mese. Il numero di giorni del mese è determinato dai valori dei campi anni e mesi e può essere 28, 29, 30 o 31. (Il numero di giorni nel mese può anche dipendere si tratti di un anno bisestile.)  
  
-   Il valore del campo ora deve essere compreso tra 0 e 23, inclusivo.  
  
-   Il valore del campo relativo ai minuti deve essere compreso tra 0 e 59, inclusivo.  
  
-   Per il campo secondi finali dei tipi di dati di intervallo, il valore del campo secondi deve essere compreso tra 0 e 59,9 (*n*), inclusi, in cui *n* è il numero di cifre per la precisione frazionaria dei secondi.  
  
-   Per il campo secondi finali dei tipi di dati Data/ora, il valore del campo secondi deve essere compreso tra 0 e 61.9 (*n*), inclusi, in cui *n* specifica il numero di cifre "9" e il valore di *n*  precisione frazionaria dei secondi. (L'intervallo di secondi consente un massimo di due secondi di compensazione mantenere la sincronizzazione dell'ora siderale.)
