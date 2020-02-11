---
title: Sottochiavi di specifica del traduttore | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- translator subkey [ODBC]
- registry entries for components [ODBC], translator specification subkeys
- translator specification subkeys [ODBC]
- subkeys [ODBC], translator specification subkeys
ms.assetid: 3c0edeee-d43a-4466-a177-bf2d2435707a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: ec94f3e02b720617e8f7369b12a916c2bbbe7b16
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68093803"
---
# <a name="translator-specification-subkeys"></a>Sottochiavi di specifica dei convertitori
Ogni traduttore elencato nella sottochiave dei convertitori ODBC dispone di una sottochiave. Questa sottochiave ha lo stesso nome del valore corrispondente nella sottochiave ODBC Translator. I valori in questa sottochiave elencano i percorsi completi delle DLL di installazione di Translator e Translator e il conteggio di utilizzo. I formati dei valori sono indicati nella tabella seguente.  
  
|Nome|Tipo di dati|data|  
|----------|---------------|----------|  
|Translator|REG_SZ|*translator-DLL-percorso*|  
|Installazione|REG_SZ|*programma di installazione-DLL-percorso*|  
|UsageCount|REG_DWORD|*conteggio*|  
  
 Per informazioni sui conteggi di utilizzo, vedere [conteggio di utilizzo](../../../odbc/reference/install/usage-counting.md) in precedenza in questa sezione.  
  
 Le applicazioni non devono impostare il conteggio dell'utilizzo. Il conteggio verrà mantenuto da ODBC.  
  
 Si supponga, ad esempio, che il convertitore della tabella codici Microsoft disponga di una DLL di traduzione denominata mscpxl32. dll, che le funzioni di installazione del convertitore si trovino nella stessa DLL e che il traduttore sia stato installato tre volte. I valori nella sottochiave di conversione della tabella codici Microsoft potrebbero essere i seguenti:  
  
```  
Translator : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
UsageCount : REG_DWORD : 0x3  
```
