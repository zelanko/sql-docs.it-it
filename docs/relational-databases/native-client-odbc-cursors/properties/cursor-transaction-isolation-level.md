---
title: Livello di isolamento delle transazioni di cursore | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- isolation levels [ODBC]
- ODBC applications, row versioning
- cursors [ODBC], isolation levels
- ODBC cursors, isolation levels
- row versioning [SQL Server], ODBC
ms.assetid: 0c6663a4-5a25-44aa-8fe4-e35af9bf4a83
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5ae4ffc9b3a9c0d8122fb46ae9db215bf1560396
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68078837"
---
# <a name="cursor-transaction-isolation-level"></a>Livello di isolamento delle transazioni di cursore
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Il comportamento di blocco completo dei cursori si basa su un'interazione fra gli attributi di concorrenza e il livello di isolamento delle transazioni impostati dal client. Impostare i client ODBC transazione utilizzando il [SQLSetConnectAttr](../../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) attributi SQL_ATTR_TXN_ISOLATION o SQL_COPT_SS_TXN_ISOLATION. Il comportamento di blocco di un ambiente di cursore specifico è determinato dalla combinazione dei comportamenti di blocco della concorrenza con le opzioni del livello di isolamento delle transazioni.  
  
 I livelli di isolamento delle transazioni di cursore seguenti sono supportati per il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client:  
  
-   Read committed (SQL_TXN_READ_COMMITTED)  
  
-   Read uncommitted (SQL_TXN_READ_UNCOMMITTED)  
  
-   Repeatable read (SQL_TXN_REPEATABLE_READ)  
  
-   Serializable (SQL_TXN_SERIALIZABLE)  
  
-   Snapshot (SQL_TXN_SS_SNAPSHOT)  
  
 Si noti che l'API ODBC specifica i livelli di isolamento delle transazioni aggiuntivi, ma non sono supportati dal [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o il [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] driver ODBC Native Client.  
  
## <a name="see-also"></a>Vedere anche  
 [Proprietà del cursore](../../../relational-databases/native-client-odbc-cursors/properties/cursor-properties.md)  
  
  
