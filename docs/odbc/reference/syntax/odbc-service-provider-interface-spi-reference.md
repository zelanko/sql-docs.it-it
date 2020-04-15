---
title: Riferimento all'interfaccia del provider di servizi ODBC (SPI) Documenti Microsoft
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
ms.openlocfilehash: e9739abd13bf2c4bed1b1b3a31c18c683594705a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298909"
---
# <a name="odbc-service-provider-interface-spi-reference"></a>Informazioni di riferimento sull'interfaccia del provider di servizi (SPI) ODBC
Tradizionalmente, ODBC definisce un'API (Application Programming Interface). Le funzioni nell'API possono essere chiamate dalle applicazioni e devono essere implementate all'interno di Gestione Driver e il driver.  
  
 Con l'aggiunta della funzionalità di pool di connessioni in grado di riconoscere i driver, ODBC introduce l'interfaccia del provider di servizi (SPI). Le funzioni nell'SPI vengono utilizzate per la comunicazione tra Gestione driver e il driver. Le funzioni SPI sono implementate dal driver; Gestione Driver non espone le funzioni SPI alle applicazioni. Le applicazioni non devono chiamare direttamente queste funzioni.  
  
 Includere sqlspi.h per lo sviluppo di driver ODBC.  
  
 Questa sezione contiene i seguenti argomenti  
  
-   [SQLCleanupConnectionPoolID (informazioni in lingua inglese)](../../../odbc/reference/syntax/sqlcleanupconnectionpoolid-function.md)  
  
-   [SQLGetPoolID (IDSQLGetPoolID)](../../../odbc/reference/syntax/sqlgetpoolid-function.md)  
  
-   [SQLPoolConnect (informazioni in lingua inglese)](../../../odbc/reference/syntax/sqlpoolconnect-function.md)  
  
-   [SQLRateConnection (connessione SQLRateConnection)](../../../odbc/reference/syntax/sqlrateconnection-function.md)  
  
-   [SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqlsetconnectattrfordbcinfo-function.md)  
  
-   [SQLSetConnectInfo (informazioni in lingua inglese)](../../../odbc/reference/syntax/sqlsetconnectinfo-function.md)  
  
-   [SQLSetDriverConnectInfo (informazioni in lingua inglese)](../../../odbc/reference/syntax/installation-and-configuration-wwi-oltp.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di un driver ODBCDeveloping an ODBC Driver](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Sviluppo di riconoscimento del pool di connessione in un driver ODBCDeveloping Connection-Pool Awareness in an ODBC Driver](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)   
 [Pool di connessioni di Gestione driver](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)
