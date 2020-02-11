---
title: IMPOSTA comando esatto | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "67997732"
---
# <a name="set-exact-command"></a>SET EXACT (comando)
Specifica le regole per il confronto di due stringhe di lunghezze diverse.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
SET EXACT ON | OFF  
```  
  
## <a name="arguments"></a>Argomenti  
 ATTIVA  
 Specifica che le espressioni devono corrispondere a un carattere per essere equivalente. Eventuali spazi vuoti finali nelle espressioni vengono ignorati per il confronto. Per il confronto, la più breve delle due espressioni viene riempita a destra con spazi vuoti in modo da corrispondere alla lunghezza dell'espressione più lunga.  
  
 OFF  
 (Impostazione predefinita). Specifica che, per essere equivalente, le espressioni devono corrispondere al carattere per il carattere fino a quando non viene raggiunta la fine dell'espressione sul lato destro.  
  
## <a name="remarks"></a>Osservazioni  
 L'impostazione esatta SET non ha effetto se entrambe le stringhe hanno la stessa lunghezza.  
  
## <a name="string-comparisons"></a>Confronti tra stringhe  
 In Visual FoxPro sono presenti due operatori relazionali che verificano l'uguaglianza.  
  
 L'operatore = esegue un confronto tra due valori dello stesso tipo. Questo operatore è adatto per confrontare dati di tipo carattere, numerici, di data e logici.  
  
 Tuttavia, quando si confrontano le espressioni di caratteri con l'operatore =, i risultati potrebbero non essere esattamente quelli previsti. Le espressioni di caratteri vengono confrontate con il carattere da sinistra a destra finché una delle espressioni non è uguale all'altra, fino a quando non viene raggiunta la fine dell'espressione a destra dell'operatore = (SET EXACT OFF) o fino a quando le entità finali di entrambe le espressioni sono raggiunto (impostazione esatta in).  
  
 L'operatore = = può essere utilizzato quando è necessario un confronto esatto dei dati di tipo carattere. Se due espressioni di caratteri vengono confrontate con l'operatore = =, le espressioni su entrambi i lati dell'operatore = = devono contenere esattamente gli stessi caratteri, inclusi gli spazi vuoti, da considerare uguali. L'impostazione esatta SET viene ignorata quando le stringhe di caratteri vengono confrontate con = =.  
  
 Nella tabella seguente viene illustrato il modo in cui la scelta dell'operatore e l'impostazione esatta hanno effetto sui confronti. Un carattere di sottolineatura rappresenta uno spazio vuoto.  
  
|Confronto|= EXACT OFF|= EXACT ON|= = ESATTA ON o OFF|  
|----------------|------------------|-----------------|--------------------------|  
|"ABC" = "ABC"|Corrispondente|Corrispondente|Corrispondente|  
|"AB" = "ABC"|Nessuna corrispondenza|Nessuna corrispondenza|Nessuna corrispondenza|  
|"ABC" = "AB"|Corrispondente|Nessuna corrispondenza|Nessuna corrispondenza|  
|"ABC" = "ab_"|Nessuna corrispondenza|Nessuna corrispondenza|Nessuna corrispondenza|  
|"AB" = "ab_"|Nessuna corrispondenza|Corrispondente|Nessuna corrispondenza|  
|"ab_" = "AB"|Corrispondente|Corrispondente|Nessuna corrispondenza|  
|"" = "AB"|Nessuna corrispondenza|Nessuna corrispondenza|Nessuna corrispondenza|  
|"AB" = ""|Corrispondente|Nessuna corrispondenza|Nessuna corrispondenza|  
|"__" = ""|Corrispondente|Corrispondente|Nessuna corrispondenza|  
|"" = "___"|Nessuna corrispondenza|Corrispondente|Nessuna corrispondenza|  
|TRIM ("_ _") = ""|Corrispondente|Corrispondente|Corrispondente|  
|"" = TRIM ("_ _")|Corrispondente|Corrispondente|Corrispondente|  
  
## <a name="see-also"></a>Vedere anche  
 [SET ANSI (comando)](../../odbc/microsoft/set-ansi-command.md)
