---
title: Cifre decimali | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- size of data types [ODBC]
- decimal digits of data types [ODBC]
- data types [ODBC], decimal digits
- SQL data types [ODBC], column characteristics
ms.assetid: 07f3d1fc-b4ee-4693-b342-330b2231b6d0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f7b9a69941364b32e6b43d79f2d092511fd61f22
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/28/2018
ms.locfileid: "52506079"
---
# <a name="decimal-digits"></a>Cifre decimali
Il *cifre decimali* di dati decimali e numerici tipi viene definito come il numero massimo di cifre a destra del separatore decimale, o la scala dei dati. Per le colonne di numeri approssimative a virgola mobile o parametri, la scala è definita, poiché il numero di cifre a destra del separatore decimale non è fisso. Per datetime o intervallo di dati che contiene un componente di secondi, le cifre decimali viene definito come il numero di cifre a destra del separatore decimale nel componente di secondi di dati.  
  
 Per i tipi di dati SQL_DECIMAL e SQL_NUMERIC, la scala massima corrisponde in genere la precisione massima. Tuttavia, alcune origini dati previsto un limite separato per la scala massima. Per determinare le scale minime e massime consentite per un tipo di dati, un'applicazione chiama **SQLGetTypeInfo**.  
  
 Le cifre decimali definite per ogni tipo di dati SQL concisa è illustrato nella tabella seguente.  
  
|Tipo SQL|Cifre decimali|  
|--------------|--------------------|  
|Tutti i tipi carattere e binario [a]|n/d|  
|SQL_DECIMAL<br />SQL_NUMERIC|Il numero definito di cifre a destra del separatore decimale. Ad esempio, la scala di una colonna definita come NUMERIC(10,3) è 3. Può trattarsi di un numero negativo per il supporto di archiviazione di numeri molto grandi senza utilizzare la notazione esponenziale. ad esempio, "12000" possono essere archiviate come "12" con una scala pari a -3.|  
|Tutti i tipi numerici esatti diversi da SQL_DECIMAL e SQL_NUMERIC [a]|0|  
|Tutti i tipi di dati approssimati [a]|n/d|  
|SQL_TYPE_DATE e tutti i tipi di intervallo con alcun componente di secondi [a]|n/d|  
|Tutti i tipi di data/ora eccetto SQL_TYPE_DATE e tutti i tipi di intervallo con un componente relativo ai secondi|Il numero di cifre a destra del separatore decimale nella parte relativa ai secondi del valore (secondi frazionari). Questo numero non può essere negativo.|  
|SQL_GUID|n/d|  
  
 [a] il *DecimalDigits* argomenti del **SQLBindParameter** viene ignorata per questo tipo di dati.  
  
 I valori restituiti per le cifre decimali non corrispondono ai valori in qualsiasi campo del descrittore uno. I valori possono provenire dal SQL_DESC_SCALE o il campo SQL_DESC_PRECISION, a seconda del tipo di dati, come illustrato nella tabella seguente.  
  
|Tipo SQL|Campo di descrizione corrispondente a<br /><br /> Cifre decimali|  
|--------------|----------------------------------------------------------|  
|Tutti i tipi carattere e binario|n/d|  
|Tutti i tipi numerici esatti|SCALE|  
|SQL_BIT|n/d|  
|Tutti i tipi numerici approssimati|n/d|  
|Tutti i tipi di data/ora|PRECISION|  
|Tutti i tipi di intervallo con un componente relativo ai secondi|PRECISION|  
|Tutti i tipi di intervallo con alcun componente relativo ai secondi|n/d|
