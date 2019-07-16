---
title: Precisione del tipo di dati di intervallo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- precision [ODBC], interval data types
- seconds precision [ODBC]
- interval data type [ODBC], precision
- precision [ODBC]
- interval leading precision [ODBC]
- interval precision [ODBC]
ms.assetid: eb73bd77-2e7e-4498-a266-4d7c990a0d56
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3424c58d25be69d2ddc42a3088aa457ebddf1d4b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67947607"
---
# <a name="interval-data-type-precision"></a>Precisione del tipo di dati intervallo
Precisione per un tipo di dati di intervallo include intervallo iniziali precisione, intervallo di precisione e la precisione in secondi.  
  
 Il campo iniziale dell'intervallo è un valore numerico con segno. Il numero massimo di cifre per il campo iniziale è determinato da una quantità chiamata *intervallo di precisione, iniziale* che costituisce una parte della dichiarazione del tipo di dati. Ad esempio, la dichiarazione: INTERVALLO HOUR(5) per minuto dispone di un intervallo di precisione iniziale pari a 5; il campo dell'ora può accettare valori da-99999 e 99999. L'intervallo di precisione iniziale è contenuto nel campo SQL_DESC_DATETIME_INTERVAL_PRECISION del record del descrittore.  
  
 L'elenco dei campi che un tipo di dati di intervallo è costituito da viene chiamato *intervallo di precisione*. Non un valore numerico, come il termine "precisione" potrebbe implicare. Ad esempio, la precisione di intervallo del tipo INTERVAL DAY TO in secondo luogo è nell'elenco il giorno, ora, minuto, secondo. Nessun campo descrittore che contiene questo valore. l'intervallo di precisione può sempre essere determinato dal tipo di dati intervallo.  
  
 Qualsiasi tipo di dati di intervallo con un secondo campo ha un *precisione dei secondi*. Questo è il numero di cifre decimali consentito nella parte frazionaria del valore dei secondi. Ciò è diverso da quello per altri tipi di dati, in cui la precisione indica il numero di cifre prima del separatore decimale. La precisione dei secondi di un tipo di dati di intervallo è il numero di cifre dopo il separatore decimale. Ad esempio, se la precisione dei secondi è impostata su 6, il numero 123456 nel campo della frazione sarebbe interpretato come.123456 e il numero 1230 verrebbe interpretati come.001230. Per altri tipi di dati, questo viene detto scala. Precisione dei secondi di intervallo è contenuta nel campo SQL_DESC_PRECISION del descrittore. Se la precisione del componente i secondi frazionari del valore di intervallo SQL è maggiore di ciò che possono essere contenuti nella struttura di intervallo C, driver-definito se il valore di frazioni di secondo in un intervallo di SQL è arrotondato o troncato quando convertito in C struttura di intervallo.  
  
 Quando il campo SQL_DESC_CONCISE_TYPE è impostato su un tipo di dati di intervallo, il campo SQL_DESC_TYPE è impostato su SQL_INTERVAL e al codice per il tipo di dati di intervallo è impostato il SQL_DESC_DATETIME_INTERVAL_CODE. Il campo SQL_DESC_DATETIME_INTERVAL_PRECISION viene impostato automaticamente alla precisione iniziale intervallo predefinito di 2 e il campo SQL_DESC_PRECISION viene automaticamente impostato per la precisione dei secondi di intervallo predefinito di 6. Se uno di questi valori non è appropriato, l'applicazione deve impostare in modo esplicito il campo di descrizione tramite una chiamata a **SQLSetDescField**.
