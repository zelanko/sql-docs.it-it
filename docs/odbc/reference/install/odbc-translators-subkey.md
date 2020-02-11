---
title: Sottochiave ODBC Translator | Microsoft Docs
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
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68093938"
---
# <a name="odbc-translators-subkey"></a>Sottochiave ODBC Translators
I valori nella sottochiave ODBC Translators elencano i traduttori installati. Il formato di questi valori è illustrato nella tabella seguente.  
  
|Nome|Tipo di dati|data|  
|----------|---------------|----------|  
|*Translator-DESC*|REG_SZ|**Installato**|  
  
 Il nome *Translator-desc* viene definito dallo sviluppatore del traduttore.  
  
 Si supponga, ad esempio, che un utente abbia installato Microsoft® Code page translator e un convertitore ASCII personalizzato per EBCDIC. I valori nella sottochiave ODBC Translators potrebbero essere i seguenti:  
  
```  
MS Code Page Translator: REG_SZ : Installed  
ASCII to EBCDIC: REG_SZ : Installed.  
```
