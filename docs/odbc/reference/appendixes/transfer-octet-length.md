---
title: Trasferire la lunghezza dell'ottetto Documenti Microsoft
ms.custom: ''
ms.date: 10/28/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- transfer octet length of data types [ODBC]
- size of data types [ODBC]
- SQL data types [ODBC], column characteristics
- data types [ODBC], transfer octet length
ms.assetid: 9fdc9762-e203-4cff-9212-54f450bf18d9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4204b47816747506a5672241eeeef736eca54856
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302812"
---
# <a name="transfer-octet-length"></a>Lunghezza dell'ottetto di trasferimento
La lunghezza dell'ottetto di trasferimento di una colonna è il numero massimo di byte restituiti all'applicazione quando i dati vengono trasferiti al tipo di dati C predefinito. Per i dati di tipo carattere, la lunghezza dell'ottetto di trasferimento non include lo spazio per il carattere di terminazione null. La lunghezza dell'ottetto di trasferimento di una colonna può essere diversa dal numero di byte necessari per archiviare i dati nell'origine dati.  
  
 La lunghezza dell'ottetto di trasferimento definita per ogni tipo di dati SQL ODBC è illustrata nella tabella seguente.  
  
|Identificatore di tipo SQL|Length|  
|-------------------------|------------|  
|Tutti i tipi di carattere[a]|Lunghezza definita o massima (per il tipo di variabile) della colonna in byte. Si tratta dello stesso valore del campo del descrittore SQL_DESC_OCTET_LENGTH.|  
|SQL_DECIMAL<br />SQL_NUMERIC|Numero di byte necessari per contenere la rappresentazione dei caratteri di questi dati se il set di caratteri è ANSI e il doppio di questo numero se il set di caratteri è UNICODE. Questo è il numero massimo di cifre più due, perché i dati vengono restituiti come una stringa di caratteri e i caratteri sono necessari per le cifre, un segno e un separatore decimale. Ad esempio, la lunghezza di trasferimento di una colonna definita come NUMERIC(10,3) è 12.|  
|SQL_TINYINT|1|  
|SQL_SMALLINT|2|  
|SQL_INTEGER|4|  
|SQL_BIGINT| 8 |  
|SQL_REAL|4|  
|SQL_FLOAT|8|  
|SQL_DOUBLE|8|  
|SQL_BIT|1|  
|Tutti i tipi binari[a]|Numero di byte necessari per contenere il numero di caratteri definito (per i tipi fissi) o massimo (per i tipi di variabile).|  
|SQL_TYPE_DATE<br />SQL_TYPE_TIME|6 (la dimensione della struttura SQL_DATE_STRUCT o SQL_TIME_STRUCT).|  
|SQL_TYPE_TIMESTAMP|16 (la dimensione della struttura SQL_TIMESTAMP_STRUCT).|  
|Tutti i tipi di dati intervallo|34 (la dimensione della struttura dell'intervallo).|  
|SQL_GUID|16 (la dimensione della struttura GUID).|  
| &nbsp; | &nbsp; |

 [a] Se il driver non è in grado di determinare la lunghezza della colonna o del parametro per i tipi di variabile, restituisce SQL_NO_TOTAL.
