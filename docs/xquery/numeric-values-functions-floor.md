---
title: Funzione floor (XQuery) | Microsoft Docs
description: Informazioni sulla funzione XQuery floor () che restituisce il numero maggiore senza parte della frazione che non è maggiore del valore del relativo argomento.
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
ms.openlocfilehash: cf7943cbcef462dbdf73e72357f28e4f4e3eb20d
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85724207"
---
# <a name="numeric-values-functions---floor"></a>Funzioni per valori numerici - floor
[!INCLUDE [SQL Server Azure SQL Database ](../includes/applies-to-version/sqlserver.md)]

  Restituisce il numero più alto senza nessuna frazione, maggiore del valore del relativo argomento. Se l'argomento è una sequenza vuota, restituisce la sequenza vuota.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
fn:floor ($arg as numeric?) as numeric?  
```  
  
## <a name="arguments"></a>Argomenti  
 *$arg*  
 Numero al quale viene applicata la funzione.  
  
## <a name="remarks"></a>Osservazioni  
 Se il tipo di *$arg* è uno dei tre tipi numerici di base, **xs: float**, **xs: Double**o **xs: Decimal**, il tipo restituito è uguale al tipo di *$arg* . Se il tipo di *$arg* è un tipo derivato da uno dei tipi numerici, il tipo restituito è il tipo numerico di base.  
  
 Se l'input per le funzioni FN: floor, FN: Ceiling o FN: round è **xdt: untypedAtomic**, dati non tipizzati, viene eseguito il cast implicito a **xs: Double**. Qualsiasi altro tipo di dati genera un errore statico.  
  
## <a name="examples"></a>Esempi  
 In questo argomento vengono forniti esempi di XQuery sulle istanze XML archiviate in diverse colonne di tipo **XML** nel database di esempio AdventureWorks.  
  
 È possibile utilizzare l'esempio funzionante nella [funzione ceiling (XQuery)](../xquery/numeric-values-functions-ceiling.md) per la funzione XQuery **Floor ()** . È sufficiente sostituire la funzione **Ceiling ()** nella query con la funzione **Floor ()** .  
  
## <a name="implementation-limitations"></a>Limitazioni di implementazione  
 Limitazioni:  
  
-   La funzione **Floor ()** esegue il mapping di tutti i valori interi a xs: Decimal.  
  
## <a name="see-also"></a>Vedere anche  
 [Funzione ceiling &#40;XQuery&#41;](../xquery/numeric-values-functions-ceiling.md)   
 [Funzione round &#40;XQuery&#41;](../xquery/numeric-values-functions-round.md)   
 [Funzioni XQuery per il tipo di dati XML](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
