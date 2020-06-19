---
title: Cast (espressione SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- CAST function
- cast operator
- converting data types [Integration Services]
- data types [Integration Services], expressions
- data types [Integration Services], converting
ms.assetid: d4e915cc-1c7b-4b2e-93b0-13a8b0cb9242
author: janinezhang
ms.author: janinez
ms.openlocfilehash: d94df6a59043bee136b0dc42ad8fb013c6c77456
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84967481"
---
# <a name="cast-ssis-expression"></a>Cast (espressione SSIS)
  Viene convertita esplicitamente un'espressione da un tipo di dati a un altro. L'operatore cast può essere utilizzato anche come operatore di troncamento.

## <a name="syntax"></a>Sintassi

```

(type_spec) expression

```

## <a name="arguments"></a>Argomenti
 *type_spec* È un [!INCLUDE[ssIS](../../includes/ssis-md.md)] tipo di dati valido.

 *espressione* Espressione valida.

## <a name="result-types"></a>Tipi restituiti
 Tipo di dati *type_spec*. Per ulteriori informazioni, vedere [Integration Services tipi di dati](../data-flow/integration-services-data-types.md).

## <a name="remarks"></a>Commenti
 Nella figura seguente vengono illustrate alcune operazioni di cast valide.

 ![Cast validi e non validi tra tipi di dati](../media/data-conversion.gif "Cast validi e non validi tra tipi di dati")

 Per eseguire il cast a determinati tipi di dati è necessario specificare i parametri appropriati. Nella tabella seguente vengono elencati tali tipi di dati e i parametri corrispondenti.

|Tipo di dati|Parametro|Esempio|
|---------------|---------------|-------------|
|DT_STR|*charcount*<br /><br /> *CodePage*|(DT_STR,30,1252): esegue il cast di 30 byte, ovvero 30 caratteri singoli, al tipo di dati DT_STR utilizzando la tabella codici 1252.|
|DT_WSTR|*CharCount*|(DT_WSTR,20): esegue il cast di 20 coppie di byte, ovvero 20 caratteri Unicode, al tipo di dati DT_WSTR.|
|DT_BYTES|*ByteCount*|(DT_BYTES,50): esegue il cast di 50 byte al tipo di dati DT_BYTES.|
|DT_DECIMAL|*Ridimensionamento*|(DT_DECIMAL,2): esegue il cast di un valore numerico al tipo di dati DT_DECIMAL, utilizzando una scala pari a 2.|
|DT_NUMERIC|*Precisione*<br /><br /> *Ridimensionamento*|(DT_NUMERIC,10,3): esegue il cast di un valore numerico al tipo di dati DT_NUMERIC, utilizzando una precisione pari a 10 e una scala pari a 3.|
|DT_TEXT|*CodePage*|(DT_TEXT,1252): esegue il cast di un valore al tipo di dati DT_TEXT utilizzando la tabella codici 1252.|

 Quando si esegue il cast di una stringa a un tipo di dati DT_DATE, o viceversa, vengono utilizzate le impostazioni locali della trasformazione. Tuttavia, la data è nel formato ISO AAAA-MM-GG, indipendentemente dal fatto che le impostazioni locali utilizzino il formato ISO.

> [!NOTE]
>  Per convertire una stringa in un tipo di dati date diverso da DT_DATE, vedere [Tipi di dati di Integration Services](../data-flow/integration-services-data-types.md).

 Se la tabella codici è di tipo MBCS (Multibyte Character Set), il numero dei byte potrebbe non corrispondere a quello dei caratteri. Il cast da DT_WSTR a DT_STR con lo stesso valore di *charcount* potrebbe provocare il troncamento dei caratteri finali nella stringa convertita. Se nella colonna della tabella di destinazione è disponibile spazio di archiviazione sufficiente, impostare il valore del parametro *charcount* in modo da riflettere il numero di byte richiesto dalla tabella codici MBCS. Se ad esempio si esegue il cast di dati di tipo carattere a un tipo di dati DT_STR usando la tabella codici 936, sarà necessario impostare *charcount* su un valore fino a due volte più grande del numero di caratteri che si prevede sarà contenuto nei dati. Se si esegue il cast di dati di tipo carattere utilizzando la tabella codici UTF-8, sarà necessario impostare *charcount* su un valore fino a quattro volte più grande.

 Per altre informazioni sulla struttura dei tipi di dati di data, vedere [Tipi di dati di Integration Services](../data-flow/integration-services-data-types.md).

## <a name="ssis-expression-examples"></a>Esempi di espressione SSIS
 In questo esempio viene eseguito il cast di un valore numerico a un valore integer.

```
(DT_I4) 3.57
```

 In questo esempio viene eseguito il cast di un valore integer a una stringa di caratteri utilizzando la tabella codici 1252.

```
(DT_STR,1,1252)5
```

 In questo esempio viene eseguito il cast di una stringa di tre caratteri a caratteri DBCS (Double-Byte Character Set).

```
(DT_WSTR,3)"Cat"
```

 In questo esempio viene eseguito il cast di un valore integer a un valore decimale con scala pari a 2.

```
(DT_DECIMAl,2)500
```

 In questo esempio viene eseguito il cast di un valore integer a un valore numerico con precisione pari a 7 e scala pari a 3.

```
(DT_NUMERIC,7,3)4000
```

 In questo esempio viene eseguito il cast dei valori nella colonna **FirstName** , definita con un tipo di dati **nvarchar** e lunghezza 50, a una stringa di caratteri tramite la tabella codici 1252.

```
(DT_STR,50,1252)FirstName
```

 In questo esempio viene eseguito il cast dei valori nella colonna **DateFirstPurchase** di tipo DT_DBDATE a una stringa di caratteri Unicode con lunghezza 20.

```
(DT_WSTR,20)DateFirstPurchase
```

 In questo esempio viene eseguito il cast del valore letterale stringa "True" a un valore booleano.

```
(DT_BOOL)"True"
```

 In questo esempio viene eseguito il cast di un valore letterale stringa a DT_DBDATE.

```
(DT_DBDATE) "1999-10-11"
```

 In questo esempio viene eseguito il cast di un valore letterale stringa al tipo di dati DT_DBTIME2 che utilizza 5 cifre per i secondi frazionari. Nel tipo di dati DT_DBTIME2 possono essere specificate da 0 a 7 cifre per i secondi frazionari.

```
(DT_DBTIME2, 5) "16:34:52.12345"
```

 In questo esempio viene eseguito il cast di un valore letterale stringa al tipo di dati DT_DBTIMESTAMP2 che utilizza 4 cifre per i secondi frazionari. Nel tipo di dati DT_DBTIMESTAMP2 possono essere specificate da 0 a 7 cifre per i secondi frazionari.

```
(DT_DBTIMESTAMP2, 4) "1999-10-11 16:34:52.1234"
```

 In questo esempio viene eseguito il cast di un valore letterale stringa al tipo di dati DT_DBTIMESTAMPOFFSET che utilizza 7 cifre per i secondi frazionari. Nel tipo di dati DT_DBTIMESTAMPOFFSET possono essere specificate da 0 a 7 cifre per i secondi frazionari.

```
(DT_DBTIMESTAMPOFFSET, 7) "1999-10-11 16:34:52.1234567 + 5:35"
```

## <a name="see-also"></a>Vedere anche
 Operatori di [precedenza e associatività](operator-precedence-and-associativity.md) [degli operatori &#40;espressione ssis&#41;](operators-ssis-expression.md) [Integration Services &#40;espressioni SSIS&#41;](integration-services-ssis-expressions.md) [Integration Services tipi di dati nelle espressioni](integration-services-data-types-in-expressions.md)


