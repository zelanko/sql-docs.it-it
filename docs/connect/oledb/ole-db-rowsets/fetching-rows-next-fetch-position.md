---
title: Posizione recupero successiva | Microsoft Docs
description: Recupero di righe - Posizione del recupero successivo
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- fetching rows
- OLE DB rowsets, fetching
- next fetch position
- rowsets [OLE DB], fetching
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 2ea743770323505c611210c0bb3acd0e93c719cd
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67994195"
---
# <a name="fetching-rows---next-fetch-position"></a>Recupero di righe - Posizione del recupero successivo
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Il driver OLE DB per SQL Server tiene traccia della posizione del recupero successivo in modo che una sequenza di chiamate al metodo **GetNextRows** (senza elementi ignorati, cambiamenti di direzione o nuove chiamate ai metodi **FindNextRow**, **Seek** o **RestartPosition**) legga l'intero set di righe senza ignorare o ripetere alcuna riga. La posizione del recupero successiva viene modificata chiamando **IRowset::GetNextRows**, **IRowset::RestartPosition** o **IRowsetIndex::Seek** oppure chiamando **FindNextRow** con un valore *pBookmark* Null. La chiamata a **FindNextRow** con un valore *pBookmark* non Null non influisce sulla posizione del recupero successivo.  
  
## <a name="see-also"></a>Vedere anche  
 [Recupero di righe](../../oledb/ole-db-rowsets/fetching-rows.md)  
  
  
