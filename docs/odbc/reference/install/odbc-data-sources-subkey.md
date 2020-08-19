---
description: Sottochiave origini dati ODBC
title: Sottochiave origini dati ODBC | Microsoft Docs
ms.custom: ''
ms.date: 09/23/2019
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9897c68d110f59d03ac8e1b3e403ed21844082fb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448933"
---
# <a name="odbc-data-sources-subkey"></a>Sottochiave origini dati ODBC

I valori nella `ODBC Data Sources` sottochiave elencano le origini dati. Il formato di questi valori è illustrato nella tabella seguente.

| Nome | Tipo di dati | Data |
| :--- | :-------- | :--- |
| *nome origine dati* | REG_SZ | *Driver-Descrizione* |
| &nbsp; | &nbsp; | &nbsp; |

Il valore del *nome dell'origine dati* è definito dal programma di amministrazione (che in genere richiede l'utente) e *driver-Description* viene definito dallo sviluppatore del driver (si tratta in genere del nome del DBMS associato al driver).

Si supponga, ad esempio, che siano state definite tre origini dati: Inventory, che usa SQL Server; Payroll, che usa dBASE; e il personale, che usa file di testo formattato. I valori nella `ODBC Data Sources` sottochiave potrebbero essere i seguenti:

```console
Inventory : REG_SZ : SQL Server
Payroll : REG_SZ : dBASE
Personnel : REG_SZ : Text
```
