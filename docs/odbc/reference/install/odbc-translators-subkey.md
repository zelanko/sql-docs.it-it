---
description: Sottochiave ODBC Translators
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 46308518f1f806cea21bbb824312d5269f8b61e4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499714"
---
# <a name="odbc-translators-subkey"></a>Sottochiave ODBC Translators
I valori nella sottochiave ODBC Translators elencano i traduttori installati. Il formato di questi valori è illustrato nella tabella seguente.  
  
|Nome|Tipo di dati|Data|  
|----------|---------------|----------|  
|*Translator-DESC*|REG_SZ|**Installato**|  
  
 Il nome *Translator-desc* viene definito dallo sviluppatore del traduttore.  
  
 Si supponga, ad esempio, che un utente abbia installato Microsoft® Code page translator e un convertitore ASCII personalizzato per EBCDIC. I valori nella sottochiave ODBC Translators potrebbero essere i seguenti:  
  
```  
MS Code Page Translator: REG_SZ : Installed  
ASCII to EBCDIC: REG_SZ : Installed.  
```
