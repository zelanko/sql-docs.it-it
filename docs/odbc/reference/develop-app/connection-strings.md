---
title: Le stringhe di connessione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection functions
- connecting to driver [ODBC], connection strings
- functions [ODBC], data source or driver connections
- connection strings [ODBC], about connection strings
- connecting to data source [ODBC], connection strings
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], functions
- connection functions [ODBC]
- ODBC drivers [ODBC], connection functions
ms.assetid: 724c7b86-300a-4fa9-ad96-4afa0fdcb3e9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d7e52ec70e53608f1af48b4abcd2dd1edb4fc454
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63042578"
---
# <a name="connection-strings"></a>Stringhe di connessione
Una stringa di connessione contiene informazioni utilizzate per stabilire una connessione. Una stringa di connessione completa contiene tutte le informazioni necessarie per stabilire una connessione. La stringa di connessione è una serie di coppie parola chiave/valore separate da punti e virgola. (Per la sintassi completa di una stringa di connessione, vedere la [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) descrizione della funzione.) La stringa di connessione è usata da:  
  
-   **SQLDriverConnect**, che viene completata la stringa di connessione per l'interazione con l'utente.  
  
-   **SQLBrowseConnect**, che viene completata la stringa di connessione in maniera iterativa con l'origine dati.  
  
 **SQLConnect** non usa una stringa di connessione; utilizzando **SQLConnect** è analoga alla connessione tramite una stringa di connessione con esattamente tre coppie parola chiave/valore (per nome dell'origine dati e, facoltativamente, l'utente ID e password) .
