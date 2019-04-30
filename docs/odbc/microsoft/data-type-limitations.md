---
title: Limitazioni del tipo di dati | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d4ce0eb96832f4a6b9c1953b0a9a9d0af65cb3b0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63187439"
---
# <a name="data-type-limitations"></a>Limitazioni dei tipi di dati
I driver di Database Desktop ODBC Microsoft impone le limitazioni seguenti sui tipi di dati:  
  
|Tipo di dati|Descrizione|  
|---------------|-----------------|  
|Tutti i tipi di dati|Gli errori di conversione di tipo potrebbero comportare la colonna interessata viene impostata su NULL.|  
|BINARY|Creazione di una colonna BINARIA di lunghezza zero restituisce effettivamente una colonna BINARIA a 255 byte.|  
|DATE|Impossibile convertire il tipo di dati di data a un altro tipo di dati (o se stessa) per la funzione CONVERT.|  
|Numero decimale (numerico esatto)|Non supportato.|  
|Tipi di dati a virgola mobile|Il numero di posizioni decimali in un numero a virgola mobile può essere limitato dal formato numerico impostato nella sezione internazionale del Pannello di controllo di Windows.|  
|NUMERIC|Supporta la precisione massima e una scala di 28.|  
|timestamp|Il tipo di dati TIMESTAMP non può essere convertito a se stesso per la funzione CONVERT.|  
|TINYINT|I valori di tipo TINYINT sono sempre senza segno.|  
|Stringhe di lunghezza zero|Quando viene utilizzato un file dBASE, Microsoft Excel, Paradox o Textdriver, inserire una stringa di lunghezza zero in una colonna effettivamente inserisce un valore NULL invece.|
