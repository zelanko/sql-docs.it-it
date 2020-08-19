---
description: Aggiornamento dei dati nei set di righe-risincronizzazione delle righe in SQL Server Native Client
title: Risincronizzazione di righe (provider OLE DB di Native Client)
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- synchronization [OLE DB]
- IRowsetResynch interface
- resynchronizing rows
- data updates [SQL Server], OLE DB
ms.assetid: d2d30505-a878-4aa9-b821-53d8118a45a5
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 65f077141e6e29e3f524f8ac183e5f624b187319
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88448341"
---
# <a name="updating-data-in-rowsets---resynchronizing-rows-in-sql-server-native-client"></a>Aggiornamento dei dati nei set di righe-risincronizzazione delle righe in SQL Server Native Client
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native Client supporta solo **IRowsetResynch** nei [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] set di righe supportati dal cursore. **IRowsetResynch** non è disponibile su richiesta. Il consumer deve richiedere l'interfaccia prima di aprire il set di righe.  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiornamento dei dati nei set di righe](../../relational-databases/native-client-ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
