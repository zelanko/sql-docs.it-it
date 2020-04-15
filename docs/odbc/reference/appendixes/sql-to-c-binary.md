---
title: 'Da SQL a C: Binary Documenti Microsoft'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- converting data from SQL to c types [ODBC], binary
- binary data type [ODBC]
- data conversions from SQL to C types [ODBC], binary
- binary data transfers [ODBC]
ms.assetid: 8c519072-ae4c-4d32-9d4e-775e3d3d6389
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 70b0ce72f650e61b83ec99b0727752612d18da52
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298825"
---
# <a name="sql-to-c-binary"></a>Da SQL a C: dati binari
Gli identificatori per i tipi di dati SQL ODBC binari sono:  
  
 SQL_BINARY  
  
 SQL_VARBINARY  
  
 SQL_LONGVARBINARY  
  
 Nella tabella seguente vengono illustrati i tipi di dati ODBC C in cui è possibile convertire i dati SQL binari. Per una spiegazione delle colonne e dei termini nella tabella, vedere [Conversione di dati da SQL a tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificatore del tipo C|Test|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|(Lunghezza in byte dei dati) \* 2 < *BufferLength*<br /><br /> (Lunghezza in byte dei dati) \* 2 >- *BufferLength*|Data<br /><br /> Dati troncati|Lunghezza dei dati in byte<br /><br /> Lunghezza dei dati in byte|n/d<br /><br /> 01004|  
|SQL_C_WCHAR|(Lunghezza caratteri dei dati) \* 2 < *BufferLength*<br /><br /> (Lunghezza caratteri dei dati) \* 2 >- *BufferLength*|Data<br /><br /> Dati troncati|Lunghezza dei dati in caratteri<br /><br /> Lunghezza dei dati in caratteri|n/d<br /><br /> 01004|  
|SQL_C_BINARY|Lunghezza in byte dei dati <- *BufferLength*<br /><br /> Lunghezza in byte dei dati > *BufferLength*|Data<br /><br /> Dati troncati|Lunghezza dei dati in byte<br /><br /> Lunghezza dei dati in byte|n/d<br /><br /> 01004|  
  
 Quando i dati SQL binari vengono convertiti in dati di tipo carattere C, ogni byte (8 bit) dei dati di origine viene rappresentato da due caratteri ASCII. Questi caratteri sono la rappresentazione di caratteri ASCII del numero nella sua forma esadecimale. Ad esempio, un valore binario 00000001 viene convertito in "01" e un file binario 111111111 viene convertito in "FF".  
  
 Il driver converte sempre i singoli byte in coppie di cifre esadecimali e termina la stringa di caratteri con un byte null. Per questo motivo, se *BufferLength* è pari ed è minore della lunghezza dei dati convertiti, non viene utilizzato l'ultimo byte del buffer*TargetValuePtr.* I dati convertiti richiedono un numero pari di byte, il byte successivo all'ultimo è un byte null e non è possibile utilizzare l'ultimo byte.  
  
> [!NOTE]  
>  Gli sviluppatori di applicazioni sono sconsigliati dall'associazione di dati SQL binari a un tipo di dati carattere C.Application developers are discouraged from binding binary SQL data to a character C data type. Questa conversione è solitamente inefficiente e lenta.
