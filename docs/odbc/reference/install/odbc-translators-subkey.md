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
ms.openlocfilehash: 7d26f2d33d81e08cfe4bddff9b2260bd2f098f00
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093938"
---
# <a name="odbc-translators-subkey"></a>Sottochiave ODBC Translators
I valori nella sottochiave ODBC Translators elencare i traduttori installati. Nella tabella seguente viene illustrato il formato di questi valori.  
  
|NOME|Tipo di dati|Data|  
|----------|---------------|----------|  
|*translator-desc*|REG_SZ|**installato**|  
  
 Il *traduttore desc* nome è definito dallo sviluppatore di Microsoft translator.  
  
 Ad esempio, si supponga che un utente ha installato un ASCII personalizzato e il convertitore di tabella codici di Microsoft® per Microsoft translator EBCDIC. I valori nella sottochiave ODBC Translators potrebbero essere come segue:  
  
```  
MS Code Page Translator: REG_SZ : Installed  
ASCII to EBCDIC: REG_SZ : Installed.  
```
