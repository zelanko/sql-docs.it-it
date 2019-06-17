---
title: Strutture di interi a 64 bit | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ac1a80e94d225b26cf879b27bdb0e138e0b0d1d9
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63306329"
---
# <a name="64-bit-integer-structures"></a>Strutture di interi a 64 bit
Il tipo C per gli identificatori di tipo dati SQL_C_SBIGINT e SQL_C_UBIGINT nei compilatori Microsoft C è _int64. Quando viene utilizzato un compilatore diverso da un compilatore C Microsoft®, il tipo C potrebbe essere diverso. Se il compilatore supporta interi a 64 bit in modo nativo, il driver o l'applicazione deve definire ODBCINT64 per essere di tipo integer a 64 bit nativa. Se il compilatore non supporta valori interi a 64 bit in modo nativo, un'applicazione o driver può definire le strutture seguenti per verificare che possa accedere ai dati:  
  
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
  
 Queste strutture devono essere allineate a un limite di 8 byte perché un numero intero a 64 bit è allineato al limite di 8 byte.
