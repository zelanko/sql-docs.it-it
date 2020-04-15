---
title: Tipi di dati di Paradox - Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Paradox driver
- desktop database drivers [ODBC], Paradox driver
- Paradox data types [ODBC]
- Jet-based ODBC drivers [ODBC], Paradox driver
- data types [ODBC], Paradox driver
- Paradox driver [ODBC], data types
ms.assetid: 0c9e5d21-9321-49f8-a055-69459e1c9c85
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a85cf643a6d22b9b2fce15984539d74dc43c62ab
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81290931"
---
# <a name="paradox-data-types"></a>Tipi di dati Paradox
Il driver ODBC Paradox esegue il mapping dei tipi di dati Paradox ai tipi di dati SQL ODBC. Nella tabella seguente sono elencati tutti i tipi di dati Paradox e vengono illustrati i tipi di dati SQL ODBC a cui sono mappati.  
  
|Tipo di dati Paradox|Tipo di dati ODBC|  
|-----------------------|--------------------|  
|Alfanumerici|SQL_VARCHAR|  
|AUTOINCREMENT[1]|SQL_INTEGER|  
|BCD[1]|SQL_DOUBLE|  
|BYTE[1]|SQL_BINARY|  
|DATE|SQL_DATE|  
|IMMAGINE[2]|SQL_LONGVARBINARY|  
|Logico[1]|SQL_BIT|  
|LONG[1]|SQL_INTEGER|  
|MEMO[2]|SQL_LONGVARCHAR|  
|DENARO[1]|SQL_DOUBLE|  
|NUMBER|SQL_DOUBLE|  
|SHORT|SQL_SMALLINT|  
|ORARIO[1]|SQL_TIMESTAMP|  
|TIMESTAMP[1]|SQL_TIMESTAMP|  
  
 [1] Valido solo per le versioni di Paradox 5. *x*.  
  
 [2] Valido solo per le versioni 4 di Paradox. *x* e 5. *x*.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** restituisce i tipi di dati SQL ODBC. Tutte le conversioni nell'Appendice D di *ODBC Programmer's Reference* sono supportate per i tipi di dati SQL ODBC elencati in precedenza in questo argomento.  
  
 Nella tabella seguente vengono illustrate le limitazioni relative ai tipi di dati Paradox.  
  
|Tipo di dati|Descrizione|  
|---------------|-----------------|  
|Alfanumerici|La creazione di una colonna ALPHANUMERIC di lunghezza zero o non specificata restituisce in realtà una colonna di 255 byte.|  
|BYTES|Se si inserisce NULL in una colonna binaria con il driver Paradox5, viene modificato in 0.|  
|LONG|Il valore negativo massimo supportato dal driver Paradox per il tipo di dati Long in Paradox 5. *x* non è -2-31 (-2147483648), come dovrebbe essere poiché Long esegue il mapping al tipo di dati ODBC SQL_INTEGER. Il valore negativo massimo supportato per Long è in realtà -2-31 - 1 (-2147483647).|  
|timestamp|Quando un valore viene inserito in una colonna TIMESTAMP dal driver Paradox, quindi successivamente recuperato dalla colonna, il valore recuperato può differire dal valore inserito di ben 1 secondo a causa dell'arrotondamento.|  
  
 Ulteriori limitazioni sui tipi di dati sono disponibili in [Limitazioni dei tipi](../../odbc/microsoft/data-type-limitations.md)di dati .
