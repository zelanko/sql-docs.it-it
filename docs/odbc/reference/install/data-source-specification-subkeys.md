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
ms.openlocfilehash: fae642b46b4c652583622ec4832b3217d0b1681c
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68068548"
---
# <a name="data-source-specification-subkeys"></a>Sottochiavi di specifica dell'origine dati
Ogni origine dati elencata nella sottochiave origini dati ODBC presenta una sottochiave. Questa sottochiave ha lo stesso nome del valore corrispondente nella sottochiave origini dati ODBC. I valori in questa sottochiave devono elencare la DLL del driver e possono elencare una descrizione dell'origine dati. Se il driver supporta i convertitori, i valori possono elencare il nome di un convertitore predefinito, la DLL di traduzione predefinita e l'opzione di conversione predefinita. I valori possono anche elencare altre informazioni richieste dal driver per la connessione all'origine dati. Ad esempio, il driver potrebbe richiedere il nome del server, il nome del database o il nome dello schema.  
  
 I formati dei valori sono indicati nella tabella seguente. È necessario solo il valore del driver.  
  
|Nome|Tipo di dati|data|  
|----------|---------------|----------|  
|Descrizione|REG_SZ|*Descrizione*|  
|Driver|REG_SZ|*Driver-DLL-Path*|  
|TranslationDLL|REG_SZ|*translator-DLL-percorso*|  
|Translationname|REG_SZ|*nome traduttore*|  
|TranslationOption|REG_SZ|*Translation-opzione*|  
|*nome-valore-opt*|*opt-valore-tipo*|*opt-value-dati*|  
  
 Si supponga, ad esempio, che il driver SQL Server richieda il nome del server e un flag per la conversione da OEM a ANSI e definisce i valori server e OEMTOANSI per questi. Si supponga inoltre che l'origine dati di inventario utilizzi il convertitore della tabella codici di Microsoft® per tradurre tra le tabelle codici di Windows® Latin 1 (1250) e multilingue (850). I valori nella sottochiave Inventory possono essere i seguenti:  
  
```  
Description : REG_SZ : Inventory database on server InvServ  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\SQLSRV32.DLL  
OEMTOANSI : REG_SZ : Yes  
Server : REG_SZ : InvServ  
TranslationDLL : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
TranslationName : REG_SZ : MS Code Page Translator  
TranslationOption : REG_SZ : 12500850  
```
