---
title: Allocazione di un handle di ambiente | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, environment handles
- ODBC applications, connections
- handles [SQL Server Native Client]
- environment handles [SQLNCLI]
ms.assetid: 15c1b428-ea6d-4672-894c-f0e289e2da3f
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d36f0f2c1f2b98ef70f3a7460c5565307cc0a3d7
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: it-IT
ms.lasthandoff: 07/06/2020
ms.locfileid: "86007133"
---
# <a name="allocating-an-environment-handle"></a>Allocazione di un handle di ambiente
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Prima di poter chiamare una funzione ODBC, un'applicazione deve inizializzare l'ambiente ODBC e allocare un handle di ambiente. Si tratta dell'handle dell'ambito globale che funge da segnaposto per gli altri handle in ODBC. A tale scopo, chiamare **SQLAllocHandle** con il parametro *HandleType* impostato su SQL_HANDLE_ENV e *InputHandle puntare* impostato su SQL_NULL_HANDLE.  
  
 Dopo avere allocato l'handle di ambiente, l'applicazione deve impostare gli attributi di ambiente per indicare la versione delle chiamate alle funzioni ODBC che verrà utilizzata. Per utilizzare ODBC 3. funzioni *x* , chiamare [SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md) con il parametro *attribute* impostato su SQL_ATTR_ODBC_VERSION e *ValuePtr* impostato su SQL_OV_ODBC3.  
  
## <a name="see-also"></a>Vedere anche  
 [Comunicazione con SQL Server &#40;ODBC&#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
