---
title: Riferimento di interfaccia (SPI) ODBC del servizio Provider | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cdeffb4a-f344-4abe-97f3-be2ede1c8e59
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 88053620fa413c50a8faff4cc47cbbe1457249f2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68073828"
---
# <a name="odbc-service-provider-interface-spi-reference"></a>Informazioni di riferimento sull'interfaccia del provider di servizi (SPI) ODBC
In genere, ODBC definita un'interfaccia di programmazione dell'applicazione (API). Le funzioni dell'API possono essere chiamate dalle applicazioni e che devono essere implementate all'interno di gestione Driver sia il driver.  
  
 Con l'aggiunta della funzionalità del pool di connessioni compatibile con il driver, ODBC viene presentata l'interfaccia di provider di servizi (SPI). Le funzioni di SPI vengono utilizzate per la comunicazione tra il gestore dei Driver e il driver. Funzioni SPI vengono implementate dal driver; Gestione Driver non espone le funzioni SPI alle applicazioni. Le applicazioni non devono chiamare direttamente queste funzioni.  
  
 Includere sqlspi.h per lo sviluppo di driver ODBC.  
  
 In questa sezione contiene gli argomenti seguenti  
  
-   [SQLCleanupConnectionPoolID](../../../odbc/reference/syntax/sqlcleanupconnectionpoolid-function.md)  
  
-   [SQLGetPoolID](../../../odbc/reference/syntax/sqlgetpoolid-function.md)  
  
-   [SQLPoolConnect](../../../odbc/reference/syntax/sqlpoolconnect-function.md)  
  
-   [SQLRateConnection](../../../odbc/reference/syntax/sqlrateconnection-function.md)  
  
-   [SQLSetConnectAttrForDbcInfo](../../../odbc/reference/syntax/sqlsetconnectattrfordbcinfo-function.md)  
  
-   [SQLSetConnectInfo](../../../odbc/reference/syntax/sqlsetconnectinfo-function.md)  
  
-   [SQLSetDriverConnectInfo](../../../odbc/reference/syntax/installation-and-configuration-wwi-oltp.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Sviluppo di un Driver ODBC](../../../odbc/reference/develop-driver/developing-an-odbc-driver.md)   
 [Sviluppo di riconoscimento dei Pool di connessioni in un Driver ODBC](../../../odbc/reference/develop-driver/developing-connection-pool-awareness-in-an-odbc-driver.md)   
 [Pool di connessioni di Gestione driver](../../../odbc/reference/develop-app/driver-manager-connection-pooling.md)
