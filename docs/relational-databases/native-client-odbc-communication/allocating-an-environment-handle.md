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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: eae9e11006a8a832523a7f72bdade6e943e57f50
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73784741"
---
# <a name="allocating-an-environment-handle"></a>Allocazione di un handle di ambiente
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Prima di poter chiamare una funzione ODBC, un'applicazione deve inizializzare l'ambiente ODBC e allocare un handle di ambiente. Si tratta dell'handle dell'ambito globale che funge da segnaposto per gli altri handle in ODBC. A tale scopo, chiamare **SQLAllocHandle** con il parametro *HandleType* impostato su SQL_HANDLE_ENV e *InputHandle puntare* impostato su SQL_NULL_HANDLE.  
  
 Dopo avere allocato l'handle di ambiente, l'applicazione deve impostare gli attributi di ambiente per indicare la versione delle chiamate alle funzioni ODBC che verrà utilizzata. Per utilizzare ODBC 3. funzioni *x* , chiamare [SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md) con il parametro *attribute* impostato su SQL_ATTR_ODBC_VERSION e *ValuePtr* impostato su SQL_OV_ODBC3.  
  
## <a name="see-also"></a>Vedere anche  
 [Comunicazione con SQL Server &#40;ODBC&#41;](../../relational-databases/native-client-odbc-communication/communicating-with-sql-server-odbc.md)  
  
  
