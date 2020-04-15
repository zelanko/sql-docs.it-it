---
title: Sottochiave dei traduttori ODBC Documenti Microsoft
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
ms.openlocfilehash: 617416adfcddfbf041c48acbf83cb9589e34ae27
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296221"
---
# <a name="odbc-translators-subkey"></a>Sottochiave ODBC Translators
I valori nella sottochiave ODBC Translators elencano i traduttori installati. Il formato di questi valori è illustrato nella tabella seguente.  
  
|Nome|Tipo di dati|Data|  
|----------|---------------|----------|  
|*traduttore-desc*|REG_SZ|**Installato**|  
  
 Il nome *del traduttore-desc* è definito dallo sviluppatore del traduttore.  
  
 Si supponga, ad esempio, che un utente abbia installato Microsoft® Code Page Translator e un ASCII personalizzato per il traduttore EBCDIC. I valori nella sottochiave ODBC Translators potrebbero essere i seguenti:  
  
```  
MS Code Page Translator: REG_SZ : Installed  
ASCII to EBCDIC: REG_SZ : Installed.  
```
