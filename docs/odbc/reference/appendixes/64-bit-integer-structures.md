---
title: Strutture Integer a 64 bit Documenti Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- C data types [ODBC], 64-bit integer structures
- data types [ODBC], C data types
- 64-bit integer structures [ODBC]
ms.assetid: ac80c798-d9b2-4430-85ed-bd2461db0ac7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1ecbe4dae4c1bd21ac3d542ee0d9b18169df0116
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307512"
---
# <a name="64-bit-integer-structures"></a>Strutture di interi a 64 bit
Il tipo C per gli identificatori dei tipi di dati SQL_C_SBIGINT e SQL_C_UBIGINT nei compilatori Microsoft C è _int64. Quando viene utilizzato un compilatore diverso da un compilatore Microsoft® C, il tipo C potrebbe essere diverso. Se il compilatore supporta gli interi a 64 bit in modo nativo, il driver o l'applicazione deve definire ODBCINT64 come tipo integer nativo a 64 bit. Se il compilatore non supporta in modo nativo numeri interi a 64 bit, un'applicazione o un driver può definire le strutture seguenti per garantire che abbia accesso a questi dati:If the compiler does not support 64-bit integers natively, an application or driver can define the following structures to ensure that it has access to this data:  
  
```  
typedef struct{  
SQLUINTEGER dwLowWord;  
SQLUINTEGER dwHighWord;  
} SQLUBIGINT  
  
typedef struct{  
SQLUINTEGER dwLowWord;  
SQLINTEGER sdwHighWord;  
} SQLBIGINT  
```  
  
 Queste strutture devono essere allineate a un limite a 8 byte perché un numero intero a 64 bit è allineato al limite di 8 byte.
