---
title: == (uguale) (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- equal operator (==)
- == (equal operator)
ms.assetid: 36fd2354-7b93-4c95-9cf3-51ee24568950
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 782d0289c90255743774de65f18848b7e9891271
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/20/2019
ms.locfileid: "58270606"
---
# <a name="-equal-ssis-expression"></a>== (uguale) (espressione SSIS)
  Viene eseguito un confronto per determinare se due espressioni sono uguali. L'analizzatore di espressioni converte automaticamente numerosi tipi di dati prima di eseguire il confronto. Per altre informazioni, vedere [Tipi di dati nelle espressioni di Integration Services](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
 Per alcuni tipi di dati, tuttavia, è necessario che l'espressione includa un cast esplicito per consentirne la corretta valutazione. Per altre informazioni sui cast supportati tra tipi di dati, vedere [Cast &#40;espressione SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
expression1 == expression2  
  
```  
  
## <a name="arguments"></a>Argomenti  
 *expression1, expression2*  
 Qualsiasi espressione valida.  
  
## <a name="result-types"></a>Tipi restituiti  
 DT_BOOL  
  
## <a name="remarks"></a>Remarks  
 Se una delle espressioni nel confronto è Null, il risultato del confronto sarà Null. Se entrambe le espressioni sono Null, il risultato sarà Null.  
  
 Il set di espressioni *expression1* e *expression2*deve seguire una di queste regole:  
  
-   **Numeric** Sia *expression1* che *expression2* devono essere un tipo di dati numerici. L'intersezione dei tipi di dati deve essere un tipo di dati numeric come specificato dalle regole relative alle conversioni numeriche implicite eseguite dall'analizzatore di espressioni. L'intersezione dei due tipi di dati numeric non può essere Null. Per altre informazioni, vedere [Tipi di dati nelle espressioni di Integration Services](../../integration-services/expressions/integration-services-data-types-in-expressions.md).  
  
-   **Character** Sia *expression1* che *expression2* devono restituire un tipo di dati DT_STR o DT_WSTR. Le due espressioni possono restituire tipi di dati string diversi.  
  
    > [!NOTE]  
    >  Per i confronti di stringa viene applicata la distinzione tra maiuscole e minuscole, tra caratteri accentati e non accentati, la distinzione Kana e di larghezza.  
  
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
  
-   **Logical** Sia *expression1* che *expression2* devono restituire un valore booleano.  
  
-   **GUID** Sia *expression1* che *expression2* devono restituire il tipo di dati DT_GUID.  
  
-   **Binary** Sia *expression1* che *expression2* devono restituire il tipo di dati DT_BYTES.  
  
-   **BLOB** Sia *expression1* che *expression2* devono restituire lo stesso tipo di dati BLOB (Binary Large Object Block): DT_TEXT, DT_NTEXT o DT_IMAGE.  
  
 Per altre informazioni sui tipi di dati, vedere [Tipi di dati di Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
## <a name="expression-examples"></a>Esempi di espressione  
 In questo esempio viene restituito TRUE se la data corrente è il 4 luglio 2003. Per altre informazioni, vedere [GETDATE &#40;espressione SSIS&#41;](../../integration-services/expressions/getdate-ssis-expression.md).  
  
 "7/4/2003" == GETDATE()  
  
 In questo esempio viene restituito TRUE se il valore nella colonna **ListPrice** è 500.  
  
```  
ListPrice == 500  
```  
  
 In questo esempio viene usata la variabile **LPrice**. Viene restituito TRUE se il valore di **LPrice** è 500. Per consentire la corretta analisi dell'espressione, il tipo di dati della variabile deve essere numeric.  
  
```  
@LPrice == 500  
```  
  
## <a name="see-also"></a>Vedere anche  
 [! = &#40;diverso da&#41; &#40;espressione SSIS&#41;](../../integration-services/expressions/unequal-ssis-expression.md)   
 [Precedenza e associatività degli operatori](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operatori &#40;espressione SSIS&#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  
