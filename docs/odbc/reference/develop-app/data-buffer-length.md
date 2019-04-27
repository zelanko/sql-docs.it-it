---
title: La lunghezza del Buffer dei dati | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data buffers [ODBC], length
- buffers [ODBC], data
- length of data buffers [ODBC]
- buffers [ODBC], length
ms.assetid: 7288d143-f9e5-4f90-9b31-2549df79c109
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 57f4fd34cfe3896bb29ed31f02906ce675e4b854
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62640503"
---
# <a name="data-buffer-length"></a>Lunghezza del buffer dei dati
L'applicazione supera la lunghezza in byte del buffer di dati del driver in un argomento, denominato *BufferLength* o un nome simile. Ad esempio, nella chiamata seguente a **SQLBindCol**, l'applicazione specifica la lunghezza delle *ValuePtr* buffer (**sizeof (***ValuePtr***)**):  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 Un driver restituirà sempre il numero di byte, non il numero di caratteri, nell'argomento di lunghezza del buffer di qualsiasi funzione che dispone di un argomento di stringa di output.  
  
 Lunghezza dei buffer di dati è necessari solo per i buffer di output. il driver li utilizza per evitare di scrivere oltre la fine del buffer. Tuttavia, il driver controlla la lunghezza del buffer dei dati solo quando il buffer contiene dati a lunghezza variabile, ad esempio carattere o binario. Se il buffer contiene dati a lunghezza fissa, ad esempio una struttura di data o numero intero, il driver ignora la lunghezza del buffer dei dati e si presuppone che il buffer è sufficientemente grande da contenere i dati. viene troncata, mai dati a lunghezza fissa. È quindi importante per l'applicazione allocare un buffer sufficiente per i dati a lunghezza fissa.  
  
 Quando il troncamento dei dati non stringhe di output viene generato (ad esempio il nome del cursore restituito per **SQLGetCursorName**), la lunghezza restituita nell'argomento di lunghezza di buffer è la lunghezza caratteri massima possibile.  
  
 Lunghezza dei buffer di dati non è necessari per i buffer di input perché il driver non scrivere tali buffer.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Usando i valori di lunghezza/indicatore](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)  
  
-   [Lunghezza dei dati, lunghezza del buffer e troncamento](../../../odbc/reference/develop-app/data-length-buffer-length-and-truncation.md)  
  
-   [Dati di tipo carattere e stringhe C](../../../odbc/reference/develop-app/character-data-and-c-strings.md)
