---
title: Risincronizzazione di righe | Microsoft Docs
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
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: fd994f7ec89f154f106df25190819b227495f290
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "73788728"
---
# <a name="updating-data-in-rowsets---resynchronizing-rows"></a>Aggiornamento dei dati nei set di righe - Risincronizzazione delle righe
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Il [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provider di OLE DB di Native **** client supporta [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo IRowsetResynch nei set di righe supportati dal cursore. **IRowsetResynch** non è disponibile su richiesta. Il consumer deve richiedere l'interfaccia prima di aprire il set di righe.  
  
## <a name="see-also"></a>Vedere anche  
 [Aggiornamento dei dati nei set di righe](../../relational-databases/native-client-ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
