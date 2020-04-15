---
title: Limitazioni del tipo di dati Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], data types
- data types [ODBC], desktop database drivers
- desktop database drivers [ODBC], data types
ms.assetid: 81c4eab7-1f6b-47a0-b940-89d6c6a14dae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4beaf91a4ead743e3e8a2e32578796baba3c17be
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280671"
---
# <a name="data-type-limitations"></a>Limitazioni dei tipi di dati
I driver di database desktop Microsoft ODBC impongono le seguenti limitazioni sui tipi di dati:  
  
|Tipo di dati|Descrizione|  
|---------------|-----------------|  
|Tutti i tipi di dati|Gli errori di conversione dei tipi potrebbero causare l'impostazione della colonna interessata su NULL.|  
|BINARY|La creazione di una colonna BINARY di lunghezza zero restituisce in realtà una colonna BINARY a 255 byte.|  
|DATE|Il tipo di dati DATE non può essere convertito in un altro tipo di dati (o se stesso) dalla funzione CONVERT.|  
|DECIMALE (carattere esatto)|Non supportato.|  
|Tipi di dati a virgola mobile|Il numero di posizioni decimali in un numero a virgola mobile può essere limitato dal formato numerico impostato nella sezione Internazionale del Pannello di controllo di Windows.|  
|NUMERIC|Supporta la massima precisione e una scala di 28.|  
|timestamp|Il tipo di dati TIMESTAMP non può essere convertito in se stesso dalla funzione CONVERT.|  
|TINYINT|I valori TINYINT sono sempre senza segno.|  
|Stringhe di lunghezza zero|Quando si utilizza un dBASE, Microsoft Excel, Paradox o Textdriver, l'inserimento di una stringa di lunghezza zero in una colonna inserisce effettivamente un valore NULL.|
