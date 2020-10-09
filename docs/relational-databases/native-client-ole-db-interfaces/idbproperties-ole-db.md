---
description: IDBProperties (provider OLE DB Native Client)
title: IDBProperties (provider OLE DB Native Client) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 2e5a4fd8-5164-495a-9986-3477aef8d8a5
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: d8b1e72d69d047f2fee77db933f9acb447724035
ms.sourcegitcommit: 4d370399f6f142e25075b3714e5c2ce056b1bfd0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/09/2020
ms.locfileid: "91866749"
---
# <a name="idbproperties-native-client-ole-db-provider"></a>IDBProperties (provider OLE DB Native Client)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  La specifica dello standard OLE DB consente ai provider di specificare VT_EMPTY per **DBPROPINFO::vValues**. Tuttavia, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client OLE DB restituisce sempre VT_EMPTY quando si chiama **IDBProperties::GetPropertyInfo** con **DBPROPSET_ROWSETALL** per recuperare le proprietà dei set di righe.  
  
## <a name="see-also"></a>Vedere anche  
 [Interfacce &#40;OLE DB&#41;](./sql-server-native-client-ole-db-interfaces.md)  
  
