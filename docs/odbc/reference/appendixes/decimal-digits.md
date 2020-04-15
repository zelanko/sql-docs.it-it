---
title: Cifre decimali Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4921a6162b6d711e657f223b5be5783dfa37bca8
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285161"
---
# <a name="decimal-digits"></a>Cifre decimali
Le *cifre decimali* dei tipi di dati decimali e numerici sono definite come il numero massimo di cifre a destra del separatore decimale o la scala dei dati. Per colonne o parametri approssimativi di numeri a virgola mobile, la scala non è definita perché il numero di cifre a destra del separatore decimale non è fisso. Per i dati datetime o interval che contengono un componente secondi, le cifre decimali sono definite come il numero di cifre a destra del separatore decimale nel componente secondi dei dati.  
  
 Per i tipi di dati SQL_DECIMAL e SQL_NUMERIC, la scala massima è in genere la stessa della precisione massima. Tuttavia, alcune origini dati impongono un limite separato sulla scala massima. Per determinare le scale minime e massime consentite per un tipo di dati, un'applicazione chiama **SQLGetTypeInfo**.  
  
 Le cifre decimali definite per ogni tipo di dati SQL conciso sono illustrate nella tabella seguente.  
  
|Tipo SQL|Cifre decimali|  
|--------------|--------------------|  
|Tutti i caratteri e i tipi binari[a]|n/d|  
|SQL_DECIMAL<br />SQL_NUMERIC|Numero definito di cifre a destra del separatore decimale. Ad esempio, la scala di una colonna definita come NUMERIC(10,3) è 3. Questo può essere un numero negativo per supportare l'archiviazione di numeri molto grandi senza usare la notazione esponenziale; ad esempio, "12000" potrebbe essere memorizzato come "12" con una scala di -3.|  
|Tutti i tipi numerici esatti diversi da SQL_DECIMAL e SQL_NUMERIC[a]|0|  
|Tutti i tipi di dati approssimativi[a]|n/d|  
|SQL_TYPE_DATE e tutti i tipi di intervallo senza componente secondi[a]|n/d|  
|Tutti i tipi datetime ad eccezione di SQL_TYPE_DATE e tutti i tipi di intervallo con un componente secondi|Il numero di cifre a destra del separatore decimale nella parte dei secondi del valore (secondi frazionari). Questo numero non può essere negativo.|  
|SQL_GUID|n/d|  
  
 L'argomento *DecimalDigits* di **SQLBindParameter** viene ignorato per questo tipo di dati.  
  
 I valori restituiti per le cifre decimali non corrispondono ai valori in un campo descrittore. I valori possono provenire dal campo SQL_DESC_SCALE o SQL_DESC_PRECISION, a seconda del tipo di dati, come illustrato nella tabella seguente.  
  
|Tipo SQL|Campo descrittore corrispondente a<br /><br /> cifre decimali|  
|--------------|----------------------------------------------------------|  
|Tutti i tipi di caratteri e binari|n/d|  
|Tutti i tipi numerici esatti|SCALE|  
|SQL_BIT|n/d|  
|Tutti i tipi numerici approssimativi|n/d|  
|Tutti i tipi datetime|PRECISION|  
|Tutti i tipi di intervallo con un componente secondi|PRECISION|  
|Tutti i tipi di intervallo senza componente secondi|n/d|
