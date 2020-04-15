---
title: Utilizzo delle stringhe di connessione . Documenti Microsoft
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
ms.openlocfilehash: 9083414503606720a40d372ed883a140953dc415
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307592"
---
# <a name="using-connection-strings"></a>Uso delle stringhe di connessione
È possibile utilizzare una stringa di connessione per connettersi a un'origine dati Visual FoxPro.You can use a connection string to connect to a Visual FoxPro data source.  
  
 Ad esempio, per connettersi all'origine dati TasTrade ed eseguire l'override dell'impostazione corrente Di Esclusiva associata all'origine dati, è necessario utilizzare la stringa:  
  
```  
DSN=TasTrade;Exclusive=Yes  
```  
  
 Per un elenco delle parole chiave e dei valori degli attributi che è possibile includere nella stringa di connessione, vedere [SQLDriverConnect](../../odbc/microsoft/sqldriverconnect-visual-foxpro-odbc-driver.md).  
  
 Per una spiegazione completa della sintassi delle stringhe di connessione, vedere [SQLBrowseConnect](../../odbc/reference/syntax/sqlbrowseconnect-function.md) in *ODBC Programmer's Reference*.
