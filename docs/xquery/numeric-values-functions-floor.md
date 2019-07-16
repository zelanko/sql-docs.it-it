---
title: Funzione floor (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- floor function [XQuery]
- fn:floor function
ms.assetid: 4ace57dd-b66e-4b60-a2b9-a1b0f1a0831d
author: rothja
ms.author: jroth
ms.openlocfilehash: 1c27e432dc258b4d2b9d21bfe0ab28df8ee5b510
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67946539"
---
# <a name="numeric-values-functions---floor"></a>Funzioni per valori numerici - floor
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Restituisce il numero più alto senza nessuna frazione, maggiore del valore del relativo argomento. Se l'argomento è una sequenza vuota, restituisce la sequenza vuota.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
fn:floor ($arg as numeric?) as numeric?  
```  
  
## <a name="arguments"></a>Argomenti  
 *$arg*  
 Numero al quale viene applicata la funzione.  
  
## <a name="remarks"></a>Note  
 Se il tipo di *$arg* è uno dei tre tipi numerici di base, **xs: float**, **xs: double**, oppure **xs: decimal**, il tipo restituito è come il *$arg* tipo. Se il tipo della *$arg* è un tipo derivato da uno dei tipi numerici, il tipo restituito è il tipo di base numerico.  
  
 Se l'input per le funzioni: floor, fn: Ceiling o Fn **xdt: untypedAtomic**, i dati non tipizzati, viene eseguito in modo implicito il cast **xs: double**. Qualsiasi altro tipo di dati genera un errore statico.  
  
## <a name="examples"></a>Esempi  
 In questo argomento vengono forniti esempi di XQuery sulle istanze XML archiviate in diverse **xml** colonne di tipo nel database di esempio AdventureWorks.  
  
 È possibile usare l'esempio reale disponibile nella [funzione ceiling (XQuery)](../xquery/numeric-values-functions-ceiling.md) per il **floor ()** funzione XQuery. È necessario eseguire è sostituire il **Ceiling ()** funzione nella query con la **floor ()** (funzione).  
  
## <a name="implementation-limitations"></a>Limitazioni di implementazione  
 Limitazioni:  
  
-   Il **floor ()** funzione esegue il mapping di tutti i valori interi a xs: decimal.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzione CEILING &#40;XQuery&#41;](../xquery/numeric-values-functions-ceiling.md)   
 [Funzione Round &#40;XQuery&#41;](../xquery/numeric-values-functions-round.md)   
 [Funzioni XQuery per il tipo di dati XML](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
