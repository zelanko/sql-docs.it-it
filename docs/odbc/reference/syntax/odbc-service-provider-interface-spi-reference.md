---
description: Informazioni di riferimento sull'interfaccia del provider di servizi (SPI) ODBC
title: Guida di riferimento all'interfaccia del provider di servizi (SPI) ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cdeffb4a-f344-4abe-97f3-be2ede1c8e59
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7ef1eea6dd78537169d3394c7d048d1829e8d9a5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487354"
---
# <a name="odbc-service-provider-interface-spi-reference"></a>Informazioni di riferimento sull'interfaccia del provider di servizi (SPI) ODBC
Tradizionalmente, ODBC definisce un Application Programming Interface (API). Le funzioni nell'API possono essere chiamate dalle applicazioni e devono essere implementate all'interno di gestione driver e del driver.  
  
 Con l'aggiunta della funzionalità di pool di connessioni compatibile con il driver, in ODBC è stata introdotta l'interfaccia del provider di servizi (SPI). Le funzioni nell'SPI vengono utilizzate per la comunicazione tra il driver e la gestione driver. Le funzioni SPI sono implementate dal driver; Gestione driver non espone le funzioni SPI alle applicazioni. Le applicazioni non devono chiamare direttamente queste funzioni.  
  
 Includere sqlspi. h per lo sviluppo di driver ODBC.  
  
 Questa sezione contiene i seguenti argomenti  
  
-   [SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqlcleanupconnectionpoolid-function.md)  
  
-   [SQLGetPoolID](../../../odbc/reference/syntax/sqlgetpoolid-function.md)  
  
-   [SQLPoolConnect](../../../odbc/reference/syntax/sqlpoolconnect-function.md)  
  
-   [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)  
  
-   [SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqlsetconnectattrfordbcinfo-function.md)  
  
-   [SQLSetConnectInfo](../../../odbc/reference/syntax/sqlsetconnectinfo-function.md)  
  
-   [SQLSetDriverConnectInfo](../../../odbc/reference/syntax/installation-and-configuration-wwi-oltp.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di un driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Sviluppo della consapevolezza del pool di connessioni in un driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)   
 [Pool di connessioni di Gestione driver](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)
