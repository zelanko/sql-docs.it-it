---
title: Lunghezza trasferimento in ottetti | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d8f64172685c42a5dde8de9027c8c7e621ddd9f2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62735067"
---
# <a name="transfer-octet-length"></a>Lunghezza dell'ottetto di trasferimento
La lunghezza dell'ottetto di trasferimento di una colonna è il numero massimo di byte restituiti all'applicazione quando i dati vengono trasferiti al relativo tipo di dati C predefiniti. Per dati di tipo carattere, la lunghezza dell'ottetto di trasferimento non include lo spazio per il carattere di terminazione null. La lunghezza dell'ottetto di trasferimento di una colonna può essere diversa rispetto al numero di byte necessari per archiviare i dati nell'origine dati.  
  
 La lunghezza dell'ottetto di trasferimento definita per ogni tipo di dati SQL ODBC è illustrata nella tabella seguente.  
  
|Identificatore di tipo SQL|Length|  
|-------------------------|------------|  
|Tutti i tipi di carattere [a]|L'oggetto definito o la lunghezza massima (per tipo di variabile) della colonna in byte. Questo è lo stesso valore di campo di descrizione SQL_DESC_OCTET_LENGTH.|  
|SQL_DECIMAL<br />SQL_NUMERIC|Il numero di byte necessari per contenere la rappresentazione di caratteri di questi dati se il set di caratteri ANSI e due volte questo numero se il set di caratteri UNICODE. Questo è il numero massimo di cifre più di due, perché i dati vengono restituiti come una stringa di caratteri e caratteri necessari per le cifre, un segno e un separatore decimale. Ad esempio, la lunghezza di trasferimento di una colonna definita come NUMERIC(10,3) è 12.|  
|SQL_TINYINT|1|  
|SQL_SMALLINT|2|  
|SQL_INTEGER|4|  
|SQL_BIGINT|Il numero di byte necessari per contenere la rappresentazione di caratteri di questi dati se il set di caratteri ANSI e due volte questo numero, se il set di caratteri UNICODE, perché questo tipo di dati viene restituito come una stringa di caratteri per impostazione predefinita. La rappresentazione di caratteri è costituito da 20 caratteri: 19 cifre e un segno, se è firmato o 20 cifre, se senza segno. Pertanto, la lunghezza è 20.|  
|SQL_REAL|4|  
|SQL_FLOAT|8|  
|SQL_DOUBLE|8|  
|SQL_BIT|1|  
|Tutti i tipi binari [a]|Il numero di byte necessari per contenere l'oggetto definito (per tipi predefiniti) o numero massimo (tipi di variabile) di caratteri.|  
|SQL_TYPE_DATE<br />SQL_TYPE_TIME|6 (la dimensione della struttura del valore SQL_DATE_STRUCT o SQL_TIME_STRUCT).|  
|SQL_TYPE_TIMESTAMP|16 (le dimensioni della struttura di SQL_TIMESTAMP_STRUCT).|  
|Tutti i tipi di dati intervallo|34 (la dimensione della struttura di intervallo).|  
|SQL_GUID|16 (le dimensioni della struttura di GUID).|  
  
 [a] se il driver non è possibile determinare la lunghezza della colonna o del parametro per i tipi di variabili, restituirà SQL_NO_TOTAL.
