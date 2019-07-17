---
title: Sottochiave ODBC Core | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], core subkey
- registry entries for components [ODBC], core subkey
- core subkey [ODBC]
ms.assetid: 055b31fc-f96c-450b-a596-d4570079fbf2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 98c9380083eb5a0ad796f436af271564676b757d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68094015"
---
# <a name="odbc-core-subkey"></a>Sottochiave ODBC Core
Il valore della sottochiave ODBC Core fornisce il conteggio di utilizzo per i componenti di base (gestione Driver, libreria di cursori, programma di installazione di DLL e così via). Nella tabella seguente viene illustrato il formato di questo valore.  
  
|Name|Tipo di dati|Data|  
|----------|---------------|----------|  
|UsageCount|REG_DWORD|*count*|  
  
 Si supponga, ad esempio, che sono stati installati i componenti di base di ODBC per i programmi di installazione per tre diverse applicazioni e i due diversi driver. Il valore della sottochiave ODBC Core sarebbe:  
  
```  
UsageCount : REG_DWORD : 0x5  
```
