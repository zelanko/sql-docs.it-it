---
title: Comando SET EXACT Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SET EXACT command [ODBC]
ms.assetid: 9533d3e0-e7c1-49de-a3a3-0cc4373a91cb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3e754fff35b6b948ac63d19361067b2d65a07fdd
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300871"
---
# <a name="set-exact-command"></a>SET EXACT (comando)
Specifica le regole per il confronto di due stringhe di lunghezza diversa.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SET EXACT ON | OFF  
```  
  
## <a name="arguments"></a>Argomenti  
 ON  
 Specifica che le espressioni devono corrispondere al carattere per l'equivalente di carattere. Tutti gli spazi vuoti finali nelle espressioni vengono ignorati per il confronto. Per il confronto, la più breve delle due espressioni viene riempita a destra con spazi vuoti in modo che corrisponda alla lunghezza dell'espressione più lunga.  
  
 OFF  
 (Impostazione predefinita.) Specifica che, per essere equivalenti, le espressioni devono corrispondere al carattere per carattere fino a raggiungere la fine dell'espressione sul lato destro.  
  
## <a name="remarks"></a>Osservazioni  
 L'impostazione SET EXACT non ha effetto se entrambe le stringhe hanno la stessa lunghezza.  
  
## <a name="string-comparisons"></a>Confronti tra stringhe  
 Visual FoxPro dispone di due operatori relazionali che verificano l'uguaglianza.  
  
 L'operatore , esegue un confronto tra due valori dello stesso tipo. Questo operatore è adatto per confrontare dati numerici, numerici e logici.  
  
 Tuttavia, quando si confrontano le espressioni di caratteri con l'operatore , i risultati potrebbero non essere esattamente quello previsto. Le espressioni di carattere vengono confrontate con il carattere da sinistra a destra fino a quando non viene raggiunta una delle espressioni, fino a raggiungere la fine dell'espressione sul lato destro dell'operatore s (SET EXACT OFF) o fino al raggiungimento delle estremità di entrambe le espressioni (SET EXACT ON).  
  
 Quando è necessario un confronto esatto dei dati di tipo carattere, è possibile utilizzare l'operatore . Se due espressioni di caratteri vengono confrontate con l'operatore , le espressioni su entrambi i lati dell'operatore , devono contenere esattamente gli stessi caratteri, inclusi gli spazi vuoti, per essere considerate uguali. L'impostazione SET EXACT viene ignorata quando le stringhe di caratteri vengono confrontate con il carattere .  
  
 Nella tabella seguente viene illustrato in che modo la scelta dell'operatore e l'impostazione SET EXACT influiscono sui confronti. (Un trattino di sottolineatura rappresenta uno spazio vuoto.)  
  
|Confronto|- ESATTIVA OFF|- ESATTO SU|ESATTE ON o OFF|  
|----------------|------------------|-----------------|--------------------------|  
|"abc" - "abc"|Corrispondente|Corrispondente|Corrispondente|  
|"ab" - "abc"|Nessuna corrispondenza.|Nessuna corrispondenza.|Nessuna corrispondenza.|  
|"abc" - "ab"|Corrispondente|Nessuna corrispondenza.|Nessuna corrispondenza.|  
|"abc" - "ab_"|Nessuna corrispondenza.|Nessuna corrispondenza.|Nessuna corrispondenza.|  
|"ab" - "ab_"|Nessuna corrispondenza.|Corrispondente|Nessuna corrispondenza.|  
|"ab_" - "ab"|Corrispondente|Corrispondente|Nessuna corrispondenza.|  
|"" - "ab"|Nessuna corrispondenza.|Nessuna corrispondenza.|Nessuna corrispondenza.|  
|"ab" - ""|Corrispondente|Nessuna corrispondenza.|Nessuna corrispondenza.|  
|"__" = ""|Corrispondente|Corrispondente|Nessuna corrispondenza.|  
|"" = "___"|Nessuna corrispondenza.|Corrispondente|Nessuna corrispondenza.|  
|TRIM("___") - ""|Corrispondente|Corrispondente|Corrispondente|  
|"" : trim("___")|Corrispondente|Corrispondente|Corrispondente|  
  
## <a name="see-also"></a>Vedere anche  
 [SET ANSI (comando)](../../odbc/microsoft/set-ansi-command.md)
