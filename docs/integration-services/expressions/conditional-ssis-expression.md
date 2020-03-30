---
title: '? : (condizionale) (espressione SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- conditional operator (?:)
- '?: (conditional operator)'
ms.assetid: d38e6890-7338-4ce0-a837-2dbb41823a37
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 758cd90c3932d59e725f6a8a9bf829e59ecf5474
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "71290170"
---
# <a name="--conditional-ssis-expression"></a>? : (condizionale) (espressione SSIS)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Viene restituita una di due espressioni in base alla valutazione di un'espressione booleana. Se l'espressione booleana restituisce TRUE, verrà valutata la prima espressione e il risultato sarà il risultato di tale espressione. Se l'espressione booleana restituisce FALSE, verrà valutata la seconda espressione e il risultato sarà il risultato di tale espressione.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
boolean_expression?expression1:expression2  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *boolean_expression*  
 Qualsiasi espressione valida che restituisce TRUE, FALSE o NULL.  
  
 *expression1*  
 È qualsiasi espressione valida.  
  
 *expression2*  
 È qualsiasi espressione valida.  
  
## <a name="result-types"></a>Tipi restituiti  
 Il tipo di dati *expression1* o *expression2*.  
  
## <a name="remarks"></a>Osservazioni  
 Se *boolean_expression* restituisce NULL, il risultato dell'espressione sarà NULL. Se un'espressione selezionata, *expression1* o *expression2* è NULL, il risultato sarà NULL. Se l'espressione selezionata non è NULL, ma quella non selezionata è NULL, il risultato sarà il valore dell'espressione selezionata.  
  
 Se *expression1* e *expression2* hanno lo stesso tipo di dati, anche il risultato sarà di tale tipo. Ai tipi di risultato si applicano le seguenti ulteriori regole:  
  
-   Il tipo di dati DT_TEXT richiede che *expression1* e *expression2* abbiano la stessa tabella codici.  
  
-   La lunghezza di un risultato con tipo di dati DT_BYTES corrisponde a quella dell'argomento più lungo.  
  
 Il set di espressioni, *expression1* e *expression2*, deve restituire tipi di dati validi e seguire una di queste regole:  
  
-   **Numeric** Sia *expression1* che *expression2* devono essere un tipo di dati numerici. L'intersezione dei tipi di dati deve essere un tipo di dati numeric come specificato dalle regole relative alle conversioni numeriche implicite eseguite dall'analizzatore di espressioni. L'intersezione dei due tipi di dati numeric non può essere Null. Per altre informazioni, vedere [Tipi di dati nelle espressioni di Integration Services](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
-   **String** Sia *expression1* che *expression2* devono avere un tipo di dati string, ovvero DT_STR o DT_WSTR. Le due espressioni possono restituire tipi di dati string diversi. Il risultato ha tipo di dati DT_WSTR e lunghezza pari a quella dell'argomento più lungo.  
  
-   **Date, Time o Date/Time** Sia *expression1* che *expression2* devono restituire uno dei tipi di dati seguenti: DT_DBDATE, DT_DATE, DT_DBTIME, DT_DBTIME2, DT_DBTIMESTAMP, DT_DBTIMESTAMP2, DT_DBTIMESTAPMOFFSET o DT_FILETIME.  
  
    > [!NOTE]  
    >  Il sistema non supporta i confronti tra un'espressione che restituisce un tipo di dati di ora e un'espressione che restituisce una data o un tipo di dati di data/ora. Viene generato un errore.  
  
     In caso di confronto delle espressioni, vengono applicate le regole di conversione seguenti nell'ordine elencato:  
  
    -   Quando le due espressioni restituiscono lo stesso tipo di dati, viene effettuato un confronto del tipo di dati.  
  
    -   Se un'espressione è un tipo di dati DT_DBTIMESTAMPOFFSET, l'altra espressione viene convertita implicitamente in DT_DBTIMESTAMPOFFSET e viene eseguito un confronto DT_DBTIMESTAMPOFFSET. Per altre informazioni, vedere [Tipi di dati nelle espressioni di Integration Services](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
    -   Se un'espressione è un tipo di dati DT_DBTIMESTAMP2, l'altra espressione viene convertita implicitamente in DT_DBTIMESTAMP2 e viene eseguito un confronto DT_DBTIMESTAMP2.  
  
    -   Se un'espressione è un tipo di dati DT_DBTIME2, l'altra espressione viene convertita implicitamente in DT_DBTIME2 e viene eseguito un confronto DT_DBTIME2.  
  
    -   Se un'espressione è di un tipo diverso da DT_DBTIMESTAMPOFFSET, DT_DBTIMESTAMP2 o DT_DBTIME2, le espressioni vengono convertite nel tipo di dati DT_DBTIMESTAMP prima del confronto.  
  
     In caso di confronto delle espressioni, il sistema presuppone quanto segue:  
  
    -   Se ogni espressione è un tipo di dati che include secondi frazionari, il sistema presuppone che il tipo di dati con il numero di cifre più basso per secondi frazionari presenti un valore pari a zero per le cifre rimanenti.  
  
    -   Se ogni espressione è un tipo di dati relativo alla data, ma solo una dispone di una differenza di fuso orario, il sistema presuppone che il tipo di dati senza la differenza di fuso orario sia espresso in formato UTC (Coordinated Universal Time).  
  
 Per altre informazioni sui tipi di dati, vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio viene illustrata un'espressione tramite cui viene restituito `savannah` o `unknown`, a seconda del valore restituito dalla condizione.  
  
```  
@AnimalName == "Elephant"? "savannah": "unknown"  
```  
  
 In questo esempio viene illustrata un'espressione che fa riferimento a una colonna di nome **ListPrice** . **ListPrice** ha tipo di dati DT_CY. Tramite l'espressione **ListPrice** viene moltiplicato per 0,2 o 0,1, a seconda del valore restituito dalla condizione.  
  
```  
ListPrice < 350.00 ? ListPrice * .2 : ListPrice * .1  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Precedenza e associatività degli operatori](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operatori &#40;espressione SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
