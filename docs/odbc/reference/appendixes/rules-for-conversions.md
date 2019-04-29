---
title: Regole per le conversioni | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- numeric data type [ODBC], literals
- conversions with numeric literals [ODBC]
- numeric literals [ODBC]
- literals [ODBC], numeric
ms.assetid: 89f846a3-001d-496a-9843-ac9c38dc1762
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a3ecee500204303dfcbcd8e179b9cb9cb0a94bae
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63032924"
---
# <a name="rules-for-conversions"></a>Regole per le conversioni
Le regole in questa sezione si applicano per le conversioni che includono valori letterali numerici. Ai fini di queste regole, vengono definiti i termini seguenti:  
  
-   *Assegnazione Store:* Quando si inviano dati in una colonna di tabella in un database. Ciò si verifica durante le chiamate a **SQLExecute**, **SQLExecDirect**, e **SQLSetPos**. Durante l'assegnazione di archivio, "target" fa riferimento a una colonna del database e "origine" fa riferimento ai dati nel buffer dell'applicazione.  
  
-   *Assegnazione di recupero:* Quando si recuperano dati dal database nel buffer dell'applicazione. Ciò si verifica durante le chiamate a **SQLFetch**, **SQLGetData**, **SQLFetchScroll**, e **SQLSetPos**. Durante l'assegnazione di recupero, "target" fa riferimento al buffer dell'applicazione e "origine" fa riferimento alla colonna del database.  
  
-   *CS:* Il valore dell'origine del carattere.  
  
-   *NT:* Il valore nel database di destinazione numerica.  
  
-   *NS:* Il valore nell'origine numerico.  
  
-   *CT:* Il valore nella destinazione di caratteri.  
  
-   La precisione di un valore letterale numerico esatto: il numero di cifre che contiene.  
  
-   La scala di un valore letterale numerico esatto: il numero di cifre a destra del periodo di espressa o implicito.  
  
-   La precisione di un valore letterale numerico approssimativo: la precisione del relativo mantissa.  
  
## <a name="character-source-to-numeric-target"></a>Carattere di origine alla destinazione numerica  
 Di seguito sono le regole per la conversione da una fonte di carattere (CS) in una destinazione numerica (NT):  
  
1.  Sostituire CS con il valore ottenuto rimuovendo gli spazi iniziali o finali in CS. Se non è valida. CS *letterali numerici*, viene restituito l'errore SQLSTATE 22018 (valore di carattere non valido per la specifica del cast).  
  
2.  Sostituire CS con il valore ottenuto rimuovendo gli zeri iniziali prima del separatore decimale, finali zeri dopo il separatore decimale, o entrambi.  
  
3.  Convertire CS NT. Se la conversione comporta la perdita di cifre significative, viene restituito l'errore SQLSTATE 22003 (valore numerico non compreso nell'intervallo). Se la conversione comporta la perdita di cifre non significative, di errore SQLSTATE 01S07 (troncamento frazionario) viene restituito.  
  
## <a name="numeric-source-to-character-target"></a>Numerici di origine alla destinazione di caratteri  
 Di seguito sono le regole per la conversione da un'origine numerica (NS) a una destinazione di caratteri (CT):  
  
1.  Si supponga che LT sia la lunghezza in caratteri del CT Per l'assegnazione di recupero, LT è uguale alla lunghezza del buffer in caratteri meno il numero di byte in carattere di terminazione null per questo set di caratteri.  
  
2.  Casi:  
  
    -   Se NS è un tipo numerico esatto, quindi consentire YP il più breve stringa di caratteri che è conforme alla definizione di è uguale *letterale numerico esatto* in modo che la scala di YP è quello utilizzato per la scala del servizio NS e il valore di YP interpretato è la valore assoluto di NS.  
  
    -   Se NS è un tipo numerico approssimato, quindi consentire YP essere una stringa di caratteri come indicato di seguito:  
  
         Caso:  
  
         Se NS è uguale a 0, YP è 0.  
  
         Consentire a essere il più breve stringa di caratteri che è conforme alla definizione dell'esatta - YSN*letterali numerici* e il cui valore interpretato è il valore assoluto di NS. Se la lunghezza di YSN è minore di (*precisione* + 1) del tipo di dati di NS, quindi consentire YP YSN è uguale.  
  
         In caso contrario, YP è il più breve stringa di caratteri che è conforme alla definizione della *letterali numerici approssimati* il cui valore interpretato è il valore assoluto di NS e la cui proprietà *mantissa* è costituito da un singolo *cifra* vale a dire non '0', seguito da un *periodo* e un *unsigned integer*.  
  
3.  Caso:  
  
    -   Se NS è minore di 0, quindi consentire Y essere il risultato di:  
  
         '-' &AMP;#124; &AMP;#124; YP  
  
         dove '&#124;&#124;' è l'operatore di concatenazione di stringhe.  
  
         In caso contrario, lasciare Y YP è uguale.  
  
4.  Si supponga LY sia la lunghezza in caratteri di Y.  
  
5.  Caso:  
  
    -   Se è uguale a LY LT, CT viene impostato su Y.  
  
    -   Se SO è inferiore a lungo termine, quindi CT è impostato su Y estesi a destra per il numero appropriato di spazi.  
  
         In caso contrario (LY > LT), copiarne i primi caratteri LT di Y CT  
  
         Caso:  
  
         Se si tratta di un'assegnazione di archivio, restituire l'errore SQLSTATE 22001 (dati String, troncati a destra).  
  
         Se si tratta di assegnazione di recupero, restituire il messaggio di avviso SQLSTATE 01004 (dati String, troncati a destra). Quando la copia comporta la perdita di cifre frazionarie (diverso da zero finali), è definito dal driver se si verifica una delle operazioni seguenti:  
  
         (1) il driver tronca la stringa y a una scala appropriata (che può essere anche zero) e scrive il risultato in CT  
  
         (2) il driver viene arrotondata la stringa y a una scala appropriata (che può essere anche zero) e scrive il risultato in CT  
  
         (3) il driver né tronca né Arrotonda ma copia solo i primi caratteri LT di Y nella CT
