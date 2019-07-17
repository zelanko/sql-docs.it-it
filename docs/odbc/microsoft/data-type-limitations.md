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
ms.openlocfilehash: 64d16a9181c475427677371d1e6e180570225b7a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096458"
---
# <a name="data-type-limitations"></a>Limitazioni dei tipi di dati
I driver di Database Desktop ODBC Microsoft impone le limitazioni seguenti sui tipi di dati:  
  
|Tipo di dati|Descrizione|  
|---------------|-----------------|  
|Tutti i tipi di dati|Gli errori di conversione di tipo potrebbero comportare la colonna interessata viene impostata su NULL.|  
|BINARY|Creazione di una colonna BINARIA di lunghezza zero restituisce effettivamente una colonna BINARIA a 255 byte.|  
|DATE|Impossibile convertire il tipo di dati di data a un altro tipo di dati (o se stessa) per la funzione CONVERT.|  
|Numero decimale (numerico esatto)|Non supportati.|  
|Tipi di dati a virgola mobile|Il numero di posizioni decimali in un numero a virgola mobile può essere limitato dal formato numerico impostato nella sezione internazionale del Pannello di controllo di Windows.|  
|NUMERIC|Supporta la precisione massima e una scala di 28.|  
|TIMESTAMP|Il tipo di dati TIMESTAMP non può essere convertito a se stesso per la funzione CONVERT.|  
|TINYINT|I valori di tipo TINYINT sono sempre senza segno.|  
|Stringhe di lunghezza zero|Quando viene utilizzato un file dBASE, Microsoft Excel, Paradox o Textdriver, inserire una stringa di lunghezza zero in una colonna effettivamente inserisce un valore NULL invece.|
