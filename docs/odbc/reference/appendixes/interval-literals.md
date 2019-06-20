---
title: Valori letterali intervallo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], interval data types
- interval literals [ODBC]
- interval data type [ODBC], literals
ms.assetid: f9e6c3c7-4f98-483f-89d8-ebc5680f021b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc5d09bca83724bb956d39512c51c3dc47db1bad
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63188812"
---
# <a name="interval-literals"></a>Valori letterali intervallo
ODBC è necessario che tutti i driver supportano la conversione del tipo di dati SQL_CHAR o SQL_VARCHAR a tutti i tipi di dati di intervallo C. Se l'origine dati sottostante non supporta tipi di dati di intervallo, tuttavia, il driver deve conoscere il formato corretto del valore nel campo SQL_CHAR per supportare queste conversioni. Analogamente, ODBC richiede che deve disporre di qualsiasi tipo di essere convertibile in SQL_CHAR o SQL_VARCHAR, in modo che un driver deve sapere quale formato di un intervallo archiviato nel campo carattere dati ODBC C. In questa sezione viene descritta la sintassi dei valori letterali di intervallo, che scrive il driver deve utilizzare per convalidare i campi SQL_CHAR durante la conversione da o verso tipi di dati di intervallo C.  
  
> [!NOTE]  
>  La sintassi BNF completa per i valori letterali intervallo viene visualizzata nella sezione [sintassi dei valori letterali intervallo](../../../odbc/reference/appendixes/interval-literal-syntax.md) nell'appendice c: Grammatica SQL.  
  
 Per passare valori letterali di intervallo come parte di un'istruzione SQL, una sintassi della clausola di escape è definita per i valori letterali intervallo. Per altre informazioni, vedere [Date, Time e Timestamp valori letterali](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md).  
  
 Un intervallo di valori letterale è nel formato:  
  
```  
INTERVAL[<sign>] 'value' <interval qualifier>  
```  
  
 dove "INTERVAL" indica che il valore letterale carattere è un intervallo. Può essere il segno più o meno; è di fuori della stringa di intervallo ed è facoltativo.  
  
 Il qualificatore di intervallo può essere un campo datetime singolo o essere costituita da due campi di data/ora, nel formato: \< *campo iniziale*> TO \< *campo finale*>.  
  
-   Quando l'intervallo è costituita da un singolo campo, il singolo campo può essere un campo non secondi che può essere accompagnato da un valore di precisione iniziale facoltativo racchiuso tra parentesi. Il campo datetime singolo può essere anche un secondo campo che può essere accompagnato dalla precisione iniziale facoltativa, la precisione secondi frazionari facoltativo racchiuso tra parentesi o entrambi. Se sono presenti per un campo secondi sia una precisione iniziale e una precisione in secondi frazionari, sono separati da virgole. Se il campo secondi ha una precisione in secondi frazionari, è necessario che abbia una precisione iniziale.  
  
-   Quando l'intervallo è costituita da campi iniziali e finali, il campo iniziale è un campo non secondi che può essere accompagnato dall'intervallo di precisione campo iniziale racchiuso tra parentesi. Il campo finale può essere un campo non secondi o a un secondo campo che può essere accompagnato da un intervallo di precisione in secondi frazionari racchiuso tra parentesi.  
  
 La stringa di intervallo nella *valore* è racchiuso tra virgolette singole. Può essere un valore letterale anno-mese o un valore letterale / ora. Il formato della stringa contenuta *valore* è determinato dalle seguenti regole:  
  
-   La stringa contiene un valore decimale per ogni campo che è implicita il \< *interval* *qualificatore*>.  
  
-   Se l'intervallo di precisione include i campi con anno e mese, i valori di questi campi sono separati da un segno meno (-).  
  
-   Se l'intervallo di precisione include i campi giorno e ora, i valori di questi campi sono separati da uno spazio.  
  
-   Se l'intervallo di precisione include ora il campo e i campi di ordine inferiore (minuto e secondo), i valori di questi campi sono separati dai due punti.  
  
-   Se l'intervallo di precisione include un secondo campo e la precisione dei secondi espressa o implicita è diverso da zero, il carattere immediatamente prima della prima cifra della parte frazionaria del secondo è un punto.  
  
-   Nessun campo può essere più di due cifre lunghi, ad eccezione di:  
  
    -   Il valore del campo iniziale può essere, purché l'intervallo espressa o implicita precisione iniziale.  
  
    -   La parte frazionaria del secondo campo può essere fin quando la precisione dei secondi espressa o implicita.  
  
    -   I campi finali seguono i normali vincoli del calendario gregoriano. (Vedere [vincoli del calendario gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md).)  
  
 Nella tabella seguente sono elencati esempi di valori letterali intervallo valido incluso nella clausola di escape ODBC per gli intervalli. La sintassi della clausola di escape è come segue:  
  
