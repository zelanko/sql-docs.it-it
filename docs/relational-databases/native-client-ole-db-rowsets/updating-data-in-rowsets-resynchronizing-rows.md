---
title: Risincronizzazione delle righe | Microsoft Docs
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
ms.openlocfilehash: 44e31275a6eb3ab728d1a9d7280a3d77404f7248
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300257"
---
# <a name="updating-data-in-rowsets---resynchronizing-rows"></a>Aggiornamento dei dati nei set di righe - Risincronizzazione delle righe
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native **IRowsetResynch** client supporta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo IRowsetResynch nei set di righe supportati dal cursore. **IRowsetResynch** non è disponibile su richiesta. Il consumer deve richiedere l'interfaccia prima di aprire il set di righe.  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiornamento dei dati dei set di righe](../../relational-databases/native-client-ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
