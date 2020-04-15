---
title: Esempio di diagnostica dei driver basati su DBMS Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 117f43548d2b57233dea6f7423e6bad67b6233b0
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304352"
---
# <a name="dbms-based-driver-diagnostic-example"></a>Esempio di diagnostica di driver basato su DBMS
Un driver basato su DBMS invia richieste a un DBMS e restituisce informazioni all'applicazione tramite Gestione Driver. Poiché il driver è il componente che si interfaccia con Gestione Driver, formatta e restituisce gli argomenti per **SQLGetDiagRec**.  
  
 Ad esempio, se, utilizzando SQL/Services, un driver Microsoft per Oracle Rdb ha rilevato un nome di cursore non valido, potrebbe restituire i seguenti valori da **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "34000"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver]Invalid cursor name: EMPLOYEE_CURSOR."  
```  
  
 Poiché l'errore si è verificato nel driver, ha aggiunto prefissi al messaggio di diagnostica per il fornitore ([Microsoft]) e il driver ([ODBC Rdb Driver]).  
  
 Se il DBMS non riesce a trovare la tabella EMPLOYEE, il driver potrebbe formattare e restituire i seguenti valori da **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver][Rdb] %SQL-F-RELNOTDEF, Table EMPLOYEE "  
                  "is not defined in schema."  
```  
  
 Poiché l'errore si è verificato nell'origine dati, il driver ha aggiunto un prefisso per l'identificatore dell'origine dati ([Rdb]) al messaggio di diagnostica. Poiché il driver era il componente che si interfacciava con l'origine dati, aggiungeva prefissi per il relativo fornitore ([Microsoft]) e identificatore ([ODBC Rdb Driver]) al messaggio di diagnostica.