> [!NOTE]  
>  *{INTERVALLO sign intervallo-intervallo-qualificatore della stringa}*  
  
|Valore letterale clausola di escape|Intervallo specificato|  
|---------------------------|------------------------|  
|{YEAR(4) INTERVALLO '326'}|Specifica un intervallo di anni 326. L'intervallo di precisione iniziale è 4.|  
|{MONTH(3) INTERVALLO '326'}|Specifica un intervallo di mesi 326. L'intervallo di precisione iniziale è 3.|  
|{DAY(4) INTERVALLO '3261'}|Specifica un intervallo di giorni 3261. L'intervallo di precisione iniziale è 4.|  
|{HOUR(3) INTERVALLO '163'}|Specifica un intervallo di giorni 163. L'intervallo di precisione iniziale è 3.|  
|{MINUTE(3) INTERVALLO '163'}|Specifica un intervallo di minuti 163. L'intervallo di precisione iniziale è 3.|  
|{SECOND(3,2) INTERVALLO '223.16'}|Specifica un intervallo di 223.16 secondi. L'intervallo di precisione iniziale è 3 e la precisione dei secondi è 2.|  
|{INTERVALLO ' 163-11' YEAR(3) AL MESE}|Specifica un intervallo di 163 anni e 11 mesi. L'intervallo di precisione iniziale è 3.|  
|{INTERVALLO 163 ' 12' DAY(3) ORA}|Specifica un intervallo di 163 giorni e 12 ore. L'intervallo di precisione iniziale è 3.|  
|{INTERVALLO ' 163 12:39 ' DAY(3) AL MINUTO}|Specifica un intervallo di 163 giorni, 12 ore e 39 minuti. L'intervallo di precisione iniziale è 3.|  
|{DAY(3) INTERVALLO '12:39:59.163 163' PER SECOND(3)}|Specifica un intervallo di 163 giorni, 12 ore, 39 minuti e 59.163 secondi. L'intervallo di precisione iniziale è 3 e la precisione dei secondi è 3.|  
|{INTERVALLO '163:39' HOUR(3) AL MINUTO}|Specifica un intervallo di 163 ore e 39 minuti. L'intervallo di precisione iniziale è 3.|  
|{INTERVALLO '163:39:59.163' HOUR(3) A SECOND(4)}|Specifica un intervallo di 163 ore, 39 minuti e 59.163 secondi. L'intervallo di precisione iniziale è 3 e la precisione dei secondi è 4.|  
|{INTERVALLO '163:59.163' MINUTE(3) A SECOND(5)}|Specifica un intervallo di 163 minuti e 59.163 secondi. L'intervallo di precisione iniziale è 3 e la precisione dei secondi è 5.|  
|{INTERVAL - DAY '16 23:39:56.23' SECONDO}|Specifica un intervallo di meno 16 giorni, 23 ore, 39 minuti e 56.23 secondi. La precisione iniziale implicita è 2 e la precisione dei secondi implicita è 6.|  
  
 Nella tabella seguente sono elencati esempi di valori letterali di intervallo non valido:  
  
|Valore letterale clausola di escape|Motivo il motivo per cui non è valido|  
|---------------------------|------------------------|  
|{HOUR(2) INTERVALLO '163'}|L'intervallo di precisione iniziale è 2, ma il valore del campo iniziale è 163.|  
|{SECOND(2,2) INTERVALLO '223.16'}<br /><br /> {SECOND(3,1) INTERVALLO '223.16'}|Nel primo esempio, la precisione iniziale è troppo piccola, e nel secondo esempio, la precisione dei secondi è troppo piccola.|  
|{INTERVALLO '223.16' SECONDO}<br /><br /> {'223' INTERVALLO ANNO}|Poiché la precisione iniziale non è specificata, per impostazione predefinita a 2, che è troppo piccolo per contenere il valore letterale specificato.|  
|{INTERVALLO '22.1234567' SECONDO}|La precisione dei secondi non è specificata, in modo che l'impostazione predefinita è 6. Il valore letterale presenta sette cifre dopo il separatore decimale.|  
|{INTERVALLO ' 163-13. ' YEAR(3) AL MESE}<br /><br /> {INTERVALLO ' 163 65' DAY(3) ORA}<br /><br /> {DAY(3) INTERVALLO '62:39 163' AL MINUTO}<br /><br /> {DAY(3) INTERVALLO '12:125:59.163 163' PER SECOND(3)}<br /><br /> {INTERVALLO '163:144' HOUR(3) AL MINUTO}<br /><br /> {INTERVALLO '163:567:234.163' HOUR(3) A SECOND(4)}<br /><br /> {INTERVALLO '163:591.163' MINUTE(3) A SECOND(5)}|Il campo finale non segue le regole del calendario gregoriano.|
