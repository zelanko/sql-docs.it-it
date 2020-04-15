---
title: Regole per le conversioni Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c49177d62fffc3b3b5c47a25bf3fb421d7564245
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305087"
---
# <a name="rules-for-conversions"></a>Regole per le conversioni
Le regole in questa sezione si applicano per le conversioni che coinvolgono valori letterali numerici. Ai fini di queste regole, sono definiti i seguenti termini:  
  
-   *Assegnazione del negozio:* Quando si inviano dati in una colonna di tabella in un database. Ciò si verifica durante le chiamate a **SQLExecute**, **SQLExecDirect**e **SQLSetPos**. Durante l'assegnazione dell'archivio, "destinazione" si riferisce a una colonna di database e "origine" si riferisce ai dati nei buffer dell'applicazione.  
  
-   *Assegnazione recupero:* Quando si recuperano dati dal database in buffer dell'applicazione. Ciò si verifica durante le chiamate a **SQLFetch**, **SQLGetData**, **SQLFetchScroll**e **SQLSetPos**. Durante l'assegnazione di recupero, "destinazione" si riferisce ai buffer dell'applicazione e "origine" si riferisce alla colonna del database.  
  
-   *CS:* Valore nell'origine del carattere.  
  
-   *NT:* Valore nella destinazione numerica.  
  
-   *NS:* Valore nell'origine numerica.  
  
-   *CT:* Valore nella destinazione del carattere.  
  
-   Precisione di un valore letterale numerico esatto: il numero di cifre che contiene.  
  
-   La scala di un valore letterale numerico esatto: il numero di cifre a destra del periodo espresso o implicito.  
  
-   La precisione di un valore letterale numerico approssimativo: la precisione della sua mantissa.  
  
## <a name="character-source-to-numeric-target"></a>Origine carattere alla destinazione numerica  
 Di seguito sono riportate le regole per la conversione da un'origine di caratteri (CS) a una destinazione numerica (NT):  
  
1.  Sostituire CS con il valore ottenuto rimuovendo eventuali spazi iniziali o finali in CS. Se CS non è un *valore letterale numerico*valido, viene restituito SQLSTATE 22018 (valore carattere non valido per la specifica cast).  
  
2.  Sostituire CS con il valore ottenuto rimuovendo gli zeri iniziali prima del separatore decimale, gli zeri finali dopo il separatore decimale o entrambi.  
  
3.  Convertire CS in NT. Se la conversione comporta una perdita di cifre significative, viene restituito SQLSTATE 22003 (valore numerico non compreso nell'intervallo). Se la conversione comporta la perdita di cifre non significative, viene restituito SQLSTATE 01S07 (troncamento frazionario).  
  
## <a name="numeric-source-to-character-target"></a>Origine numerica a destinazione carattereNumeric Source to Character Target  
 Di seguito sono riportate le regole per la conversione da un'origine numerica (NS) a una destinazione carattere (CT):Following are the rules for converting from a numeric source (NS) to a character target (CT):  
  
1.  Sia LT la lunghezza in caratteri di CT. Per l'assegnazione di recupero, LT è uguale alla lunghezza del buffer in caratteri meno il numero di byte nel carattere di terminazione null per questo set di caratteri.  
  
2.  Casi:  
  
    -   Se NS è un tipo numerico esatto, quindi lasciare YP uguale alla stringa di caratteri più breve che è conforme alla definizione di *esatto-numerico-letterale* in modo che la scala di YP è la stessa della scala di NS e il valore interpretato di YP è il valore assoluto di NS.  
  
    -   Se NS è un tipo numerico approssimativo, quindi lasciare YP essere una stringa di caratteri come segue:  
  
         Maiuscole/minuscole:  
  
         Se NS è uguale a 0, allora YP è 0.  
  
         Che YSN sia la stringa di caratteri più breve conforme alla definizione di exact*numeric-literal* e il cui valore interpretato è il valore assoluto di NS. Se la lunghezza di YSN è minore di (*precisione* 1) del tipo di dati di NS, quindi lasciare YP uguale a YSN.  
  
         In caso contrario, YP è la stringa di caratteri più breve conforme alla definizione di *approssimativo-numerico-letterale* il cui valore interpretato è il valore assoluto di NS e la cui *mantissa* è costituita da una singola *cifra* diversa da '0', seguita da un *punto* e da un *unsigned-integer*.  
  
3.  Maiuscole/minuscole:  
  
    -   Se NS è minore di 0, allora lasciate che Y sia il risultato di:  
  
         '-' &#124;&#124; YP  
  
         dove '&#124;&#124;' è l'operatore di concatenazione di stringhe.  
  
         In caso contrario, lasciare Y uguale YP.  
  
4.  Lasciate che LY sia la lunghezza in caratteri di Y.  
  
5.  Maiuscole/minuscole:  
  
    -   Se LY è uguale a LT, CT è impostato su Y.  
  
    -   Se LY è minore di LT, CT viene impostato su Y esteso a destra in base al numero appropriato di spazi.  
  
         In caso contrario (LY > LT), copiare i primi caratteri LT di Y in CT.  
  
         Maiuscole/minuscole:  
  
         Se si tratta di un'assegnazione di archivio, restituire l'errore SQLSTATE 22001 (dati stringa troncati a destra).  
  
         Se si tratta di assegnazione di recupero, restituire l'avviso SQLSTATE 01004 (dati stringa troncati a destra). Quando la copia comporta la perdita di cifre frazionarie (diversi dagli zeri finali), è definito dal driver se si verifica una delle seguenti condizioni:  
  
         (1) Il driver tronca la stringa in Y in una scala appropriata (che può anche essere zero) e scrive il risultato in CT.  
  
         (2) Il conducente arrotonda la stringa in Y a una scala appropriata (che può anche essere zero) e scrive il risultato in CT.  
  
         (3) Il conducente non tronca né arrotonda, ma copia solo i primi caratteri LT di Y in CT.
