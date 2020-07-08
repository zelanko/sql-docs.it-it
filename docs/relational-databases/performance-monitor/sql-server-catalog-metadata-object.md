---
title: Oggetto Catalog Metadata di SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Catalog Metadata
ms.assetid: 665e63e6-4bd2-4091-92a5-327364db2f8d
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: 5c8b74e6647422231f0ace765f57579bb3ea2b84
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85656179"
---
# <a name="sql-server-catalog-metadata-object"></a>SQL Server, oggetto Catalog Metadata
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
L'oggetto prestazione **SQLServer:Catalog Metadata** fornisce contatori per i metadati del catalogo per SQL Server.

La tabella seguente descrive gli oggetti prestazioni **Catalog Metadata** di SQL Server.


|**Contatori dell'oggetto Catalog Metadata di SQL Server**|Descrizione|  
|-------------|-----------------|  
|**Conteggio voci cache**|Numero di voci nella cache dei metadati del catalogo.|
|**Conteggio voci cache bloccate**|Numero di voci bloccate nella cache dei metadati del catalogo.|
|**Percentuale riscontri cache**|Rapporto tra riscontri e ricerche nella cache dei metadati del catalogo.|
|**Base percentuale riscontri cache**|Solo per uso interno.|

C'è un'istanza del contatore per ogni database.

## <a name="see-also"></a>Vedere anche  
[Monitoraggio dell'utilizzo delle risorse (Monitor di sistema)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)
