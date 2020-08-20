---
description: Sottochiavi di specifica dei convertitori
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c02317c8abe12dbc693cdf7b715b6de84e5bc631
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461293"
---
# <a name="translator-specification-subkeys"></a>Sottochiavi di specifica dei convertitori
Ogni traduttore elencato nella sottochiave dei convertitori ODBC dispone di una sottochiave. Questa sottochiave ha lo stesso nome del valore corrispondente nella sottochiave ODBC Translator. I valori in questa sottochiave elencano i percorsi completi delle DLL di installazione di Translator e Translator e il conteggio di utilizzo. I formati dei valori sono indicati nella tabella seguente.  
  
|Nome|Tipo di dati|Data|  
|----------|---------------|----------|  
|Funzione di conversione|REG_SZ|*translator-DLL-percorso*|  
|Configurazione|REG_SZ|*programma di installazione-DLL-percorso*|  
|UsageCount|REG_DWORD|*count*|  
  
 Per informazioni sui conteggi di utilizzo, vedere [conteggio di utilizzo](../../../odbc/reference/install/usage-counting.md) in precedenza in questa sezione.  
  
 Le applicazioni non devono impostare il conteggio dell'utilizzo. Il conteggio verrà mantenuto da ODBC.  
  
 Si supponga, ad esempio, che il convertitore della tabella codici Microsoft disponga di una DLL di traduzione denominata Mscpxl32.dll, che le funzioni di installazione del convertitore si trovino nella stessa DLL e che il traduttore sia stato installato tre volte. I valori nella sottochiave di conversione della tabella codici Microsoft potrebbero essere i seguenti:  
  
```  
Translator : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
UsageCount : REG_DWORD : 0x3  
```
