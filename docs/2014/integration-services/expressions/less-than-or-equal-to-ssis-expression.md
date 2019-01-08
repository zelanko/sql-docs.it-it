---
title: '&lt;= (minore o uguale a) (espressione SSIS) | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- <= (less than or equal to operator)
- less than or equal to operator (<=)
ms.assetid: 946c5630-dccf-4dae-9cfd-6ea823641ab2
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d10d10388f6efa55fb2655a21b50b2ebdd58e5b2
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52754343"
---
# <a name="lt-less-than-or-equal-to-ssis-expression"></a>&lt;= (minore o uguale a) (espressione SSIS)
  Viene eseguito un confronto per determinare se la prima espressione è minore o uguale alla seconda. L'analizzatore di espressioni converte automaticamente numerosi tipi di dati prima di eseguire il confronto.  
  
> [!NOTE]  
>  Questo operatore non supporta confronti tra espressioni che utilizzano il tipo di dati DT_TEXT, DT_NTEXT o DT_IMAGE.  
  
 Per alcuni tipi di dati, tuttavia, è necessario che l'espressione includa un cast esplicito per consentirne la corretta valutazione. Per altre informazioni sui cast supportati tra tipi di dati, vedere [Cast &#40;espressione SSIS&#41;](cast-ssis-expression.md).  
  
> [!NOTE]  
>  Tra i due caratteri di questo operatore non sono presenti spazi.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
expression1 <= expression2  
  
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
  
-   **Data, ora o data/ora** entrambe *expression1* e *expression2* deve restituire uno dei tipi di dati seguenti: DT_DBDATE, DT_DATE, DT_DBTIME, DT_DBTIME2, DT_DBTIMESTAMP, DT_DBTIMESTAMP2, DT_DBTIMESTAPMOFFSET o DT_FILETIME.  
  
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
  
 Per altre informazioni sui tipi di dati, vedere [Tipi di dati di Integration Services](../data-flow/integration-services-data-types.md).  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio viene restituito TRUE se la data corrente è il 4 luglio 2003 o una data successiva. Per altre informazioni, vedere [GETDATE &#40;espressione SSIS&#41;](getdate-ssis-expression.md).  
  
```  
"7/4/2003" <= GETDATE()  
```  
  
 Questo esempio restituisce TRUE se il valore nella colonna **ListPrice** è minore o uguale a 500.  
  
```  
ListPrice <= 500  
```  
  
 In questo esempio viene valutata la variabile **LPrice** e viene restituito TRUE se il valore è minore o uguale a 500. Per consentire l'analisi dell'espressione, il tipo di dati di **LPrice** deve essere numeric.  
  
```  
@LPrice <= 500  
```  
  
## <a name="see-also"></a>Vedere anche  
 [&#62; &#40;maggiore di&#41; &#40;espressione SSIS&#41;](greater-than-ssis-expression.md)   
 [&#60; &#40;minore di&#41; &#40;espressione SSIS&#41;](less-than-ssis-expression.md)   
 [&#62;= &#40;maggiore o uguale a&#41; &#40;espressione SSIS&#41;](greater-than-or-equal-to-ssis-expression.md)   
 [Precedenza e associatività degli operatori](operator-precedence-and-associativity.md)   
 [Operatori &#40;espressione SSIS&#41;](operators-ssis-expression.md)  
  
  
