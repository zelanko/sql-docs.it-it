---
title: Possibilità di confronto per IRowsetFind | Microsoft Docs
description: Informazioni sui confronti supportati da IRowsetFind per i tipi di date e time in OLE DB Driver per SQL Server. Per gli altri confronti viene restituito DB_E_BADCOMPAREOP.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- IRowsetFind comparability
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 16ef589a18c2be5317157e7db5790af06c8c613a
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/25/2020
ms.locfileid: "88861401"
---
# <a name="comparability-for-irowsetfind"></a>Possibilità di confronto per IRowsetFind
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Solo per i tipi data/ora, IRowsetFind supporta i confronti seguenti:  
  
-   LT  
  
-   LE  
  
-   EQ  
  
-   GE  
  
-   GT  
  
-   NE  
  
-   IGNORE  
  
 Se viene tentato qualsiasi altro confronto, viene restituito DB_E_BADCOMPAREOP, in conformità con la specifica OLE DB.  
  
## <a name="see-also"></a>Vedere anche  
 [Miglioramenti relativi a data e ora &#40;OLE DB&#41;](../../oledb/ole-db-date-time/date-and-time-improvements-ole-db.md)  
  
  
