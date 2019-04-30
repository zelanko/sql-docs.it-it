---
title: Sottochiavi di specifica dell'origine dati | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data source specification subkeys [ODBC]
- registry entries for data sources [ODBC], data source specification subkeys
- subkeys [ODBC], data source specification subkeys
ms.assetid: d7e88a07-e6ab-4258-a45d-1ca21234fbec
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ad210f91d00f9e692c8ee20fef01a808a01501c3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63198212"
---
# <a name="data-source-specification-subkeys"></a>Sottochiavi di specifica dell'origine dati
Ogni origine dati elencate nella sottochiave ODBC Zdroje dat ha una sottochiave propri. Questa sottochiave ha lo stesso nome come valore corrispondente nella sottochiave origini dati ODBC. I valori sotto questa sottochiave necessario elencare la DLL del driver e possono elencare una descrizione dell'origine dati. Se il driver supporta i traduttori, i valori possono elencare il nome di una funzione di conversione predefinita, la DLL di conversione predefinita e l'opzione di conversione predefinita. I valori possono inoltre essere elencate altre informazioni richieste dal driver per la connessione all'origine dati. Ad esempio, il driver potrebbe richiedere un nome del server, nome del database o nome dello schema.  
  
 I formati dei valori vengono visualizzati nella tabella seguente. È necessario solo il valore di Driver.  
  
|Nome|Tipo di dati|Dati|  
|----------|---------------|----------|  
|Descrizione|REG_SZ|*description*|  
|Driver|REG_SZ|*driver-DLL-path*|  
|TranslationDLL|REG_SZ|*translator-DLL-path*|  
|TranslationName|REG_SZ|*translator-name*|  
|TranslationOption|REG_SZ|*translation-option*|  
|*opt-value-name*|*opt-value-type*|*opt-value-data*|  
  
 Si supponga, ad esempio, il driver SQL Server richiede il nome del server e un flag per OEM per la conversione ANSI e definisce i valori del Server e non vengono per questi. Si supponga inoltre che l'origine dati di inventario utilizza il convertitore di tabella codici di Microsoft® per la conversione tra tabelle codici multilingue (850) e il Windows® latino 1 (1250). I valori nella sottochiave inventario potrebbero essere come segue:  
  
```  
Description : REG_SZ : Inventory database on server InvServ  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\SQLSRV32.DLL  
OEMTOANSI : REG_SZ : Yes  
Server : REG_SZ : InvServ  
TranslationDLL : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
TranslationName : REG_SZ : MS Code Page Translator  
TranslationOption : REG_SZ : 12500850  
```
