---
title: I caratteri di dati e stringhe C | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68044924"
---
# <a name="character-data-and-c-strings"></a>Dati di tipo carattere e stringhe C
I parametri di input che fanno riferimento ai dati di tipo carattere a lunghezza variabile (ad esempio i nomi delle colonne, i parametri dinamici e i valori di attributo di stringa) hanno un parametro di lunghezza associato. Se l'applicazione termina le stringhe con il carattere null, come avviene in C, viene fornito come argomento la lunghezza in byte della stringa (senza includere il carattere di terminazione null) né SQL_NTS (Null-Terminated String). Un argomento di lunghezza non negativa specifica la lunghezza effettiva della stringa associata. L'argomento length può essere 0 per specificare una stringa di lunghezza zero, che è diverso da un valore NULL. Il valore negativo SQL_NTS indica al driver per determinare la lunghezza della stringa individuando il carattere di terminazione null.  
  
 Quando dati di tipo carattere vengono restituiti dal driver per l'applicazione, il driver deve sempre null-terminarlo. In questo modo l'applicazione di scegliere se gestire i dati come stringa o una matrice di caratteri. Se il buffer dell'applicazione non è sufficientemente grande per restituire tutti i dati di tipo carattere, il driver lo tronca alla lunghezza in byte del buffer meno il numero di byte richiesti dal carattere di terminazione null, fa terminare con null i dati troncati e lo archivia di buffer. Di conseguenza, le applicazioni devono sempre allocare spazio aggiuntivo per il carattere di terminazione di tipo null in buffer usati per recuperare i dati di tipo carattere. Un buffer di byte a 51, ad esempio, è necessario per recuperare i 50 caratteri di dati.  
  
 È necessario prestare particolare attenzione per l'applicazione e il driver durante l'invio o recupero di dati di tipo carattere long in parti con **SQLPutData** oppure **SQLGetData**. Se i dati vengono passati come una serie di stringhe con terminazione null, i caratteri di terminazione di tipo null in queste stringhe devono essere rimossi prima che i dati possono essere riassemblati.  
  
 Un numero di programmatori ODBC è confusi dati di tipo carattere e stringhe C. Che si è verificato questo è un elemento dell'utilizzo del linguaggio C durante la definizione di funzioni di ODBC. Se un'applicazione o il driver ODBC viene utilizzato un altro linguaggio, tenere presente che ODBC è indipendente dal linguaggio questa confusione è meno probabile che si verificano.  
  
 Quando le stringhe C vengono usate per contenere dati di tipo carattere, il carattere di terminazione null non è considerato parte dei dati e non conteggiato come parte della relativa lunghezza in byte. Ad esempio, i dati di caratteri "ABC" possono essere conservati come la stringa C "ABC\0" o la matrice di caratteri {'A', 'B', 'C''}. La lunghezza in byte dei dati è 3, viene considerato come una stringa o una matrice di caratteri o meno.  
  
 Sebbene le applicazioni e driver comunemente usare stringhe C (matrici con terminazione null di caratteri) per contenere dati di tipo carattere, non è necessario eseguire questa operazione. In C, dati di tipo carattere possono anche essere considerati come una matrice di caratteri (senza terminazione null) e la relativa lunghezza di byte passati separatamente nel buffer di lunghezza/indicatore.  
  
 Poiché una matrice con terminazione null non possono contenere dati di tipo carattere e la lunghezza di byte passati separatamente, è possibile incorporare caratteri null nei dati di carattere. Tuttavia, il comportamento delle funzioni ODBC in questo caso è definito ed è specifico del driver indica se un driver viene gestita correttamente. Di conseguenza, applicazioni interoperative necessario gestire sempre i dati di tipo carattere che possono contenere caratteri null incorporati come dati binari.
