---
title: Esempio di diagnostica di driver basati su DBMS | Microsoft Docs
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
ms.openlocfilehash: ef42fe2ab881a7e24d680e0dd941cbea0d95488f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68076887"
---
# <a name="dbms-based-driver-diagnostic-example"></a>Esempio di diagnostica di driver basato su DBMS
Un driver basato su DBMS invia richieste a un DBMS e restituisce informazioni all'applicazione tramite Gestione driver. Poiché il driver è il componente che si interfaccia con Gestione driver, formatta e restituisce gli argomenti per **SQLGetDiagRec**.  
  
 Se, ad esempio, si usa SQL/Services, un driver Microsoft per Oracle RDB ha rilevato un nome di cursore non valido, potrebbe restituire i valori seguenti da **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "34000"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver]Invalid cursor name: EMPLOYEE_CURSOR."  
```  
  
 Poiché l'errore si è verificato nel driver, i prefissi sono stati aggiunti al messaggio di diagnostica per il fornitore ([Microsoft]) e al driver ([ODBC RDB driver]).  
  
 Se il sistema DBMS non è riuscito a trovare il dipendente della tabella, il driver potrebbe formattare e restituire i valori seguenti da **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver][Rdb] %SQL-F-RELNOTDEF, Table EMPLOYEE "  
                  "is not defined in schema."  
```  
  
 Poiché l'errore si è verificato nell'origine dati, il driver ha aggiunto un prefisso per l'identificatore dell'origine dati ([RDB]) al messaggio di diagnostica. Poiché il driver è il componente che è stato interfacciato con l'origine dati, ha aggiunto i prefissi per il fornitore ([Microsoft]) e l'identificatore ([ODBC RDB driver]) al messaggio di diagnostica.
