---
description: Uso delle stringhe di connessione
title: Uso di stringhe di connessione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connection strings [ODBC]
- connecting to data source [ODBC], Visual FoxPro
- Visual FoxPro data source [ODBC], connecting
ms.assetid: 57634960-47e9-49bf-95c1-6e3702ac8166
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3ae8c3b1eda098a506d273f0d7baafec40985813
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471353"
---
# <a name="using-connection-strings"></a>Uso delle stringhe di connessione
È possibile usare una stringa di connessione per connettersi a un'origine dati Visual FoxPro.  
  
 Ad esempio, per connettersi all'origine dati TasTrade ed eseguire l'override dell'impostazione corrente di Exclusive associate all'origine dati, è necessario utilizzare la stringa:  
  
```  
DSN=TasTrade;Exclusive=Yes  
```  
  
 Per un elenco delle parole chiave e dei valori degli attributi che è possibile includere nella stringa di connessione, vedere [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md).  
  
 Per una spiegazione completa della sintassi delle stringhe di connessione, vedere [SQLBrowseConnect](../../odbc/reference/syntax/sqlbrowseconnect-function.md) in *ODBC Programmer ' s Reference*.
