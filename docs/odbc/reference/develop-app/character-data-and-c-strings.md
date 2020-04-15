---
title: Dati di carattere e stringhe C Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7bb25022d4e0c0559f2a8f77b89a4ba26aeba33a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307491"
---
# <a name="character-data-and-c-strings"></a>Dati di tipo carattere e stringhe C
Ai parametri di input che fanno riferimento a dati di tipo carattere a lunghezza variabile, ad esempio nomi di colonna, parametri dinamici e valori di attributo stringa, è associato un parametro length. Se l'applicazione termina le stringhe con il carattere null, come è tipico in C, fornisce come argomento la lunghezza in byte della stringa (escluso il carattere di terminazione null) o SQL_NTS (stringa con terminazione Null). Un argomento di lunghezza non negativo specifica la lunghezza effettiva della stringa associata. L'argomento length può essere 0 per specificare una stringa di lunghezza zero, distinta da un valore NULL. Il valore negativo SQL_NTS indica al driver di determinare la lunghezza della stringa individuando il carattere di terminazione null.  
  
 Quando i dati di tipo carattere vengono restituiti dal driver all'applicazione, il driver deve sempre null terminarlo. In questo modo l'applicazione può scegliere se gestire i dati come una stringa o una matrice di caratteri. Se il buffer dell'applicazione non è sufficientemente grande per restituire tutti i dati di tipo carattere, il driver tronca alla lunghezza in byte del buffer meno il numero di byte richiesti dal carattere di terminazione null, null termina i dati troncati e li archivia nel buffer. Pertanto, le applicazioni devono sempre allocare spazio aggiuntivo per il carattere di terminazione null nei buffer utilizzati per recuperare i dati di tipo carattere. Ad esempio, è necessario un buffer di 51 byte per recuperare 50 caratteri di dati.  
  
 Particolare attenzione deve essere presa sia dall'applicazione che dal driver durante l'invio o il recupero di dati con caratteri lunghi in parti con **SQLPutData** o **SQLGetData**. Se i dati vengono passati come una serie di stringhe con terminazione null, i caratteri di terminazione null in queste stringhe devono essere rimossi prima che i dati possano essere riassemblati.  
  
 Un certo numero di programmatori ODBC hanno confuso i dati di tipo carattere e stringhe C. Che questo si è verificato è un elemento di utilizzo del linguaggio C quando si definiscono le funzioni ODBC. Se un driver ODBC o un'applicazione utilizza un'altra lingua, tenere presente che ODBC è indipendente dalla lingua, è meno probabile che si verifichi questa confusione.  
  
 Quando le stringhe C vengono utilizzate per contenere dati di tipo carattere, il carattere di terminazione null non viene considerato parte dei dati e non viene conteggiato come parte della lunghezza in byte. Ad esempio, i dati di tipo carattere "ABC" possono essere mantenuti come la stringa C "ABC 0" o la matrice di caratteri "'A', 'B', 'C'". La lunghezza in byte dei dati è 3, indipendentemente dal fatto che vengano considerati come una stringa o una matrice di caratteri.  
  
 Sebbene le applicazioni e i driver utilizzino in genere stringhe C (matrici di caratteri con terminazione null) per contenere dati di tipo carattere, non è necessario eseguire questa operazione. In C, i dati di tipo carattere possono anche essere considerati come una matrice di caratteri (senza terminazione null) e la relativa lunghezza in byte passata separatamente nel buffer di lunghezza/indicatore.  
  
 Poiché i dati di tipo carattere possono essere contenuti in una matrice senza terminazione null e la relativa lunghezza in byte passata separatamente, è possibile incorporare caratteri null nei dati di tipo carattere. Tuttavia, il comportamento delle funzioni ODBC in questo caso non è definito ed è specifico del driver se un driver gestisce questo correttamente. Di conseguenza, le applicazioni interoperabili devono sempre gestire dati di tipo carattere che possono contenere caratteri null incorporati come dati binari.
