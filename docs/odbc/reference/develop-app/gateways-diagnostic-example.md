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
ms.openlocfilehash: 50476cb92d477bb9a72ac8d4311d24572b0368e9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68069678"
---
# <a name="gateways-diagnostic-example"></a>Esempio di diagnostica di gateway
In un'architettura del gateway un driver invia richieste a un gateway che supporta ODBC. Il Gateway invia le richieste a un sistema DBMS. Poiché è il componente che si interfaccia con Gestione driver, il driver formatta e restituisce gli argomenti per **SQLGetDiagRec**.  
  
 Ad esempio, se Oracle si basa su un gateway per RDB in Microsoft Open Data Services e se RDB non è stato in grado di trovare il dipendente della tabella, il gateway potrebbe generare questo messaggio di diagnostica:  
  
```  
"[42S02][-1][DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not defined "  
   "in schema."  
```  
  
 Poiché l'errore si è verificato nell'origine dati, il gateway ha aggiunto un prefisso per l'identificatore dell'origine dati ([RDB]) al messaggio di diagnostica. Poiché il gateway è il componente che è stato interfacciato con l'origine dati, ha aggiunto i prefissi per il fornitore ([DEC]) e l'identificatore ([ODS gateway]) al messaggio di diagnostica. Ha inoltre aggiunto il valore SQLSTATE e il codice di errore RDB all'inizio del messaggio di diagnostica. In questo modo è possibile mantenere la semantica della propria struttura dei messaggi e fornire le informazioni di diagnostica ODBC al driver. Il driver analizza le informazioni sull'errore associate all'istruzione Error dal gateway.  
  
 Poiché il driver del gateway è il componente che si interfaccia con Gestione driver, utilizzerà il messaggio di diagnostica precedente per formattare e restituire i valori seguenti da **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not "  
                  "defined in schema."  
```
