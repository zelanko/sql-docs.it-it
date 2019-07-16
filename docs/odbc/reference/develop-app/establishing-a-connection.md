---
title: Stabilire una connessione | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection functions
- SQLBrowseConnect function [ODBC], establising a connection
- functions [ODBC], data source or driver connections
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], functions
- connection functions [ODBC]
- SQLConnect function [ODBC], establising a connection
- SQLDriverConnect function [ODBC], making a connection
- ODBC drivers [ODBC], connection functions
ms.assetid: 8e3c717e-35e3-47ef-b5d3-3a96eeb7b869
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6fd8d7a68e993aa6b35897ca14a7a87c08fc8763
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67901367"
---
# <a name="establishing-a-connection"></a>Istituzione di una connessione
Dopo l'allocazione di handle di ambiente e di connessione e impostando gli attributi di connessione, l'applicazione è pronta per la connessione all'origine dati o driver. Esistono tre funzioni differenti che l'applicazione può usare per eseguire questa operazione: **SQLConnect** (livello di conformità di interfaccia di base), **SQLDriverConnect** (Core), e **SQLBrowseConnect** (livello 1). Ognuno dei tre è progettato per essere usato in uno scenario diverso. Prima della connessione, l'applicazione può determinare quali di queste funzioni è supportata con il **ConnectFunctions** restituito dalla parola chiave **SQLDrivers**.  
  
> [!NOTE]  
>  Alcuni driver limitare il numero di connessioni attive che supportano. Un'applicazione chiama **SQLGetInfo** con l'opzione SQL_MAX_DRIVER_CONNECTIONS per determinare il numero di connessioni attivo supporta un driver specifico.  
  
 In questa sezione vengono trattati gli argomenti seguenti.  
  
-   [Origine dati predefinita](../../../odbc/reference/develop-app/default-data-source.md)  
  
-   [Connessione con SQLConnect](../../../odbc/reference/develop-app/connecting-with-sqlconnect.md)  
  
-   [Stringhe di connessione](../../../odbc/reference/develop-app/connection-strings.md)  
  
-   [Connessione con SQLDriverConnect](../../../odbc/reference/develop-app/connecting-with-sqldriverconnect.md)  
  
-   [Connessione con SQLBrowseConnect](../../../odbc/reference/develop-app/connecting-with-sqlbrowseconnect.md)
