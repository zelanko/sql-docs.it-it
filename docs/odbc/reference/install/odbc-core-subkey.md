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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9e6bfcf3c1efa87076e6d3e27a438cde6f794157
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304056"
---
# <a name="odbc-core-subkey"></a>Sottochiave ODBC Core
Il valore nella sottochiave ODBC Core indica il numero di utilizzi per i componenti di base (Gestione driver, libreria di cursori, DLL del programma di installazione e così via). Il formato di questo valore è illustrato nella tabella seguente.  
  
|Nome|Tipo di dati|Data|  
|----------|---------------|----------|  
|UsageCount|REG_DWORD|*count*|  
  
 Si supponga, ad esempio, che i componenti di base di ODBC siano stati installati dai programmi di installazione per tre applicazioni diverse e due driver diversi. Il valore nella sottochiave ODBC core sarà:  
  
```  
UsageCount : REG_DWORD : 0x5  
```
