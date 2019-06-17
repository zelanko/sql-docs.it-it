---
title: L'aggiornamento dei dati nei set di righe | Microsoft Docs
description: L'aggiornamento dei dati nei set di righe usando il Driver OLE DB per SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- updating data [SQL Server]
- rowsets [OLE DB], updating data
- OLE DB Driver for SQL Server, rowsets
- OLE DB rowsets, updating data
- OLE DB Driver for SQL Server, data updates
- data updates [SQL Server], OLE DB
author: pmasl
ms.author: pelopes
manager: jroth
ms.openlocfilehash: 3e6a03d5bc379b620db06e0f1308058d647397e1
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 06/07/2019
ms.locfileid: "66803778"
---
# <a name="updating-data-in-rowsets"></a>Aggiornamento dei dati dei set di righe
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Il driver OLE DB per SQL Server aggiorna i dati di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] quando un consumer aggiorna un set di righe modificabile che li contiene. Un set di righe modificabile viene creato quando il consumer richiede il supporto per l'interfaccia **IRowsetChange** o **IRowsetUpdate**.  
  
 Tutti i Driver OLE DB per l'uso di set di righe modificabile con SQL Server [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cursori per supportare il set di righe. La proprietà del set di righe DBPROP_LOCKMODE modifica il comportamento di controllo della concorrenza di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nei cursori e determina il comportamento di recupero delle righe del set di righe e di generazione degli errori di integrità dei dati nei set di righe aggiornabili.  
  
 Il Driver OLE DB per SQL Server supporta la sincronizzazione di riga prima o dopo un aggiornamento.  
  
> [!NOTE]  
>  IRowChange::SetColumns è disponibile per l'impostazione dei valori di una o più colonne denominate di un oggetto riga.  
  
## <a name="in-this-section"></a>Contenuto della sezione  
  
-   [Aggiornamento dei dati nei cursori SQL Server](../../oledb/ole-db-rowsets/updating-data-in-sql-server-cursors.md)  
  
-   [Risincronizzazione delle righe](../../oledb/ole-db-rowsets/updating-data-in-rowsets-resynchronizing-rows.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Set di righe](../../oledb/ole-db-rowsets/rowsets.md)  
  
  
