---
title: Funzione round (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:round function
- round function [XQuery]
ms.assetid: 320b572f-bd5b-4055-95a6-dec5718c0041
author: rothja
ms.author: jroth
ms.openlocfilehash: 1927d6e483683699196cfc7e87928f27bf23446a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67946548"
---
# <a name="numeric-values-functions---round"></a>Funzioni per valori numerici - round
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Restituisce il numero senza parte frazionaria più vicino all'argomento. Se esiste più di un numero, viene restituito quello più vicino a infinito positivo. Ad esempio:  
  
 Se l'argomento è 2,5, **round ()** restituisce 3.  
  
 Se l'argomento è 2,4999, **round ()** restituisce 2.  
  
 Se l'argomento è-2,5, **round ()** restituisce-2.  
  
 Se l'argomento è una sequenza vuota, **round ()** restituisce la sequenza vuota.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
fn:round ( $arg as numeric?) as numeric?  
```  
  
## <a name="arguments"></a>Argomenti  
 *$arg*  
 Numero al quale viene applicata la funzione.  
  
## <a name="remarks"></a>Osservazioni  
 Se il tipo di *$arg* è uno dei tre tipi numerici di base, **xs: float**, **xs: Double**o **xs: Decimal**, il tipo restituito è uguale al tipo di *$arg* . Se il tipo di *$arg* è un tipo derivato da uno dei tipi numerici, il tipo restituito è il tipo numerico di base.  
  
 Se l'input per le funzioni **FN: floor**, **FN: Ceiling**o **FN: Round** è **xdt: untypedAtomic**, dati non tipizzati, viene eseguito il cast implicito a **xs: Double**.  
  
 Qualsiasi altro tipo di dati genera un errore statico.  
  
## <a name="examples"></a>Esempi  
 In questo argomento vengono forniti esempi di XQuery sulle istanze XML archiviate in diverse colonne di tipo **XML** nel database AdventureWorks.  
  
 È possibile utilizzare l'esempio funzionante nella [funzione ceiling (XQuery)](../xquery/numeric-values-functions-ceiling.md) per la funzione XQuery **round ()** . È sufficiente sostituire la funzione **Ceiling ()** nella query con la funzione **round ()** .  
  
## <a name="implementation-limitations"></a>Limitazioni di implementazione  
 Limitazioni:  
  
-   La funzione **round ()** esegue il mapping dei valori interi a xs: Decimal.  
  
-   Viene eseguito il mapping della funzione **round ()** dei valori xs: Double e xs: float compresi tra-0,5 E0 e-0e0 a 0e0 anziché-0e0.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzione floor &#40;XQuery&#41;](../xquery/numeric-values-functions-floor.md)   
 [Funzione ceiling &#40;XQuery&#41;](../xquery/numeric-values-functions-ceiling.md)  
  
  
