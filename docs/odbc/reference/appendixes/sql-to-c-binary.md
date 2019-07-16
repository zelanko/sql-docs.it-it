---
title: 'Da SQL a C: Binary | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e280afb03eeac46a58943d276137e2019340a0a2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68057006"
---
# <a name="sql-to-c-binary"></a>Da SQL a C: Binary
Gli identificatori per i tipi di dati SQL ODBC binari sono:  
  
 SQL_BINARY  
  
 SQL_VARBINARY  
  
 SQL_LONGVARBINARY  
  
 Nella tabella seguente mostra i dati ODBC C i tipi di dati a cui possono essere convertiti i dati binari di SQL. Per una spiegazione delle colonne e le condizioni nella tabella, vedere [conversione di dati da SQL a tipi di dati C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md).  
  
|Identificatore di tipo C|Test|**TargetValuePtr*|**StrLen_or_IndPtr*|SQLSTATE|  
|-----------------------|----------|------------------------|----------------------------|--------------|  
|SQL_C_CHAR|(Lunghezza in byte dei dati) \* 2 < *BufferLength*<br /><br /> (Lunghezza in byte dei dati) \* 2 > = *BufferLength*|Data<br /><br /> Dati troncati|Lunghezza in byte dei dati<br /><br /> Lunghezza in byte dei dati|n/d<br /><br /> 01004|  
|SQL_C_WCHAR|(Lunghezza in caratteri di dati) \* 2 < *BufferLength*<br /><br /> (Lunghezza in caratteri di dati) \* 2 > = *BufferLength*|Data<br /><br /> Dati troncati|Lunghezza dei dati in caratteri<br /><br /> Lunghezza dei dati in caratteri|n/d<br /><br /> 01004|  
|SQL_C_BINARY|Lunghezza in byte dei dati < = *BufferLength*<br /><br /> Lunghezza in byte di dati > *BufferLength*|Data<br /><br /> Dati troncati|Lunghezza in byte dei dati<br /><br /> Lunghezza in byte dei dati|n/d<br /><br /> 01004|  
  
 Quando i dati binari di SQL viene convertiti in dati di tipo carattere C, ogni byte (8 bit) dei dati di origine è rappresentata come due caratteri ASCII. Questi caratteri sono la rappresentazione di caratteri ASCII del numero in formato esadecimale. Ad esempio, un 00000001 binario viene convertito in "01" e un binario 11111111 viene convertito in "FF".  
  
 Il driver converte singoli byte alle coppie di cifre esadecimali sempre e termina la stringa di caratteri con un byte null. Per questo motivo, se *BufferLength* è pari ed è minore della lunghezza dei dati convertiti, l'ultimo byte del **TargetValuePtr* buffer non viene utilizzato. (I dati convertiti richiedono un numero pari di byte, il byte successivo all'ultima è un byte null e non può essere utilizzato l'ultimo byte.)  
  
> [!NOTE]  
>  Gli sviluppatori di applicazioni sono sconsigliati dall'associazione di dati binari SQL a un tipo di dati C di carattere. Questa conversione è in genere lenti e poco efficiente.
