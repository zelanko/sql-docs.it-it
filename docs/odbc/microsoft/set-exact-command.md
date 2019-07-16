---
title: SET EXACT (comando) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 686ecc89f44bac4b219b760e55160f451a15c503
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67997732"
---
# <a name="set-exact-command"></a>SET EXACT (comando)
Specifica le regole di confronto di due stringhe di lunghezza diversa.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SET EXACT ON | OFF  
```  
  
## <a name="arguments"></a>Argomenti  
 ON  
 Specifica che le espressioni devono corrispondere esattamente carattere per carattere siano equivalenti. Per il confronto vengono ignorati gli spazi vuoti finali nelle espressioni. Per il confronto, il valore inferiore tra due espressioni viene riempito a destra con spazi vuoti in base alla lunghezza dell'espressione più lunga.  
  
 OFF  
 (Predefinito). Specifica che, per essere equivalenti, espressioni devono corrispondere esattamente carattere per carattere fino a quando non viene raggiunta la fine dell'espressione sul lato destro.  
  
## <a name="remarks"></a>Note  
 Il SET esatto impostazione non ha effetto se entrambe le stringhe sono della stessa lunghezza.  
  
## <a name="string-comparisons"></a>Confronti di stringhe  
 Visual FoxPro ha due operatori relazionali che verifica l'uguaglianza.  
  
 I = operatore esegue un confronto tra due valori dello stesso tipo. Questo operatore è adatta per il confronto dei caratteri, numerici, date e dati logici.  
  
 Tuttavia, quando si confrontano le espressioni di caratteri con l'operatore =, i risultati potrebbero non essere esattamente quello previsto. Espressioni di caratteri vengono confrontate carattere per carattere da sinistra verso destra fino a quando una delle espressioni non è uguale a altro, fino alla fine dell'espressione sul lato destro del = operatore è raggiungibile (SET esatto OFF), o fino a quando non sono le entità finali di entrambe le espressioni raggiunto (impostato esattamente su ON).  
  
 I = = operatore può essere usato quando è necessario un confronto esatto dei dati di tipo carattere. Se due espressioni di caratteri vengono confrontate con l'operatore = =, le espressioni su entrambi i lati del = = operator deve contenere esattamente gli stessi caratteri, compresi gli spazi vuoti, per essere considerate uguali. L'impostazione SET EXACT viene ignorata quando vengono confrontate le stringhe di caratteri utilizzando = =.  
  
 Nella tabella seguente viene illustrato come la scelta dell'operatore e l'impostazione SET EXACT interessano i confronti. (Un carattere di sottolineatura rappresenta uno spazio vuoto).  
  
|Confronto|= ESATTA OFF|= ESATTA SU|= = ESATTA su ON oppure OFF|  
|----------------|------------------|-----------------|--------------------------|  
|"abc" = "abc"|Corrispondenza|Corrispondenza|Corrispondenza|  
|"ab" = "abc"|Nessuna corrispondenza|Nessuna corrispondenza|Nessuna corrispondenza|  
|"abc" = "ab"|Corrispondenza|Nessuna corrispondenza|Nessuna corrispondenza|  
|"abc" = "ab_"|Nessuna corrispondenza|Nessuna corrispondenza|Nessuna corrispondenza|  
|"ab" = "ab_"|Nessuna corrispondenza|Corrispondenza|Nessuna corrispondenza|  
|"ab_" = "ab"|Corrispondenza|Corrispondenza|Nessuna corrispondenza|  
|"" = "ab"|Nessuna corrispondenza|Nessuna corrispondenza|Nessuna corrispondenza|  
|"ab" = ""|Corrispondenza|Nessuna corrispondenza|Nessuna corrispondenza|  
|"__" = ""|Corrispondenza|Corrispondenza|Nessuna corrispondenza|  
|"" = "___"|Nessuna corrispondenza|Corrispondenza|Nessuna corrispondenza|  
|TRIM("___") = ""|Corrispondenza|Corrispondenza|Corrispondenza|  
|"" = TRIM("___")|Corrispondenza|Corrispondenza|Corrispondenza|  
  
## <a name="see-also"></a>Vedere anche  
 [SET ANSI (comando)](../../odbc/microsoft/set-ansi-command.md)
