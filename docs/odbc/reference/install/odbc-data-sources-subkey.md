---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4d6d54d1fc7c7742bf94e91d7370f356e28b5624
ms.sourcegitcommit: 816ff47eeab157c66e0f75f18897a63dc8033502
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 09/24/2019
ms.locfileid: "71207684"
---
# <a name="odbc-data-sources-subkey"></a>Sottochiave origini dati ODBC

I valori `ODBC Data Sources` nella sottochiave elencano le origini dati. Il formato di questi valori è illustrato nella tabella seguente.

| Nome | Tipo di dati | Data |
| :--- | :-------- | :--- |
| *nome origine dati* | REG_SZ | *driver-description* |
| &nbsp; | &nbsp; | &nbsp; |

Il valore del *nome dell'origine dati* è definito dal programma di amministrazione (che in genere richiede l'utente) e *driver-Description* viene definito dallo sviluppatore del driver (si tratta in genere del nome del DBMS associato al driver).

Si supponga, ad esempio, che siano state definite tre origini dati: Inventario, che usa SQL Server; Payroll, che usa dBASE; e il personale, che usa file di testo formattato. I valori nella `ODBC Data Sources` sottochiave potrebbero essere i seguenti:

```console
Inventory : REG_SZ : SQL Server
Payroll : REG_SZ : dBASE
Personnel : REG_SZ : Text
```
