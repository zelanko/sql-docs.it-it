---
title: Sottochiave Origini dati ODBC - Documenti Microsoft
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
ms.openlocfilehash: c5e97e643a78187b15e91833c832cd16ca435c7f
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304059"
---
# <a name="odbc-data-sources-subkey"></a>Sottochiave Origini dati ODBC

I valori `ODBC Data Sources` nella sottochiave elencano le origini dati. Il formato di questi valori è illustrato nella tabella seguente.

| Nome | Tipo di dati | Data |
| :--- | :-------- | :--- |
| *nome origine dati* | REG_SZ | *descrizione del conducente* |
| &nbsp; | &nbsp; | &nbsp; |

Il valore *data-source-name* è definito dal programma di amministrazione (che in genere richiede all'utente per esso) e *driver-descrizione* è definita dallo sviluppatore del driver (in genere è il nome del DBMS associato al driver).

Si supponga, ad esempio, che siano state definite tre origini dati: Inventory, che utilizza SQL Server; Retribuzioni, che utilizza dBASE; e Personale, che utilizza file di testo formattati. I valori `ODBC Data Sources` nella sottochiave potrebbero essere i seguenti:

```console
Inventory : REG_SZ : SQL Server
Payroll : REG_SZ : dBASE
Personnel : REG_SZ : Text
```
