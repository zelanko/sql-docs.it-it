---
title: I tipi di dati Paradox | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8e2f3b1e63578af7c0b42f00113fbb9e87cb8003
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63208427"
---
# <a name="paradox-data-types"></a>Tipi di dati Paradox
Il driver ODBC Paradox esegue il mapping di tipi di dati Paradox ai tipi di dati SQL ODBC. Nella tabella seguente sono elencati tutti i tipi di dati Paradox e illustra i tipi di dati a che vengono mappati ODBC SQL.  
  
|Tipo di dati Paradox|Tipo di dati ODBC|  
|-----------------------|--------------------|  
|ALPHANUMERIC|SQL_VARCHAR|  
|INCREMENTO AUTOMATICO [1]|SQL_INTEGER|  
|BCD[1]|SQL_DOUBLE|  
|BYTES[1]|SQL_BINARY|  
|DATE|SQL_DATE|  
|IMMAGINE DI [2]|SQL_LONGVARBINARY|  
|LOGICAL[1]|SQL_BIT|  
|LONG[1]|SQL_INTEGER|  
|MEMO[2]|SQL_LONGVARCHAR|  
|MONEY[1]|SQL_DOUBLE|  
|NUMBER|SQL_DOUBLE|  
|BREVE|SQL_SMALLINT|  
|TIME[1]|SQL_TIMESTAMP|  
|TIMESTAMP[1]|SQL_TIMESTAMP|  
  
 [1] valido solo per le versioni Paradox 5. *x*.  
  
 [2] valido solo per le versioni Paradox 4. *x* e 5. *x*.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** restituisce i tipi di dati SQL ODBC. Tutte le conversioni nell'appendice D i *riferimento per programmatori ODBC* sono supportati per i tipi di dati SQL ODBC elencati in precedenza in questo argomento.  
  
 La tabella seguente illustra le limitazioni sui tipi di dati Paradox.  
  
|Tipo di dati|Descrizione|  
|---------------|-----------------|  
|ALPHANUMERIC|Creazione di una colonna ALFANUMERICA pari a zero o di lunghezza non specificata restituisce effettivamente una colonna a 255 byte.|  
|BYTES|Se si inserisce NULL in una colonna binaria con il driver Paradox5, si viene modificato a 0.|  
|LONG|Il valore negativo massimo supportato dal driver Paradox per il tipo di dati Long in 5 Paradox. *x* non è -2 ^ 31 (-2147483648), come deve essere dal momento che lungo associato ai dati ODBC digitare SQL_INTEGER. Il valore negativo massimo supportato per Long è effettivamente -2 ^ 31 + 1 (-2147483647).|  
|timestamp|Quando un valore viene inserito in una colonna TIMESTAMP dal driver Paradox, quindi in seguito recuperato dalla colonna, il valore recuperato può differire dal valore inserito da più di 1 secondo a causa dell'arrotondamento.|  
  
 Altre limitazioni sui tipi di dati sono disponibili nel [limitazioni del tipo di dati](../../odbc/microsoft/data-type-limitations.md).
