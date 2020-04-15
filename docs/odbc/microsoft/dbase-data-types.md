---
title: Tipi di dati dBASE Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], DBasedriver
- desktop database drivers [ODBC], DBasedriver
- DBase driver [ODBC], data types
- data types [ODBC], DBase driver
- dbase data types [ODBC]
- ODBC desktop database drivers [ODBC], DBasedriver
ms.assetid: a0e31e6b-d02b-4ee2-9b37-5baf6a11c0a6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 17b96ad0b6674a2d120ef46d9bfa221e8df6d140
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307692"
---
# <a name="dbase-data-types"></a>Tipi di dati dBASE
Nella tabella seguente viene illustrato il mapping dei tipi di dati dBASE ai tipi di dati SQL ODBC. Si noti che non tutti i tipi di dati SQL ODBC sono supportati.  
  
|Tipo di dati dBASE|Tipo di dati ODBC|  
|---------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATE|SQL_DATE|  
|GALLEGGIANTE[1]|SQL_DOUBLE|  
|Logico|SQL_BIT|  
|Memo|SQL_LONGVARCHAR|  
|NUMERICO (BCD)|SQL_DOUBLE|  
|Oggetto OLEOBJECT[1]|SQL_LONGBINARY|  
  
 [1] Valido solo per dBASE versione 5. *x (in* questo modo  
  
 Precisione in dBASE III consente numeri con esponenti fino a due cifre e in numeri dBASE IV con esponenti fino a tre cifre. Poiché i numeri vengono memorizzati come testo, vengono convertiti in numeri. Se il numero da convertire non rientra in un campo, potrebbero verificarsi risultati inspiegabili.  
  
 Mentre dBASE consente di specificare una precisione e una scala con un tipo di dati NUMERIC, non è supportato dal driver dBASE ODBC. Il driver dBASE ODBC restituisce sempre una precisione di 15 e una scala 0 per un tipo di dati NUMERIC.  
  
 Una colonna creata con il tipo di dati Numeric utilizzando il driver ODBC dBASE viene mappata al tipo di dati ODBC SQL_DOUBLE. Pertanto, i dati in questa colonna sono soggetti a arrotondamento. Questo comportamento non corrisponde a quello del tipo di dati NUMERIC in dBASE (tipo N), ovvero Binary Coded Decimal (BCD).  
  
> [!NOTE]  
>  **SQLGetTypeInfo** restituisce i tipi di dati SQL ODBC. Tutte le conversioni nell'Appendice D di *ODBC Programmer's Reference* sono supportate per i tipi di dati SQL ODBC elencati in precedenza in questo argomento.  
  
 Nella tabella seguente vengono illustrate le limitazioni relative ai tipi di dati dBASE.  
  
|Tipo di dati|Descrizione|  
|---------------|-----------------|  
|CHAR|La creazione di una colonna CHAR di lunghezza zero o non specificata restituisce in realtà una colonna di 254 byte.|  
|Dati crittografati|Il driver dBASE non supporta le tabelle dBASE crittografate.|  
|Logico|Il driver dBASE non è in grado di creare un indice in una colonna LOGICAL.|  
|Memo|La lunghezza massima di una colonna MEMO è 65.500 byte.|  
  
 Ulteriori limitazioni sui tipi di dati sono disponibili in [Limitazioni dei tipi](../../odbc/microsoft/data-type-limitations.md)di dati .
