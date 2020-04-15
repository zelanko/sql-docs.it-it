---
title: Sottochiavi delle specifiche del traduttore Documenti Microsoft
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
ms.openlocfilehash: ad21943c5313edcb09aba88d45ea21132aa9757f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296041"
---
# <a name="translator-specification-subkeys"></a>Sottochiavi di specifica dei convertitori
Ogni traduttore elencato nella sottochiave ODBC Translators dispone di una sottochiave propria. Questa sottochiave ha lo stesso nome del valore corrispondente nella sottochiave ODBC Translators. I valori in questa sottochiave elencano i percorsi completi delle DLL di installazione del traduttore e del traduttore e il conteggio di utilizzo. I formati dei valori sono come illustrato nella tabella seguente.  
  
|Nome|Tipo di dati|Data|  
|----------|---------------|----------|  
|Funzione di conversione|REG_SZ|*percorso DLL-traduttore*|  
|Configurazione|REG_SZ|*setup-DLL-percorso*|  
|UsageCount|REG_DWORD|*count*|  
  
 Per informazioni sui conteggi di utilizzo, vedere [Conteggio dati di utilizzo](../../../odbc/reference/install/usage-counting.md) più indietro in questa sezione.  
  
 Le applicazioni non devono impostare il conteggio di utilizzo. ODBC manterrà questo conteggio.  
  
 Si supponga, ad esempio, che Microsoft Code Page Translator disponga di una DLL di conversione denominata Mscpxl32.dll, che le funzioni di installazione del convertitore si trovino nella stessa DLL e che il traduttore sia stato installato tre volte. I valori nella sottochiave Microsoft Code Page Translator potrebbero essere i seguenti:  
  
```  
Translator : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
UsageCount : REG_DWORD : 0x3  
```
