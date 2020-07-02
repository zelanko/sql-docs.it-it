---
title: Comunicazione con SQL Server (ODBC) | Microsoft Docs
description: Informazioni sul modo in cui un'applicazione ODBC comunica con un'istanza di SQL Server usando le connessioni e le risorse di connessione.
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, communicating with SQL Server
- ODBC applications, communicating with SQL Server
- ODBC, communicating with SQL Server
ms.assetid: cca3dcf0-2a7e-465a-84de-7ce055360eb6
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b6f149f8d1d714839d356d3675a19656f2ea7d53
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85734897"
---
# <a name="communicating-with-sql-server-odbc"></a>Comunicazione con SQL Server (ODBC)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  Affinché un'applicazione ODBC comunichi con un'istanza di [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , deve allocare gli handle di ambiente e di connessione e connettersi all'origine dati. Una volta stabilita una connessione, l'applicazione può inviare query al server ed elaborare qualsiasi set di risultati. Quando l'applicazione ha completato l'utilizzo dell'origine dati, si disconnette dall'origine dati e rilascia l'handle di connessione. Quando l'applicazione ha rilasciato tutti gli handle di connessione, rilascia l'handle di ambiente.  
  
 Un'applicazione può connettersi a qualsiasi numero di origini dati. L'applicazione può utilizzare una combinazione di driver e origini dati, lo stesso driver e una combinazione di origini dati o persino lo stesso driver e più connessioni alla stessa origine dati.  
  
 È possibile scaricare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gli esempi ODBC di Native Client dalla pagina di [download SQL Server](https://go.microsoft.com/fwlink/?LinkId=62796) su MSDN.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Allocazione di un handle di ambiente](../../relational-databases/native-client-odbc-communication/allocating-an-environment-handle.md)  
  
-   [Allocazione di un handle di connessione](../../relational-databases/native-client-odbc-communication/allocating-a-connection-handle.md)  
  
-   [Origini dati ODBC di SQL Server Native Client](../../relational-databases/native-client-odbc-communication/sql-server-native-client-odbc-data-sources.md)  
  
-   [Connessione a un'origine dati &#40;ODBC&#41;](../../relational-databases/native-client-odbc-communication/connecting-to-a-data-source-odbc.md)  
  
-   [Disconnessione da un'origine dati](../../relational-databases/native-client-odbc-communication/disconnecting-from-a-data-source.md)  
  
## <a name="see-also"></a>Vedere anche  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)   
 [SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md)  
  
  
