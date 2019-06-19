---
title: Disconnessione da un'origine dei dati | Documenti di Microsoft
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
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4a909fcf550a26542612b6cd8fab4dc003bcdbec
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63013853"
---
# <a name="disconnecting-from-a-data-source"></a>Disconnessione da un'origine dati
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Quando un'applicazione ha terminato di utilizzare un'origine dati, viene chiamato **SQLDisconnect**. **SQLDisconnect** libera le istruzioni allocate nella connessione e disconnette il driver dell'origine dati. Dopo la disconnessione, l'applicazione può chiamare [SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) per liberare l'handle di connessione. Prima di uscire, un'applicazione chiama inoltre **SQLFreeHandle** per liberare l'handle di ambiente.  
  
 Dopo la disconnessione, un'applicazione può riutilizzare l'handle di connessione allocato per connettersi a un'origine dati diversa oppure per riconnettersi alla stessa origine dati. La decisione di rimanere connessi anziché disconnettersi e riconnettersi in un secondo momento richiede la valutazione da parte del writer dell'applicazione dei costi relativi di ogni opzione. Connettersi e rimanere connessi a un'origine dati può essere relativamente costoso, a seconda del supporto di connessione utilizzato. Nella valutazione vanno considerati anche la probabilità di dover eseguire operazioni aggiuntive sulla stessa origine dati e il tempo richiesto. È inoltre possibile che un'applicazione debba utilizzare più di una connessione.  
  
## <a name="see-also"></a>Vedere anche  
 [Comunicazione con SQL Server &#40;ODBC&#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
