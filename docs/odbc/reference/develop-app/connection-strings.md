---
title: Stringhe di connessione - Documenti Microsoft
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: bbbb5b4672a8ea393380063887cfd77b3e910238
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299031"
---
# <a name="connection-strings"></a>Stringhe di connessione
Una stringa di connessione contiene informazioni utilizzate per stabilire una connessione. Una stringa di connessione completa contiene tutte le informazioni necessarie per stabilire una connessione. La stringa di connessione è una serie di coppie parola chiave/valore separate da punto e virgola. (Per la sintassi completa di una stringa di connessione, vedere il [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) descrizione della funzione.) La stringa di connessione viene utilizzata da:The connection string is used by:  
  
-   **SQLDriverConnect**, che completa la stringa di connessione in base all'interazione con l'utente.  
  
-   **SQLBrowseConnect**, che completa la stringa di connessione in modo iterativo con l'origine dati.  
  
 **SQLConnect** non utilizza una stringa di connessione; l'utilizzo di **SQLConnect** è analogo alla connessione tramite una stringa di connessione con esattamente tre coppie parola chiave/valore (per il nome dell'origine dati e, facoltativamente, per l'ID utente e la password).
