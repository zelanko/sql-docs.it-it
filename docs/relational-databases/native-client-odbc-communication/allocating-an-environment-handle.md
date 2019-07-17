---
title: Allocare un Handle di ambiente | Microsoft Docs
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 35c58f136668893bb6dd865859f42b2bcaefe128
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68134221"
---
# <a name="allocating-an-environment-handle"></a>Allocazione di un handle di ambiente
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Prima di poter chiamare una funzione ODBC, un'applicazione deve inizializzare l'ambiente ODBC e allocare un handle di ambiente. Si tratta dell'handle dell'ambito globale che funge da segnaposto per gli altri handle in ODBC. Eseguire questa operazione chiamando **SQLAllocHandle** con il *HandleType* parametro impostato su SQL_HANDLE_ENV e *InputHandle* impostato su SQL_NULL_HANDLE.  
  
 Dopo avere allocato l'handle di ambiente, l'applicazione deve impostare gli attributi di ambiente per indicare la versione delle chiamate alle funzioni ODBC che verrà utilizzata. Per usare ODBC 3. *x* funzioni, chiamate [SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md) con il *attributo* parametro impostato su SQL_ATTR_ODBC_VERSION e *ValuePtr* impostato su SQL_OV_ ODBC3.  
  
## <a name="see-also"></a>Vedere anche  
 [Comunicazione con SQL Server &#40;ODBC&#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
