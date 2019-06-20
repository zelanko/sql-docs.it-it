---
title: SET ANSI (comando) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- set ANSI command [ODBC]
ms.assetid: cf9a01b2-14bf-458c-a73c-2a58ddef32d8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5af98bd8f16d7278b932ad89f1c81c58ddb1fb54
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127868"
---
# <a name="set-ansi-command"></a>SET ANSI (comando)
Determina come i confronti tra stringhe di lunghezza diversa vengono apportati con l'operatore = di comandi di Visual FoxPro SQL.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SET ANSI ON | OFF  
```  
  
## <a name="arguments"></a>Argomenti  
 ON  
 (Valore predefinito per il driver, il valore predefinito di Visual FoxPro è impostata su OFF). La stringa più breve con i campi vuoti necessari per i riquadri rendono lunghezza della stringa uguale a più tempo. Le due stringhe vengono successivamente confrontate carattere per carattere per l'intera lunghezza. Prendere in considerazione questo confronto:  
  
```  
'Tommy' = 'Tom'  
```  
  
 Il risultato è False (. F.) se SET ANSI è attivato, perché quando riempiti, 'Tom' diventa 'Tom' e le stringhe 'Tom' e 'Tommaso' non corrispondono a carattere per carattere.  
  
 I = = operatore Usa questo metodo per i confronti nei comandi di Visual FoxPro SQL.  
  
 OFF  
 Specifica che la stringa più corta non vengano riempiti con spazi vuoti. Le due stringhe vengono confrontate carattere per carattere fino a quando non viene raggiunta la fine della stringa più breve. Prendere in considerazione questo confronto:  
  
```  
'Tommy' = 'Tom'  
```  
  
 Il risultato è True (. T.) quando SET ANSI è off, in quanto il confronto si arresta dopo 'Tom'.  
  
## <a name="remarks"></a>Note  
 SET ANSI determina se il valore inferiore tra due stringhe viene riempito con spazi vuoti quando viene effettuato un confronto tra stringhe SQL. SET ANSI non ha alcun effetto sui = = operator; Quando si usa l'operatore = =, la stringa più breve sempre viene riempita con spazi vuoti per il confronto.  
  
## <a name="string-order"></a>Ordine di stringa  
 Nei comandi SQL, l'ordine da sinistra a destra delle due stringhe in un confronto è irrelevantswitching una stringa da un lato dell'operatore = o = = operatore a altro non influisce sul risultato del confronto.  
  
## <a name="see-also"></a>Vedere anche  
 [SELECT - comando SQL](../../odbc/microsoft/select-sql-command.md)   
 [SET EXACT (comando)](../../odbc/microsoft/set-exact-command.md)
