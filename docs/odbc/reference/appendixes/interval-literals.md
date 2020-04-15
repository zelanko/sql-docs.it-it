---
title: Valori letterali di intervallo Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c1761ac0acb57b3f375a7d19e9371384c000eca5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304942"
---
# <a name="interval-literals"></a>Valori letterali intervallo
ODBC richiede che tutti i driver supportino la conversione del tipo di dati SQL_CHAR o SQL_VARCHAR in tutti i tipi di dati dell'intervallo C. Se l'origine dati sottostante non supporta i tipi di dati intervallo, tuttavia, il driver deve conoscere il formato corretto del valore nel campo SQL_CHAR per supportare queste conversioni. Analogamente, ODBC richiede che qualsiasi tipo C ODBC sia convertibile in SQL_CHAR o SQL_VARCHAR, pertanto un driver deve sapere quale formato deve avere un intervallo archiviato nel campo carattere. In questa sezione viene descritta la sintassi dei valori letterali di intervallo, che il writer del driver deve utilizzare per convalidare i campi SQL_CHAR durante la conversione in uno o dall'intervallo C.  
  
> [!NOTE]  
>  La sintassi BNF completa per i valori letterali di intervallo è illustrata nella sezione [Sintassi dei valori letterali](../../../odbc/reference/appendixes/interval-literal-syntax.md) di intervallo nell'Appendice C: Grammatica SQL.  
  
 Per passare valori letterali di intervallo come parte di un'istruzione SQL, viene definita una sintassi della clausola di escape per i valori letterali di intervallo. Per ulteriori informazioni, vedere [Valori letterali di data, ora e timestamp](../../../odbc/reference/develop-app/date-time-and-timestamp-literals.md).  
  
 Un valore letterale intervallo ha la forma seguente:  
  
```  
INTERVAL[<sign>] 'value' <interval qualifier>  
```  
  
 dove "INTERVAL" indica che il valore letterale carattere è un intervallo. Il segno può essere più o meno; è al di fuori della stringa di intervallo ed è facoltativo.  
  
 Il qualificatore intervallo può essere un singolo campo datetime o essere \<composto da \<due campi datetime, nel formato: *campo iniziale*> a campo *finale*>.  
  
-   Quando l'intervallo è composto da un singolo campo, il singolo campo può essere un campo non secondario che può essere accompagnato da una precisione iniziale facoltativa tra parentesi. Il singolo campo datetime può anche essere un secondo campo che può essere accompagnato dalla precisione iniziale facoltativa, dalla precisione facoltativa dei secondi frazionari tra parentesi o da entrambi. Se per un campo secondi sono presenti sia una precisione iniziale che una precisione frazionaria secondi, sono separate da virgole. Se il campo dei secondi ha una precisione frazionaria-secondi, deve avere anche una precisione iniziale.  
  
-   Quando l'intervallo è composto da campi iniziali e finali, il campo iniziale è un campo non secondario che può essere accompagnato dalla precisione del campo iniziale dell'intervallo tra parentesi. Il campo finale può essere un campo non di secondo o un secondo campo che può essere accompagnato da un intervallo frazionario secondi precisione tra parentesi.  
  
 La stringa di intervallo in *value* è racchiusa tra virgolette singole. Può essere un valore letterale anno-mese o un valore letterale giorno-ora. Il formato della stringa in *value* è determinato dalle regole seguenti:  
  
-   La stringa contiene un valore decimale per ogni \<campo implicito dal *qualificatore* *intervallo*>.  
  
-   Se la precisione dell'intervallo include i campi ANNO e MESE, i valori di questi campi sono separati da un segno meno.  
  
-   Se la precisione dell'intervallo include i campi GIORNO e ORA, i valori di questi campi sono separati da uno spazio.  
  
-   Se la precisione dell'intervallo include il campo HOUR e i campi dell'ordine inferiore (MINUTE e SECOND), i valori di questi campi sono separati da due punti.  
  
-   Se la precisione dell'intervallo include un campo SECOND e la precisione espressa o implicita dei secondi è diversa da zero, il carattere immediatamente prima della prima cifra della parte frazionaria del secondo è un punto.  
  
