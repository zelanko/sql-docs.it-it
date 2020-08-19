---
description: Stringhe di connessione
title: Stringhe di connessione | Microsoft Docs
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
ms.openlocfilehash: fbb2d4b0c80a93b225bac754d2905b27e8844cbb
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424773"
---
# <a name="connection-strings"></a>Stringhe di connessione
Una stringa di connessione contiene le informazioni utilizzate per stabilire una connessione. Una stringa di connessione completa contiene tutte le informazioni necessarie per stabilire una connessione. La stringa di connessione è una serie di coppie parola chiave/valore separate da punti e virgola. Per la sintassi completa di una stringa di connessione, vedere la descrizione della funzione [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) . La stringa di connessione viene utilizzata da:  
  
-   **SQLDriverConnect**, che completa la stringa di connessione per interazione con l'utente.  
  
-   **SQLBrowseConnect**, che completa la stringa di connessione in modo iterativo con l'origine dati.  
  
 **SQLConnect** non utilizza una stringa di connessione. l'utilizzo di **SQLConnect** è analogo alla connessione tramite una stringa di connessione con esattamente tre coppie parola chiave/valore (per il nome dell'origine dati e, facoltativamente, ID utente e password).
