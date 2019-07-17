---
title: Sottochiavi di specifica di Microsoft Translator | Microsoft Docs
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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093803"
---
# <a name="translator-specification-subkeys"></a>Sottochiavi di specifica dei convertitori
Ogni funzione di conversione elencate nella sottochiave ODBC Translators ha una sottochiave propri. Questa sottochiave ha lo stesso nome come valore della sottochiave ODBC Translators corrispondente. I valori sotto questa sottochiave elencare i percorsi completi della funzione di conversione e file DLL di installazione di Microsoft translator e il conteggio di utilizzo. I formati dei valori vengono visualizzati nella tabella seguente.  
  
|Name|Tipo di dati|Data|  
|----------|---------------|----------|  
|Funzione di conversione|REG_SZ|*translator-DLL-path*|  
|Configurazione|REG_SZ|*il programma di installazione-DLL-path*|  
|UsageCount|REG_DWORD|*count*|  
  
 Per informazioni su conteggi dell'utilizzo, vedere [Conteggio utilizzi](../../../odbc/reference/install/usage-counting.md) più indietro in questa sezione.  
  
 Le applicazioni non devono impostare il conteggio di utilizzo. ODBC manterrà questo conteggio.  
  
 Si supponga, ad esempio, la pagina di codice di Microsoft Translator ha una traduzione DLL denominata Mscpxl32, che le funzioni di installazione di Microsoft translator sono nella stessa DLL, e che la funzione di conversione sia stata installata per tre volte. I valori nella sottochiave Microsoft Translator pagina codice potrebbero essere come segue:  
  
```  
Translator : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
Setup : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
UsageCount : REG_DWORD : 0x3  
```
