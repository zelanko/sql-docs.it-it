---
title: Sottochiave le origini dati ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], for data sources
- data sources [ODBC], subkeys
- registry entries for data sources [ODBC], subkeys
ms.assetid: 0a8ccb80-c573-4418-84e5-f04a2b0e2ac1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9867946ce84163a504582c8a9575100c3c9aacd3
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63069820"
---
# <a name="odbc-data-sources-subkey"></a>Sottochiave ODBC Data Sources
I valori nella sottochiave origini dati ODBC elencare le origini dati. Il formato di questi valori è come illustrato nella tabella seguente.  
  
|Nome|Tipo di dati|Dati|  
|----------|---------------|----------|  
|*data-source-name*|REG_SZ|*driver-description*|  
  
 Il *nome dell'origine dati* valore viene definito dal programma di amministrazione (che in genere richiesto all'utente per tale), e *driver-description* è definito dallo sviluppatore del driver (in genere è il nome del DBMS associato con il driver).  
  
 Ad esempio, si supponga che i dati di tre origini sono state definite: Inventario, che Usa SQL Server. Libro paga, che usa dBASE; e personale, che usa i file di testo in formato. I valori nella sottochiave origini dati ODBC potrebbero essere come segue:  
  
```  
Inventory : REG_SZ : SQL Server  
Payroll : REG_SZ : dBASE  
Personnel : REG_SZ : Text  
```
