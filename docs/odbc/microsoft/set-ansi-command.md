---
title: Comando SET ANSI Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 97269642b4147b966fdd71003f5f81ebe7905282
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300911"
---
# <a name="set-ansi-command"></a>SET ANSI (comando)
Determina il modo in cui vengono eseguiti i confronti tra stringhe di lunghezza diversa con l'operatore .  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SET ANSI ON | OFF  
```  
  
## <a name="arguments"></a>Argomenti  
 ON  
 (Impostazione predefinita per il driver; l'impostazione predefinita per Visual FoxPro è OFF. Riempie la stringa più corta con gli spazi vuoti necessari per renderla uguale alla lunghezza della stringa più lunga. Le due stringhe vengono quindi confrontate carattere per carattere per l'intera lunghezza. Si consideri questo confronto:Consider this comparison:  
  
```  
'Tommy' = 'Tom'  
```  
  
 Il risultato è False (. F.) se SET ANSI è attivato, perché quando è imbottito, 'Tom' diventa 'Tom' e le stringhe 'Tom' e 'Tommy' non corrispondono al carattere per carattere.  
  
 L'operatore di s per i confronti nei comandi SQL di Visual FoxPro.  
  
 OFF  
 Specifica che la stringa più corta non deve essere riempita con spazi vuoti. Le due stringhe vengono confrontate carattere per carattere fino a quando non viene raggiunta la fine della stringa più breve. Si consideri questo confronto:Consider this comparison:  
  
```  
'Tommy' = 'Tom'  
```  
  
 Il risultato è True (. T.) quando set ANSI è disattivato, perché il confronto si interrompe dopo 'Tom'.  
  
## <a name="remarks"></a>Osservazioni  
 SET ANSI determina se la più breve delle due stringhe viene riempita con spazi vuoti quando viene eseguito un confronto tra stringhe SQL. SET ANSI non ha alcun effetto sull'operatore di s;; quando si utilizza l'operatore , la stringa più breve viene sempre riempita con spazi vuoti per il confronto.  
  
## <a name="string-order"></a>Ordine delle stringhe  
 Nei comandi SQL, l'ordine da sinistra a destra delle due stringhe in un confronto è irrilevantecambiare una stringa da un lato dell'operatore o l'operatore di tipo , o , all'altro non influisce sul risultato del confronto.  
  
## <a name="see-also"></a>Vedere anche  
 [SELECT - Comando SQL](../../odbc/microsoft/select-sql-command.md)   
 [SET EXACT (comando)](../../odbc/microsoft/set-exact-command.md)
