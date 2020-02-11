---
title: Dati di tipo carattere e stringhe C | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data buffers [ODBC], length
- data buffers [ODBC], character data
- buffers [ODBC], C strings
- buffers [ODBC], character data
- character data and buffers [ODBC]
- length of data buffers [ODBC]
- data buffers [ODBC], C strings
- buffers [ODBC], length
- C strings and buffers [ODBC]
ms.assetid: 3a141cb4-229d-4027-9349-615cb2995e36
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ed99ab72e3d5112588a0b1c93df34b01aff7acdd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68044924"
---
# <a name="character-data-and-c-strings"></a>Dati di tipo carattere e stringhe C
I parametri di input che fanno riferimento a dati di tipo carattere a lunghezza variabile (ad esempio nomi di colonna, parametri dinamici e valori di attributo stringa) hanno un parametro di lunghezza associato. Se l'applicazione termina le stringhe con il carattere null, come tipico in C, fornisce come argomento la lunghezza in byte della stringa (escluso il carattere di terminazione null) o SQL_NTS (stringa con terminazione null). Un argomento di lunghezza non negativa specifica la lunghezza effettiva della stringa associata. L'argomento length può essere 0 per specificare una stringa di lunghezza zero, che è diversa da un valore NULL. Il valore negativo SQL_NTS indica al driver di determinare la lunghezza della stringa individuando il carattere di terminazione null.  
  
 Quando i dati di tipo carattere vengono restituiti dal driver all'applicazione, il driver deve sempre essere null per terminarlo. Ciò consente all'applicazione di scegliere se gestire i dati come una stringa o una matrice di caratteri. Se il buffer dell'applicazione non è sufficientemente grande da restituire tutti i dati di tipo carattere, il driver lo tronca alla lunghezza in byte del buffer meno il numero di byte richiesto dal carattere di terminazione null, termina i dati troncati e li archivia nel buffer. Pertanto, le applicazioni devono sempre allocare spazio aggiuntivo per il carattere di terminazione null nei buffer utilizzati per recuperare i dati di tipo carattere. Ad esempio, è necessario un buffer a 51 byte per recuperare 50 caratteri di dati.  
  
 È necessario prestare particolare attenzione all'applicazione e al driver quando si inviano o si recuperano dati di tipo carattere lungo in parti con **SQLPutData** o **SQLGetData**. Se i dati vengono passati come una serie di stringhe con terminazione null, i caratteri di terminazione null in queste stringhe devono essere rimossi prima che i dati possano essere riassemblati.  
  
 Molti programmatori ODBC hanno confuso i dati di tipo carattere e le stringhe C. Questo problema si verifica quando si definiscono le funzioni ODBC utilizzando il linguaggio C. Se un'applicazione o un driver ODBC utilizza un'altra lingua, tenere presente che ODBC è indipendente dalla lingua. è meno probabile che si verifichi questa confusione.  
  
 Quando si utilizzano stringhe C per contenere dati di tipo carattere, il carattere di terminazione null non viene considerato parte dei dati e non viene conteggiato come parte della lunghezza in byte. Ad esempio, i dati di tipo carattere "ABC" possono essere mantenuti come la stringa C "ABC\0" o la matrice di caratteri {' A ',' B ',' c'}. La lunghezza in byte dei dati è 3, indipendentemente dal fatto che venga considerata come una stringa o una matrice di caratteri.  
  
 Sebbene le applicazioni e i driver usino comunemente stringhe C (matrici di caratteri con terminazione null) per conservare i dati di tipo carattere, non è necessario eseguire questa operazione. In C, i dati di tipo carattere possono essere considerati anche come una matrice di caratteri (senza terminazione null) e la relativa lunghezza in byte viene passata separatamente nel buffer di lunghezza/indicatore.  
  
 Poiché i dati di tipo carattere possono essere conservati in una matrice con terminazione non null e la relativa lunghezza in byte viene passata separatamente, è possibile incorporare caratteri null nei dati di tipo carattere. Tuttavia, il comportamento delle funzioni ODBC in questo caso non è definito ed è specifico del driver se un driver gestisce correttamente questa operazione. Pertanto, le applicazioni interoperative devono gestire sempre i dati di tipo carattere che possono contenere caratteri null incorporati come dati binari.
