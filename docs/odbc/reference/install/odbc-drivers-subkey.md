---
title: Sottochiave dei driver ODBC - Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: dd1f8d3293e35a543cce6b5079d9c6e10a331a88
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304032"
---
# <a name="odbc-drivers-subkey"></a>Sottochiave ODBC Drivers
I valori nella sottochiave Driver ODBC elencano i driver installati. Il formato di questi valori è illustrato nella tabella seguente.  
  
|Nome|Tipo di dati|Data|  
|----------|---------------|----------|  
|*descrizione del conducente*|REG_SZ|**Installato**|  
  
 Il nome *della descrizione del driver* è definito dallo sviluppatore del driver. In genere è il nome del DBMS associato al driver.  
  
 Si supponga, ad esempio, che siano stati installati driver per i file di testo formattati e SQL Server. I valori nella sottochiave Driver ODBC potrebbero essere:  
  
```  
Text : REG_SZ : Installed  
SQL Server : REG_SZ : Installed  
```
