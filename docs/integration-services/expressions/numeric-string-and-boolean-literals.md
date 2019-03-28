---
title: Valori letterali (SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- string literals
- numeric literals [Integration Services]
- Boolean literals
- expressions [Integration Services], literals
- literals [Integration Services]
- mapping literals [Integration Services]
ms.assetid: a980cd52-54ef-4b9c-b00c-e6807cf8e01f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d4b6dec2cd9698d347ca247e26f4b931cb6ab56d
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/20/2019
ms.locfileid: "58279165"
---
# <a name="numeric-string-and-boolean-literals"></a>Valori letterali numerici, stringa e booleani
 Le espressioni possono includere valori letterali numerici, stringa e booleani. L'analizzatore di espressioni supporta un'ampia gamma di valori letterali numerici, quali costanti intere, decimali e a virgola mobile. Supporta inoltre i suffissi per valori di tipo long e float, che specificano come gestire tali valori, e la notazione scientifica nei valori letterali numerici.  
  
## <a name="numeric-literals"></a>Valori letterali numerici  
 L'analizzatore di espressioni supporta tipi di dati numerici integrali e non integrali. Supporta inoltre gli identificatori di derivazione, ossia gli identificatori numerici univoci per gli elementi dei pacchetti. Gli identificatori di derivazione sono numeri, ma non possono essere utilizzati nelle operazioni matematiche.  
  
 L'analizzatore di espressioni supporta i suffissi, che consentono di indicare come gestire i valori letterali numerici. Per indicare ad esempio che il numero intero 37 deve essere gestito come un tipo di dati long integer, è possibile specificare 37L o 37l.  
  
 I suffissi per i valori letterali numerici sono elencati nella tabella seguente.  
  
|Suffisso|Descrizione|  
|------------|-----------------|  
|L o l|Valore letterale numerico long.|  
|U o u|Valore letterale numerico senza segno.|  
|E o e|Esponente, nella notazione scientifica.|  
  
 Nella tabella seguente sono elencati gli elementi delle espressioni numeriche e le rispettive espressioni regolari.  
  
|Elemento dell'espressione|Espressione regolare‏|Descrizione|  
|------------------------|------------------------|-----------------|  
|Cifra espressa come D.|[0-9]|Qualsiasi cifra.|  
|Notazione scientifica espressa come E.|[Ee][+-]?{D}+|E maiuscola o minuscola, + o - facoltativo e una o più cifre come definito in D.|  
|Suffisso per valori di tipo Integer espresso come IS.|(([lL]?[uU]?)&#124;([uU]?[lL]?))|Facoltativamente, u e l maiuscole o minuscole o una combinazione di u e l. U o u indica un valore senza segno. L o l indica un valore di tipo long.|  
|Suffisso per valori di tipo float espresso come FS.|([f&#124;F]&#124;[l&#124;L])|f o l maiuscola o minuscola. F o f indica un valore float (tipo di dati DT_R4). L o l indica un valore di tipo long (tipo di dati DT_R8).|  
|Cifra esadecimale espressa come H.|[a-fA-F0-9]|Qualsiasi cifra esadecimale.|  
  
 Nella tabella seguente vengono descritti i valori letterali numerici validi nel linguaggio delle espressioni regolari.  
  
|Espressione regolare‏|Descrizione|  
|------------------------|-----------------|  
|{D}+{IS}|Valore letterale numerico integrale con almeno una cifra (D) e, facoltativamente, suffisso per valori di tipo long e/o per valori senza segno (IS).  Esempi: 457, 785u, 986L e 7945ul.|  
|{D}+{E}{FS}|Valore letterale numerico non integrale con almeno una cifra (D), notazione scientifica e suffisso per valori di tipo long o float.  Esempi: 4E8l, 13e-2f e 5E+L.|  
|{D}*"."{D}+{E}?{FS}|Valore letterale numerico non integrale con una cifra decimale, frazione decimale con almeno una cifra (D), esponente facoltativo (E) e identificatore di tipo float o long (FS). Questo valore letterale numerico ha tipo di dati DT_R4 o DT_R8.  Esempi: 6,45E3f, 0,89E-2l e 1,05E+7F.|  
|{D}+"."{D}*{E}?{FS}|Valore letterale numerico non integrale con almeno una cifra significativa (D), una cifra decimale, esponente (E) e un identificatore di tipo float o long (FS). Questo valore letterale numerico ha tipo di dati DT_R4 o DT_R8.  Esempi: 1,E-4f, 4,6E6L e 8,365E+2f.|  
|{D}*.{D}+|Valore letterale numerico non integrale con precisione e scala. Include una cifra decimale e una frazione decimale con almeno una cifra (D). Questo valore letterale numerico ha tipo di dati DT_NUMERIC.  Esempi: ,9, 5,8 e 0,346.|  
|{D}+.{D}*|Valore letterale numerico non integrale con precisione e scala. Include almeno una cifra significativa (D) e una cifra decimale. Questo valore letterale numerico ha tipo di dati DT_NUMERIC.  Esempi: 6., 0,2 e 8,.0.|  
|#{D}+|Identificatore di derivazione. È costituito dal simbolo di cancelletto (#) e da almeno una cifra (D). Esempi: #123.|  
|0[xX]{H}+{uU}|Valore letterale stringa in formato esadecimale. Include uno zero, una x maiuscola o minuscola, almeno una H maiuscola e, facoltativamente, il suffisso per valori senza segno. Esempi: 0xFF0A e 0X000010000U.|  
  
 Per altre informazioni sui tipi di dati utilizzati dall'analizzatore di espressioni, vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
 Le espressioni possono includere valori letterali numerici con tipi di dati diversi. Quando l'analizzatore di espressioni valuta espressioni di questo tipo, ne converte i dati in tipi compatibili. Per altre informazioni, vedere [Tipi di dati nelle espressioni di Integration Services](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
 La conversione tra alcuni tipi di dati richiede tuttavia un cast esplicito. L'analizzatore di espressioni dispone di un operatore cast per la conversione esplicita dei tipi di dati. Per altre informazioni, vedere [Cast &#40;espressione SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
### <a name="mapping-numeric-literals-to-integration-services-data-types"></a>Mapping tra valori letterali numerici e tipi di dati di Integration Services  
 Durante la valutazione dei valori letterali numerici l'analizzatore di espressioni esegue le conversioni seguenti:  
  
-   Per i valori letterali numerici integrali viene eseguito il mapping a tipi di dati Integer come indicato di seguito.  
  
    |Suffisso|Tipo di risultato|  
    |------------|-----------------|  
    |None|DT_I4|  
    |U|DT_UI4|  
    |L|DT_I8|  
    |UL|DT_UI8|  
  
    > **IMPORTANTE** Se non è specificato il suffisso per valori di tipo long (L o l), l'analizzatore di espressioni eseguirà il mapping dei valori con segno al tipo di dati DT_I4 e i valori senza segno al tipo di dati DT_UI4, anche se il valore causa un overflow del tipo di dati.  
  
-   I valori letterali numerici che includono un esponente vengono convertiti nel tipo di dati DT_R4 o DT_R8. Se l'espressione include il suffisso per valori di tipo long, verrà convertita nel tipo di dati DT_R8. Se include il suffisso per valori di tipo float, verrà convertita nel tipo di dati DT_R4.  
  
-   Se un valore letterale numerico non integrale include F o f, verrà mappato al tipo di dati DT_R4. Se include L o l e il numero è un intero, verrà mappato al tipo di dati DT_I8. Se è un numero reale, verrà mappato al tipo di dati DT_R8. Se include il suffisso per valori di tipo long, verrà convertito nel tipo di dati DT_R8.  
  
-   I valori letterali numerici non integrali con precisione e scala vengono mappati al tipo di dati DT_NUMERIC.  
  
## <a name="string-literals"></a>Valori letterali stringa  
 I valori letterali stringa devono essere racchiusi tra virgolette. Il linguaggio delle espressioni include un set di sequenze di escape per i caratteri di escape più comuni, quali i caratteri non stampabili e le virgolette.  
  
 Un valore letterale stringa è costituito da zero o più caratteri racchiusi tra virgolette. Se nella stringa sono presenti virgolette, dovranno essere precedute da un carattere di escape affinché l'espressione possa essere analizzata. Nelle stringhe sono ammessi tutti i caratteri di due byte, a eccezione di \x0000, che è il terminatore Null delle stringhe.  
  
 Le stringhe possono includere altri caratteri che richiedono una sequenza di escape. Le sequenze di escape per i valori letterali stringa sono elencate nella tabella seguente.  
  
|Sequenza di escape|Descrizione|  
|---------------------|-----------------|  
|\a|Avviso|  
|\b|Backspace|  
|\f|Avanzamento carta|  
|\n|Nuova riga|  
|\r|Ritorno a capo|  
|\t|Tabulazione orizzontale|  
|\v|Tabulazione verticale|  
|\\"|Virgoletta|  
|\\\|Barra rovesciata|  
|\xhhhh|Carattere Unicode in notazione esadecimale|  
  
## <a name="boolean-literals"></a>Valori letterali booleani  
 L'analizzatore di espressioni supporta i valori letterali booleani soliti: **True** e **False**. L'analizzatore di espressioni non fa distinzione tra maiuscole e minuscole ed è pertanto possibile utilizzare qualsiasi combinazione di maiuscole e minuscole. Ad esempio, è possibile utilizzare indifferentemente TRUE o True.  
  
> **NOTA:** Nelle espressioni i valori letterali booleani devono essere delimitati da spazi.  
  
  
