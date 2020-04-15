---
title: Lunghezza del buffer di dati Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d4a4e9a739201d74cfc6c4f7c18e64b91e0fabe4
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305262"
---
# <a name="data-buffer-length"></a>Lunghezza del buffer dei dati
L'applicazione passa la lunghezza in byte del buffer di dati al driver in un argomento, denominato *BufferLength* o un nome simile. Ad esempio, nella seguente chiamata a **SQLBindCol**, l'applicazione specifica la lunghezza del buffer *ValuePtr* (**sizeof(***ValuePtr***)**):  
  
```  
SQLCHAR      ValuePtr[50];  
SQLINTEGER   ValueLenOrInd;  
SQLBindCol(hstmt, 1, SQL_C_CHAR, ValuePtr, sizeof(ValuePtr), &ValueLenOrInd);  
```  
  
 Un driver restituirà sempre il numero di byte, non il numero di caratteri, nell'argomento lunghezza del buffer di qualsiasi funzione che dispone di un argomento di stringa di output.  
  
 Le lunghezze del buffer di dati sono necessarie solo per i buffer di output; il driver li utilizza per evitare di scrivere oltre la fine del buffer. Tuttavia, il driver controlla la lunghezza del buffer di dati solo quando il buffer contiene dati a lunghezza variabile, ad esempio dati di tipo carattere o binario. Se il buffer contiene dati a lunghezza fissa, ad esempio un numero intero o una struttura di data, il driver ignora la lunghezza del buffer di dati e presuppone che il buffer sia sufficientemente grande per contenere i dati. ovvero non tronca mai i dati a lunghezza fissa. È quindi importante che l'applicazione allochi un buffer sufficientemente grande per i dati a lunghezza fissa.  
  
 Quando si verifica un troncamento di stringhe di output non di dati (ad esempio il nome del cursore restituito per **SQLGetCursorName**), la lunghezza restituita nell'argomento lunghezza del buffer è la lunghezza massima possibile dei caratteri.  
  
 Le lunghezze del buffer di dati non sono necessarie per i buffer di input perché il driver non scrive in questi buffer.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Utilizzo dei valori di lunghezza/indicatore](../../../odbc/reference/develop-app/using-length-and-indicator-values.md)  
  
-   [Lunghezza dei dati, lunghezza del buffer e troncamento](../../../odbc/reference/develop-app/data-length-buffer-length-and-truncation.md)  
  
-   [Dati di tipo carattere e stringhe C](../../../odbc/reference/develop-app/character-data-and-c-strings.md)
