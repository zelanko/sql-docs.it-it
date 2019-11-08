---
title: SQLSetEnvAttr | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLSetEnvAttr function
ms.assetid: d4114571-feca-4330-b2e4-7bfd1050b812
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8e1d8e6ea962f5cd8fe094fca195a2fa59a5701d
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/07/2019
ms.locfileid: "73785638"
---
# <a name="sqlsetenvattr"></a>SQLSetEnvAttr
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Il [riferimento per programmatori ODBC](https://go.microsoft.com/fwlink/?LinkId=45250) definisce il modo in cui i driver ODBC devono interpretare le specifiche dell'attributo **SQLSetEnvAttr** dalle applicazioni scritte in ODBC 2. *x* o ODBC 3. API *x* . Il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client è conforme a tali regole.  
  
 Uno degli attributi controllati da **SQLSetEnvAttr** è se deve essere usato il pool di connessioni. Se il pool di connessioni viene utilizzato con il driver ODBC di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] native client, è necessario impostare il parametro *DriverCompletion* su SQL_DRIVER_NOPROMPT quando ci si connette con [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) o **SQLConnect**.  
  
## <a name="see-also"></a>Vedere anche  
   [funzione SQLSetEnvAttr](https://go.microsoft.com/fwlink/?LinkId=59369)  
 [Dettagli di implementazione dell'API ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