-   Nessun campo può avere più di due cifre, ad eccezione di:  
  
    -   Il valore del campo iniziale può essere lungo quanto la precisione di interlinea dell'intervallo espressa o implicita.  
  
    -   La parte frazionaria del campo SECOND può essere lunga quanto la precisione espressa o implicita dei secondi.  
  
    -   I campi finali seguono i vincoli abituali del calendario gregoriano. (Vedere [Vincoli del calendario gregoriano](../../../odbc/reference/appendixes/constraints-of-the-gregorian-calendar.md).  
  
 Nella tabella seguente sono elencati esempi di valori letterali di intervallo validi inclusi nella clausola di escape ODBC per gli intervalli. La sintassi della clausola escape è la seguente:  
  
> [!NOTE]  
>  *-INTERVAL-string-qualifier del segno INTERVAL-string*  
  
|Clausola di escape letterale|Intervallo specificato|  
|---------------------------|------------------------|  
|"INTERVAL '326' ANNO(4)|Specifica un intervallo di 326 anni. La precisione di interlinea dell'intervallo è 4.|  
|"INTERVAL '326' mese(3)|Specifica un intervallo di 326 mesi. La precisione di interlinea dell'intervallo è 3.The interval leading precision is 3.|  
|INTERVALLO '3261' GIORNO(4)|Specifica un intervallo di 3261 giorni. La precisione di interlinea dell'intervallo è 4.|  
|INTERVAL '163' ORA(3)|Specifica un intervallo di 163 giorni. La precisione di interlinea dell'intervallo è 3.The interval leading precision is 3.|  
|INTERVALLO '163' MINUTI(3)|Specifica un intervallo di 163 minuti. La precisione di interlinea dell'intervallo è 3.The interval leading precision is 3.|  
|INTERVALLO '223.16' secondo(3,2)|Specifica un intervallo di 223,16 secondi. La precisione di interlinea dell'intervallo è 3 e la precisione dei secondi è 2.The interval leading precision is 3 and the seconds precision is 2.|  
|INTERVALLO '163-11' ANNO(3) AL MESE|Specifica un intervallo di 163 anni e 11 mesi. La precisione di interlinea dell'intervallo è 3.The interval leading precision is 3.|  
|INTERVALLO '163 12' GIORNO(3) ALL'ORA|Specifica un intervallo di 163 giorni e 12 ore. La precisione di interlinea dell'intervallo è 3.The interval leading precision is 3.|  
|INTERVALLO '163 12:39' GIORNO(3) A MINUTO|Specifica un intervallo di 163 giorni, 12 ore e 39 minuti. La precisione di interlinea dell'intervallo è 3.The interval leading precision is 3.|  
|INTERVALLO '163 12:39:59.163' GIORNO(3) AL SECONDO(3)|Specifica un intervallo di 163 giorni, 12 ore, 39 minuti e 59,163 secondi. La precisione di interlinea dell'intervallo è 3 e la precisione dei secondi è 3.The interval leading precision is 3 and the seconds precision is 3.|  
|INTERVALLO '163:39' ORA(3) A MINUTO|Specifica un intervallo di 163 ore e 39 minuti. La precisione di interlinea dell'intervallo è 3.The interval leading precision is 3.|  
|INTERVALLO '163:39:59.163' ORA(3) A SECONDO(4)|Specifica un intervallo di 163 ore, 39 minuti e 59,163 secondi. La precisione di interlinea dell'intervallo è 3 e la precisione dei secondi è 4.The interval leading precision is 3 and the seconds precision is 4.|  
|INTERVALLO '163:59.163' MINUTO(3) AL SECONDO(5)|Specifica un intervallo di 163 minuti e 59,163 secondi. La precisione di interlinea dell'intervallo è 3 e la precisione dei secondi è 5.The interval leading precision is 3 and the seconds precision is 5.|  
|INTERVALLO -'16 23:39:56.23' DAL GIORNO AL SECONDO|Specifica un intervallo di meno 16 giorni, 23 ore, 39 minuti e 56,23 secondi. La precisione iniziale implicita è 2 e la precisione implicita dei secondi è 6.|  
  
 Nella tabella seguente sono elencati esempi di valori letterali di intervallo non validi:The following table lists examples of invalid interval literals:  
  
|Clausola di escape letterale|Motivo per cui non è valido|  
|---------------------------|------------------------|  
|INTERVAL '163' HOUR(2)|La precisione di interlinea dell'intervallo è 2, ma il valore del campo iniziale è 163.|  
|INTERVALLO '223.16' secondo(2,2)<br /><br /> INTERVALLO '223.16' secondo(3,1)|Nel primo esempio, la precisione iniziale è troppo piccola e nel secondo esempio la precisione dei secondi è troppo piccola.|  
|Secondo INTERVALLO '223.16'<br /><br /> "INTERVAL '223' ANNO"|Poiché la precisione iniziale non è specificata, il valore predefinito è 2, che è troppo piccolo per contenere il valore letterale specificato.|  
|Secondo INTERVALLO '22.1234567'|La precisione dei secondi non è specificata, pertanto il valore predefinito è 6.The seconds precision is unspecified, so it defaults to 6. Il valore letterale ha sette cifre dopo il separatore decimale.|  
|INTERVALLO '163-13' ANNO(3) AL MESE<br /><br /> INTERVALLO '163 65' GIORNO(3) ALL'ORA<br /><br /> INTERVALLO '163 62:39' GIORNO(3) A MINUTO<br /><br /> INTERVALLO '163 12:125:59.163' giorno(3) AL SECONDO(3)<br /><br /> INTERVALLO '163:144' ORA(3) A MINUTO<br /><br /> INTERVALLO '163:567:234.163' ORA(3) A SECONDO(4)<br /><br /> INTERVALLO '163:591.163' MINUTO(3) AL SECONDO(5)|Il campo finale non segue le regole del calendario gregoriano.|
