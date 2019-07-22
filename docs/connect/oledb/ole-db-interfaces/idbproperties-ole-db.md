---
title: IDBProperties (OLE DB) | Microsoft Docs
description: Interfaccia IDBProperties (OLE DB)
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
author: pmasl
ms.author: pelopes
ms.openlocfilehash: d8515ef92ce1284379327e63a4bd1730577bd8df
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67994482"
---
# <a name="idbproperties-ole-db"></a>IDBProperties (OLE DB)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  La specifica dello standard OLE DB consente ai provider di specificare VT_EMPTY per **DBPROPINFO::vValues**. Tuttavia, il driver OLE DB per SQL Server restituisce sempre VT_EMPTY quando si chiama **IDBProperties::GetPropertyInfo** con **DBPROPSET_ROWSETALL** per recuperare le proprietà dei set di righe.  
  
## <a name="see-also"></a>Vedere anche  
 [Interfacce &#40;OLE DB&#41;](../../oledb/ole-db-interfaces/oledb-driver-for-sql-server-ole-db-interfaces.md) 
  
  
