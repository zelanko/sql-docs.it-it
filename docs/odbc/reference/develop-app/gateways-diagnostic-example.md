---
title: Esempio di diagnostica di gateway | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], examples
- gateway diagnostic [ODBC]
- error messages [ODBC], diagnostic messages
ms.assetid: e0695fac-4593-4b3d-8675-cb8f73dab966
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5f4e17074616111ee93ce87c04036d1fc3fd48dd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63062419"
---
# <a name="gateways-diagnostic-example"></a>Esempio di diagnostica di gateway
In un'architettura di gateway, un driver invia richieste a un gateway che supporti ODBC. Il gateway invia le richieste a un sistema DBMS. Poiché è il componente che si interfaccia con gestione Driver, il driver formati e restituisce gli argomenti per **SQLGetDiagRec**.  
  
 Ad esempio, se Oracle in base un gateway a Rdb Open Data Services e Microsoft se Rdb non è riuscito a trovare la tabella dipendente, il gateway potrebbe generare questo messaggio di diagnostica:  
  
```  
"[42S02][-1][DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not defined "  
   "in schema."  
```  
  
 Perché si è verificato l'errore nell'origine dati, il gateway di aggiunta un prefisso per l'identificatore dell'origine dati ([Rdb]) al messaggio di diagnostica. Perché il gateway è il componente che interfaccia duale con l'origine dati, i prefissi per il fornitore ([DEC]) e l'identificatore ([ODS Gateway]) aggiunto al messaggio di diagnostica. Inoltre aggiunto il valore SQLSTATE e il codice di errore Rdb all'inizio del messaggio di diagnostica. Ciò è consentito per mantenere la semantica della propria struttura di messaggio e ancora fornire le informazioni di diagnostica per il driver ODBC. Il driver analizza le informazioni sull'errore associate all'istruzione di errore da parte del gateway.  
  
 Poiché il driver del gateway è il componente che si interfaccia con gestione Driver, viene utilizzato il messaggio di diagnostica riportato sopra per formattare e restituire i valori seguenti dal **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not "  
                  "defined in schema."  
```
