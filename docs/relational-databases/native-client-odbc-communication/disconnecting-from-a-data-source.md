---
description: Disconnessione da un'origine dati
title: Disconnessione da un'origine dati | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC data sources, connections
- data sources [SQL Server Native Client]
- disconnecting [ODBC]
- ODBC applications, disconnecting
- SQLDisconnect function
- ODBC applications, data sources
- connections [SQL Server Native Client]
- SQLFreeHandle function
- ODBC data sources, disconnecting
- SQL Server Native Client ODBC driver, data sources
- ODBC functions
- SQL Server Native Client ODBC driver, connections
ms.assetid: 65b0267d-b2ab-4a59-83f2-436d90cfbf79
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fd4277c773c07e56a8669d1bb5c6f9d8e024d769
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97464972"
---
# <a name="disconnecting-from-a-data-source"></a>Disconnessione da un'origine dati
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Quando un'applicazione ha terminato di usare un'origine dati, chiama **SQLConnect**. **SQLConnect** libera tutte le istruzioni allocate sulla connessione e disconnette il driver dall'origine dati. Dopo la disconnessione, l'applicazione può chiamare [SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) per liberare l'handle di connessione. Prima di uscire, un'applicazione chiama anche **SQLFreeHandle** per liberare l'handle di ambiente.  
  
 Dopo la disconnessione, un'applicazione può riutilizzare l'handle di connessione allocato per connettersi a un'origine dati diversa oppure per riconnettersi alla stessa origine dati. La decisione di rimanere connessi anziché disconnettersi e riconnettersi in un secondo momento richiede la valutazione da parte del writer dell'applicazione dei costi relativi di ogni opzione. Connettersi e rimanere connessi a un'origine dati può essere relativamente costoso, a seconda del supporto di connessione utilizzato. Nella valutazione vanno considerati anche la probabilità di dover eseguire operazioni aggiuntive sulla stessa origine dati e il tempo richiesto. È inoltre possibile che un'applicazione debba utilizzare più di una connessione.  
  
## <a name="see-also"></a>Vedere anche  
 [Comunicazione con SQL Server &#40;ODBC&#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
