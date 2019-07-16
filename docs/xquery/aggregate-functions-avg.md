---
title: Funzione AVG (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:avg function
- avg function [XQuery]
ms.assetid: 0cc60267-3c56-4a88-8ad7-bb07f0255d56
author: rothja
ms.author: jroth
ms.openlocfilehash: b659aa13a8704a060be12bb015bd0de0fd126562
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67985991"
---
# <a name="aggregate-functions---avg"></a>Funzioni di aggregazione - avg
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Restituisce la media di una sequenza di numeri.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
fn:avg($arg as xdt:anyAtomicType*) as xdt:anyAtomicType?  
```  
  
## <a name="arguments"></a>Argomenti  
 *$arg*  
 Sequenza di valori atomici per la quale viene calcolata la media.  
  
## <a name="remarks"></a>Note  
 Tutti i tipi di valori atomizzati passati a **AVG ()** deve essere un sottotipo di esattamente uno dei tre tipi di base numerici predefiniti o xdt: untypedAtomic. e non possono essere una combinazione di tipi. I valori del tipo xdt:untypedAtomic vengono considerati come xs:double. Il risultato del **AVG ()** riceve il tipo di base dei tipi passati, ad esempio xs: double nel caso di xdt: untypedAtomic.  
  
 Se l'input è una sequenza vuota calcolata in modo statico, la sequenza vuota è implicita e viene restituito un errore statico.  
  
 Il **AVG ()** funzione restituisce la media dei numeri calcolata. Ad esempio:  
  
 **SUM (** *$arg* **) div count (** *$arg* **)**  
  
 Se *$arg* è una sequenza vuota, viene restituita la sequenza vuota.  
  
 Se non è possibile eseguire il cast di un valore xdt: untypedAtomic a xs: Double, tale valore viene ignorato nella sequenza di input *$arg*.  
  
 In tutti gli altri casi, la funzione restituisce un errore statico.  
  
## <a name="examples"></a>Esempi  
 In questo argomento vengono forniti esempi di XQuery sulle istanze XML archiviate in diverse **xml** colonne di tipo nel database AdventureWorks.  
  
### <a name="a-using-the-avg-xquery-function-to-find-work-center-locations-in-the-manufacturing-process-in-which-labor-hours-are-greater-than-the-average-for-all-work-center-locations"></a>R. Utilizzo della funzione XQuery avg() per trovare i centri di lavorazione del processo di produzione con ore di manodopera superiori alla media di tutti i centri.  
 È possibile riscrivere la query illustrata nel [funzione min (XQuery)](../xquery/aggregate-functions-min.md) da utilizzare il **AVG ()** (funzione).  
  
## <a name="implementation-limitations"></a>Limitazioni di implementazione  
 Limitazioni:  
  
-   Il **AVG ()** funzione esegue il mapping di tutti i valori interi a xs: decimal.  
  
-   Il **AVG ()** funzione con valori di tipo xs: Duration non è supportata.  
  
-   Non sono supportate le sequenze con combinazioni di tipi che non rispettano i limiti del tipo di base.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzioni XQuery per il tipo di dati XML](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
