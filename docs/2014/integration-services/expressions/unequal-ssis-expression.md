---
title: '!= (diverso da) (espressione SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- unequal operator (!=)
- '!= (not equal to)'
ms.assetid: fad20e85-c0e6-42bf-af70-2bc80ee09be5
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 4752685d9590056cb47e88ee2ec4fea5128cc86b
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 03/22/2019
ms.locfileid: "58378849"
---
# <a name="-unequal-ssis-expression"></a>!= (diverso da) (espressione SSIS)
  Viene eseguito un confronto per determinare se due espressioni con tipi di dati compatibili sono diverse. L'analizzatore di espressioni converte automaticamente numerosi tipi di dati prima di eseguire il confronto.  
  
 Per alcuni tipi di dati, tuttavia, è necessario che l'espressione includa un cast esplicito per consentirne la corretta valutazione. Per altre informazioni sui cast supportati tra tipi di dati, vedere [Cast &#40;espressione SSIS&#41;](cast-ssis-expression.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
expression1 != expression2  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *expression1, expression2*  
 Qualsiasi espressione valida.  
  
## <a name="result-types"></a>Tipi restituiti  
 DT_BOOL  
  
## <a name="remarks"></a>Note  
 Se una delle espressioni nel confronto è Null, il risultato del confronto sarà Null. Se entrambe le espressioni sono Null, il risultato sarà Null.  
  
 Il set di espressioni *expression1* e *expression2*deve seguire una di queste regole:  
  
-   **Numeric** Sia *expression1* che *expression2* devono essere un tipo di dati numerici. L'intersezione dei tipi di dati deve essere un tipo di dati numeric come specificato dalle regole relative alle conversioni numeriche implicite eseguite dall'analizzatore di espressioni. L'intersezione dei due tipi di dati numeric non può essere Null. Per altre informazioni, vedere [Tipi di dati nelle espressioni di Integration Services](integration-services-data-types-in-expressions.md).  
  
-   **Character** Sia *expression1* che *expression2* devono restituire un tipo di dati DT_STR o DT_WSTR. Le due espressioni possono restituire tipi di dati string diversi.  
  
    > [!NOTE]  
    >  Per i confronti di stringa viene applicata la distinzione tra maiuscole e minuscole, tra caratteri accentati e non accentati, la distinzione Kana e di larghezza.  
  
-   **Data, ora o data/ora** entrambe *expression1* e *expression2* deve restituire uno dei tipi di dati seguenti: DT_DBDATE, DT_DATE, DT_DBTIME, DT_DBTIME2, DT_DBTIMESTAMP, DT_DBTIMESTAMP2, DT_DBTIMESTAPMOFFSET, or DT_FILETIME.  
  
    > [!NOTE]  
    >  Il sistema non supporta i confronti tra un'espressione che restituisce un tipo di dati di ora e un'espressione che restituisce una data o un tipo di dati di data/ora. Viene generato un errore.  
  
     In caso di confronto delle espressioni, vengono applicate le regole di conversione seguenti nell'ordine elencato:  
  
    -   Quando le due espressioni restituiscono lo stesso tipo di dati, viene effettuato un confronto del tipo di dati.  
  
    -   Se un'espressione è un tipo di dati DT_DBTIMESTAMPOFFSET, l'altra espressione viene convertita implicitamente in DT_DBTIMESTAMPOFFSET e viene eseguito un confronto DT_DBTIMESTAMPOFFSET. Per altre informazioni, vedere [Tipi di dati nelle espressioni di Integration Services](integration-services-data-types-in-expressions.md).  
  
    -   Se un'espressione è un tipo di dati DT_DBTIMESTAMP2, l'altra espressione viene convertita implicitamente in DT_DBTIMESTAMP2 e viene eseguito un confronto DT_DBTIMESTAMP2.  
  
    -   Se un'espressione è un tipo di dati DT_DBTIME2, l'altra espressione viene convertita implicitamente in DT_DBTIME2 e viene eseguito un confronto DT_DBTIME2.  
  
    -   Se un'espressione è di un tipo diverso da DT_DBTIMESTAMPOFFSET, DT_DBTIMESTAMP2 o DT_DBTIME2, le espressioni vengono convertite nel tipo di dati DT_DBTIMESTAMP prima del confronto.  
  
     In caso di confronto delle espressioni, il sistema presuppone quanto segue:  
  
    -   Se ogni espressione è un tipo di dati che include secondi frazionari, il sistema presuppone che il tipo di dati con il numero di cifre più basso per secondi frazionari presenti un valore pari a zero per le cifre rimanenti.  
  
    -   Se ogni espressione è un tipo di dati relativo alla data, ma solo una dispone di una differenza di fuso orario, il sistema presuppone che il tipo di dati senza la differenza di fuso orario sia espresso in formato UTC (Coordinated Universal Time).  
  
-   **Logical** Sia *expression1* che *expression2* devono restituire un valore booleano.  
  
-   **GUID** Sia *expression1* che *expression2* devono restituire il tipo di dati DT_GUID.  
  
-   **Binary** Sia *expression1* che *expression2* devono restituire il tipo di dati DT_BYTES.  
  
-   **BLOB** entrambe *expression1* e *expression2* devono restituire il tipo di dati stesso BLOB Binary Large Object Block (): DT_TEXT, DT_NTEXT o DT_IMAGE.  
  
 Per altre informazioni sui tipi di dati, vedere [Tipi di dati di Integration Services](../data-flow/integration-services-data-types.md).  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio viene restituito TRUE solo se la data corrente non è il 4 luglio 2003. Per altre informazioni, vedere [GETDATE &#40;espressione SSIS&#41;](getdate-ssis-expression.md).  
  
```  
"7/4/2003" != GETDATE()  
```  
  
 In questo esempio viene restituito TRUE se il valore nella colonna **ListPrice** non è 500.  
  
```  
ListPrice != 500  
```  
  
 In questo esempio viene usata la variabile **LPrice**. Viene restituito TRUE se il valore di **LPrice** non è 500. Per consentire l'analisi dell'espressione, il tipo di dati della variabile deve essere numeric.  
  
```  
@LPrice != 500  
```  
  
## <a name="see-also"></a>Vedere anche  
 [== &#40;uguale&#41; &#40;espressione SSIS&#41;](equal-ssis-expression.md)   
 [Precedenza e associatività degli operatori](operator-precedence-and-associativity.md)   
 [Operatori &#40;espressione SSIS&#41;](operators-ssis-expression.md)  
  
  
