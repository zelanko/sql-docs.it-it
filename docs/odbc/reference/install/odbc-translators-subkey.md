---
title: Sottochiave ODBC Translators | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- translator subkey [ODBC]
- subkeys [ODBC], translator subkey
- registry entries for components [ODBC], translator subkey
ms.assetid: 6b170f1f-e263-4aac-9d49-8d0ca0470ca2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e7109a6f1b88cf7639b2fc823ce0c5f14d05002
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63280785"
---
# <a name="odbc-translators-subkey"></a>Sottochiave ODBC Translators
I valori nella sottochiave ODBC Translators elencare i traduttori installati. Nella tabella seguente viene illustrato il formato di questi valori.  
  
|Nome|Tipo di dati|Dati|  
|----------|---------------|----------|  
|*translator-desc*|REG_SZ|**installato**|  
  
 Il *traduttore desc* nome è definito dallo sviluppatore di Microsoft translator.  
  
 Ad esempio, si supponga che un utente ha installato un ASCII personalizzato e il convertitore di tabella codici di Microsoft® per Microsoft translator EBCDIC. I valori nella sottochiave ODBC Translators potrebbero essere come segue:  
  
```  
MS Code Page Translator: REG_SZ : Installed  
ASCII to EBCDIC: REG_SZ : Installed.  
```
