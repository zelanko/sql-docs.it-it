---
title: Tipi di dati di Microsoft Access - Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC desktop database drivers [ODBC], Access driver
- Jet-based ODBC drivers [ODBC], Access driver
- desktop database drivers [ODBC], Access driver
- Access driver [ODBC], data types
- access data types [ODBC]
- data types [ODBC], Access driver
ms.assetid: b537348a-bea0-4bd6-84a4-52a75292957f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 024fb65b6fdc81ae0a8e007d1cee150c6a35b91c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307730"
---
# <a name="microsoft-access-data-types"></a>Tipi di dati Microsoft Access
Nella tabella seguente vengono illustrati i tipi di dati di Microsoft Access, i tipi di dati utilizzati per creare tabelle e i tipi di dati SQL ODBC.  
  
|Tipo di dati di Microsoft Access|Tipo di dati (CREATETABLE)|Tipo di dati SQL ODBC|  
|--------------------------------|-------------------------------|------------------------|  
|BIGBINARY[1]|LONGBINARY (oggetto LONGBINARY)|SQL_LONGVARBINARY|  
|BINARY|BINARY|SQL_BINARY|  
|BIT|BIT|SQL_BIT|  
|Contatore|Contatore|SQL_INTEGER|  
|CURRENCY|CURRENCY|SQL_NUMERIC|  
|DATA/ORA|DATETIME|SQL_TIMESTAMP|  
|GUID|GUID|SQL_GUID|  
|BINARIO LUNGO|LONGBINARY (oggetto LONGBINARY)|SQL_LONGVARBINARY|  
|TESTO LUNGO|TESTO LUNGO|SQL_LONGVARCHAR[2] SQL_WLONGVARCHAR|  
|Memo|TESTO LUNGO|SQL_LONGVARCHAR[2] SQL_WLONGVARCHAR|  
|NUMERO (DimensioneCampo: SINGLE)|Singolo|SQL_REAL|  
|NUMERO (DimensioneCampo: DOUBLE)|DOUBLE|SQL_DOUBLE|  
|NUMERO (DimensioneCampo: BYTE)|BYTE NON CON SEGNO|SQL_TINYINT|  
|NUMERO (DimensioneCampo: INTEGER)|SHORT|SQL_SMALLINT|  
|NUMBER (FieldSize: LONG INTEGER)|LONG|SQL_INTEGER|  
|NUMERIC|NUMERIC|SQL_NUMERIC|  
|OLE|LONGBINARY (oggetto LONGBINARY)|SQL_LONGVARBINARY|  
|TEXT|VARCHAR|SQL_VARCHAR[1] SQL_WVARCHAR|  
|VARBINARY|VARBINARY|SQL_VARBINARY|  
  
 [1] Solo applicazioni Access 4.0. Lunghezza massima di 4000 byte. Comportamento simile a LONGBINARY.  
  
 [2] Solo applicazioni ANSI.  
  
 [3] Solo applicazioni Unicode e Access 4.0.  
  
> [!NOTE]  
>  **SQLGetTypeInfo** restituisce i tipi di dati ODBC. Non restituirà tutti i tipi di dati di Microsoft Access se più di un tipo di Microsoft Access è mappato allo stesso tipo di dati SQL ODBC. Tutte le conversioni nell'Appendice D di *ODBC Programmer's Reference* sono supportate per i tipi di dati SQL elencati nella tabella precedente.  
  
 Nella tabella seguente vengono illustrate le limitazioni relative ai tipi di dati di Microsoft Access.  
  
|Tipo di dati|Descrizione|  
|---------------|-----------------|  
|BINARY, VARBINARY e VARCHAR|La creazione di una colonna BINARY, VARBINARY o VARCHAR di lunghezza zero o non specificata restituisce in realtà una colonna di 510 byte.|  
|BYTE|Anche se un campo NUMBER di Microsoft Access con un FieldSize uguale a BYTE non è firmato, è possibile inserire un numero negativo nel campo quando si utilizza il driver di Microsoft Access.|  
|CHAR, LONGVARCHAR e VARCHAR|Un valore letterale stringa di caratteri può contenere qualsiasi carattere ANSI (1-255 decimale). Utilizzare due virgolette singole consecutive ('') per rappresentare una virgoletta singola (').<br /><br /> Le procedure devono essere utilizzate per passare dati di tipo carattere quando si utilizza qualsiasi carattere speciale in una colonna di tipo di dati carattere.|  
|DATE|I valori di data devono essere delimitati in base al formato di data canonico ODBC o delimitati dal delimitatore datetime ("-"). In caso contrario, Microsoft Access considererà il valore come un'espressione aritmetica e non genererà un avviso o un errore.<br /><br /> Ad esempio, la data "5 marzo 1996" deve essere rappresentata come "1996-03-05", o #03/05/1996; in caso contrario, se viene inviato solo il 03/05/1993, Microsoft Access valuterà 3 come 3 diviso 5 diviso per 1996. Questo valore arrotonda per esapero al numero intero 0 e poiché il giorno zero esegue il mapping al 1899-12-31, questa è la data utilizzata.<br /><br /> Un carattere barra verticale (&#124;) non può essere utilizzato in un valore di data, anche se racchiuso tra virgolette rovesciate.|  
|GUID|Tipo di dati limitato a Microsoft Access 4.0.|  
|NUMERIC|Tipo di dati limitato a Microsoft Access 4.0.|  
  
 Ulteriori limitazioni sui tipi di dati sono disponibili in [Limitazioni dei tipi](../../odbc/microsoft/data-type-limitations.md)di dati .
