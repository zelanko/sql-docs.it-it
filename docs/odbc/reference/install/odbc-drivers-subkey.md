---
title: Sottochiave driver ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- subkeys [ODBC], drivers subkey
- registry entries for components [ODBC], drivers subkey
- drivers subkey [ODBC]
ms.assetid: 8edbf68f-d05d-4d77-92f6-e9500008f520
author: MightyPen
ms.author: genemi
ms.openlocfilehash: eb54ba7becad42d8d9d2c2870c02db37a3c7d89f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "68093986"
---
# <a name="odbc-drivers-subkey"></a>Sottochiave ODBC Drivers
I valori nella sottochiave ODBC Drivers elencano i driver installati. Il formato di questi valori è illustrato nella tabella seguente.  
  
|Nome|Tipo di dati|data|  
|----------|---------------|----------|  
|*Driver-Descrizione*|REG_SZ|**Installato**|  
  
 Il nome del *driver-Description* viene definito dallo sviluppatore del driver. Si tratta in genere del nome del DBMS associato al driver.  
  
 Si supponga, ad esempio, che i driver siano stati installati per i file di testo formattati e SQL Server. I valori nella sottochiave ODBC Drivers potrebbero essere:  
  
```  
Text : REG_SZ : Installed  
SQL Server : REG_SZ : Installed  
```
