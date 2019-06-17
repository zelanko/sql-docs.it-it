---
title: Tipi di dati dBASE | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fc4b4c7a5c1074a62bf0e84d265840109f65ea55
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63126314"
---
# <a name="dbase-data-types"></a>Tipi di dati dBASE
Nella tabella seguente viene illustrato come i tipi di dati dBASE vengono mappati ai tipi di dati SQL ODBC. Si noti che non tutti i tipi di dati SQL ODBC sono supportati.  
  
|tipo di dati dBASE|Tipo di dati ODBC|  
|---------------------|--------------------|  
|CHAR|SQL_VARCHAR|  
|DATE|SQL_DATE|  
|FLOAT[1]|SQL_DOUBLE|  
|LOGICA|SQL_BIT|  
|MEMO|SQL_LONGVARCHAR|  
|NUMERIC (BCD)|SQL_DOUBLE|  
|CLASSI OLEOBJECT [1]|SQL_LONGBINARY|  
  
 [1] valido solo per dBASE versione 5. *x*  
  
 Precisione in file dBASE III ammette numeri con backup per gli esponenti a due cifre e numeri dBASE IV con fino a tre cifre esponenti. Poiché i numeri vengono archiviati come testo, essi vengono convertiti in numeri. Se il numero da convertire non rientra in un campo, si potrebbero verificare risultati inspiegabili.  
  
 File dBASE consente una precisione e scala per essere specificato con un tipo di dati numerici, ma non è supportato dal driver dBASE ODBC. Il driver dBASE ODBC restituisce sempre una precisione pari a 15 e una scala pari a 0 per un tipo di dati numerici.  
  
 Una colonna creata con il tipo di dati numerici usando le mappe di driver dBASE ODBC al tipo di dati ODBC SQL_DOUBLE. In questo modo i dati in questa colonna sono soggetta a arrotondamento. Questo comportamento non è lo stesso come che i dati numerici di tipo in file dBASE (tipo N), ovvero Binary Coded Decimal (BCD).  
  
> [!NOTE]  
>  **SQLGetTypeInfo** restituisce i tipi di dati SQL ODBC. Tutte le conversioni nell'appendice D i *riferimento per programmatori ODBC* sono supportati per i tipi di dati SQL ODBC elencati in precedenza in questo argomento.  
  
 La tabella seguente illustra le limitazioni in file dBASE i tipi di dati.  
  
|Tipo di dati|Descrizione|  
|---------------|-----------------|  
|CHAR|Creazione di una colonna CHAR pari a zero o lunghezza non specificata restituisce effettivamente una colonna di 254 byte.|  
|Dati crittografati|Il driver dBASE non supporta le tabelle crittografate dBASE.|  
|LOGICA|Il driver dBASE non è possibile creare un indice su una colonna LOGICA.|  
|MEMO|La lunghezza massima di una colonna MEMO è di tipo di 65.500 byte.|  
  
 Altre limitazioni sui tipi di dati sono disponibili nel [limitazioni del tipo di dati](../../odbc/microsoft/data-type-limitations.md).
