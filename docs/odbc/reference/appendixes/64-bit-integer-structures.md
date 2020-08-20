---
description: Strutture di interi a 64 bit
title: Strutture Integer a 64 bit | Microsoft Docs
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
ms.openlocfilehash: 13c57fc582b23c3ca10768c930d44ae758f1d3d6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471244"
---
# <a name="64-bit-integer-structures"></a>Strutture di interi a 64 bit
Il tipo C per gli identificatori del tipo di dati SQL_C_SBIGINT e SQL_C_UBIGINT sui compilatori Microsoft C è _int64. Quando si usa un compilatore diverso da un compilatore Microsoft® C, il tipo C potrebbe essere diverso. Se il compilatore supporta interi a 64 bit a livello nativo, il driver o l'applicazione deve definire ODBCINT64 come tipo Integer nativo a 64 bit. Se il compilatore non supporta Integer a 64 bit a livello nativo, un'applicazione o un driver può definire le strutture seguenti per assicurarsi che disponga dell'accesso a questi dati:  
  
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
  
 Queste strutture devono essere allineate a un limite di 8 byte perché un intero a 64 bit è allineato al limite di 8 byte.
