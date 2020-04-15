---
title: Esempio di diagnostica dei gateway Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b18fd78be7be2eb79316339cbdf3d315deb194fb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305572"
---
# <a name="gateways-diagnostic-example"></a>Esempio di diagnostica di gateway
In un'architettura gateway, un driver invia richieste a un gateway che supporta ODBC. Il gateway invia le richieste a un DBMS. Poiché è il componente che si interfaccia con Gestione Driver, il driver formatta e restituisce gli argomenti per **SQLGetDiagRec**.  
  
 Ad esempio, se Oracle basa un gateway per Rdb su Microsoft Open Data Services e se Rdb non è riuscito a trovare la tabella EMPLOYEE, il gateway potrebbe generare questo messaggio di diagnostica:  
  
```  
"[42S02][-1][DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not defined "  
   "in schema."  
```  
  
 Poiché l'errore si è verificato nell'origine dati, il gateway ha aggiunto un prefisso per l'identificatore dell'origine dati ([Rdb]) al messaggio di diagnostica. Poiché il gateway era il componente che si interfacciava con l'origine dati, aggiungeva prefissi per il relativo fornitore ([DEC]) e identificatore ([ODS Gateway]) al messaggio di diagnostica. Ha inoltre aggiunto il valore SQLSTATE e il codice di errore Rdb all'inizio del messaggio di diagnostica. Ciò ha permesso di mantenere la semantica della propria struttura di messaggi e ancora fornire le informazioni di diagnostica ODBC al driver. Il driver analizza le informazioni sull'errore associate all'istruzione error dal gateway.  
  
 Poiché il driver gateway è il componente che si interfaccia con Gestione Driver, utilizzerà il messaggio di diagnostica precedente per formattare e restituire i seguenti valori da **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not "  
                  "defined in schema."  
```
