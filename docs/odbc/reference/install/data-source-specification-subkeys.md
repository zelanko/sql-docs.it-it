---
title: Sottochiavi di specifica dell'origine dati Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 281377c307f3f3750e87bf5dc988beb7660067af
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300341"
---
# <a name="data-source-specification-subkeys"></a>Sottochiavi di specifica dell'origine dati
Ogni origine dati elencata nella sottochiave Origini dati ODBC dispone di una sottochiave propria. Questa sottochiave ha lo stesso nome del valore corrispondente nella sottochiave Origini dati ODBC. I valori in questa sottochiave devono elencare la DLL del driver e possono elencare una descrizione dell'origine dati. Se il driver supporta i convertitori, i valori possono elencare il nome di un traduttore predefinito, la DLL di conversione predefinita e l'opzione di conversione predefinita. I valori possono anche elencare altre informazioni richieste dal driver per connettersi all'origine dati. Ad esempio, il driver potrebbe richiedere un nome di server, un nome di database o un nome di schema.  
  
 I formati dei valori sono come illustrato nella tabella seguente. È necessario solo il valore Driver.  
  
|Nome|Tipo di dati|Data|  
|----------|---------------|----------|  
|Descrizione|REG_SZ|*Descrizione*|  
|Driver|REG_SZ|*driver-DLL-percorso*|  
|Dll di traduzione|REG_SZ|*percorso DLL-traduttore*|  
|NomeTraduzione|REG_SZ|*traduttore-nome*|  
|TranslationOption (Opzione)TranslationOption (|REG_SZ|*opzione di traduzione*|  
|*opt-value-name*|*opt-value-type*|*opt-value-data*|  
  
 Si supponga, ad esempio, che il driver di SQL Server richieda il nome del server e un flag per la conversione da OEM ad ANSI e definisca i valori Server e OEMTOANSI per questi. Si supponga inoltre che l'origine dati di inventario utilizzi le tabelle codici di Microsoft® per la conversione tra le tabelle codici di Windows® Latin 1 (1250) e multilingue (850). I valori nella sottochiave Inventory potrebbero essere i seguenti:  
  
```  
Description : REG_SZ : Inventory database on server InvServ  
Driver : REG_SZ : C:\WINDOWS\SYSTEM32\SQLSRV32.DLL  
OEMTOANSI : REG_SZ : Yes  
Server : REG_SZ : InvServ  
TranslationDLL : REG_SZ : C:\WINDOWS\SYSTEM32\MSCPXL32.DLL  
TranslationName : REG_SZ : MS Code Page Translator  
TranslationOption : REG_SZ : 12500850  
```
