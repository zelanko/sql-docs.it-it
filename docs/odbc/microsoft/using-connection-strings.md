---
title: Uso delle stringhe di connessione | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 77bc54f857e04f31ccb982ca40b3ed6334664870
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "62633206"
---
# <a name="using-connection-strings"></a>Uso delle stringhe di connessione
È possibile usare una stringa di connessione per connettersi a un'origine dati Visual FoxPro.  
  
 Ad esempio, per connettersi all'origine dati TasTrade e l'impostazione corrente di esclusivo associato all'origine dati di sostituzione, utilizzare la stringa:  
  
```  
DSN=TasTrade;Exclusive=Yes  
```  
  
 Per un elenco dei valori è possibile includere nella stringa di connessione e di parole chiave di attributo, vedere [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md).  
  
 Per una spiegazione completa della sintassi della stringa di connessione, vedere [SQLBrowseConnect](../../odbc/reference/syntax/sqlbrowseconnect-function.md) nel *riferimento per programmatori ODBC*.
