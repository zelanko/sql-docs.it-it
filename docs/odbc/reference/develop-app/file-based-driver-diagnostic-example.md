---
title: Esempio di diagnostica dei driver basati su file Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- file-based driver diagnostic [ODBC]
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: 0575fccd-4641-478d-a3cc-5a764e35bae2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6f09e4f4758b6276836b08f02b24fb31dd1fadc7
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305639"
---
# <a name="file-based-driver-diagnostic-example"></a>Esempio di diagnostica di driver basato su file
Un driver basato su file funge sia come driver ODBC che come origine dati. Può pertanto generare errori e avvisi sia come componente in una connessione ODBC che come origine dati. Poiché è anche il componente che si interfaccia con Gestione Driver, formatta e restituisce gli argomenti per **SQLGetDiagRec**.  
  
 Ad esempio, se un driver Microsoft® per dBASE non è in grado di allocare memoria sufficiente, potrebbe restituire i seguenti valori da **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY001"  
Native Error:      42052  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver]Unable to allocate sufficient memory."  
```  
  
 Poiché questo errore non era correlato all'origine dati, il driver aggiungeva solo prefissi al messaggio di diagnostica per il fornitore ([Microsoft]) e il driver ([ODBC dBASE Driver]).  
  
 Se il driver non riesce a trovare il file Employee.dbf, potrebbe restituire i seguenti valori da **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1305  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver][dBASE]No such table or object"  
```  
  
 Poiché questo errore era correlato all'origine dati, il driver ha aggiunto il formato di file dell'origine dati ([dBASE]) come prefisso per il messaggio di diagnostica. Poiché il driver era anche il componente che si interfacciava con l'origine dati, aggiungeva prefissi per il fornitore ([Microsoft]) e il driver ([ODBC dBASE Driver]).
