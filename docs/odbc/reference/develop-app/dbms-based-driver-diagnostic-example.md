---
title: Esempio di diagnostica di Driver basati su DBMS | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBMS-based driver diagnostic [ODBC]
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: a80d54b0-43ff-4dfd-b6cb-f4694a5ed765
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0485ecf720cb84580c17c77b31fc6816de2e679a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "62641034"
---
# <a name="dbms-based-driver-diagnostic-example"></a>Esempio di diagnostica di driver basato su DBMS
Un driver basati su DBMS invia richieste a un sistema DBMS e restituisce informazioni per l'applicazione tramite Gestione Driver. Poiché il driver è il componente che si interfaccia con gestione Driver, viene formattato e restituisce gli argomenti per **SQLGetDiagRec**.  
  
 Ad esempio, se, usando SQL/Services, un driver Microsoft per Oracle Rdb ha rilevato un nome di cursore non valido, potrebbe restituire i valori seguenti dal **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "34000"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver]Invalid cursor name: EMPLOYEE_CURSOR."  
```  
  
 Perché si è verificato l'errore nel driver, aggiungere i prefissi per il messaggio di diagnostica per il fornitore ([Microsoft]) e il driver ([Driver ODBC Rdb]).  
  
 Se il sistema DBMS non è stato possibile trovare la tabella dipendente, il driver può formattare e restituire i valori seguenti dal **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver][Rdb] %SQL-F-RELNOTDEF, Table EMPLOYEE "  
                  "is not defined in schema."  
```  
  
 Poiché si è verificato l'errore nell'origine dati, il driver aggiunto un prefisso per l'identificatore dell'origine dati ([Rdb]) per il messaggio di diagnostica. Poiché il driver è il componente che interfaccia duale con l'origine dati, aggiunto prefissi per il relativo fornitore ([Microsoft]) e l'identificatore ([Driver ODBC Rdb]) per il messaggio di diagnostica.
