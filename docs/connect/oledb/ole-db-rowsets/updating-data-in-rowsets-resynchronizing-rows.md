---
title: Risincronizzazione delle righe (OLE DB Driver)
description: Per l'aggiornamento dei dati nei set di righe, OLE DB Driver per SQL Server supporta IRowsetResynch solo nei set di righe supportati dal cursore di SQL Server.
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- synchronization [OLE DB]
- IRowsetResynch interface
- resynchronizing rows
- data updates [SQL Server], OLE DB
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 65ae67a91fc7fb5f3caaa341dbfcb00dc2e5d796
ms.sourcegitcommit: c95f3ef5734dec753de09e07752a5d15884125e2
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/25/2020
ms.locfileid: "88859969"
---
# <a name="updating-data-in-rowsets---resynchronizing-rows"></a>Aggiornamento dei dati nei set di righe - Risincronizzazione delle righe
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  OLE DB Driver per SQL Server supporta **IRowsetResynch** solo nei set di righe supportati dal cursore di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. **IRowsetResynch** non è disponibile su richiesta. Il consumer deve richiedere l'interfaccia prima di aprire il set di righe.  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiornamento dei dati nei set di righe](../../oledb/ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
