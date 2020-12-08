---
title: Oggetto Catalog Metadata di SQL Server | Microsoft Docs
description: Informazioni sull'oggetto prestazione SQLServer:Catalog Metadata, che fornisce contatori per i metadati del catalogo per SQL Server.
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
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: a02c8d6253df487ebf5c01c8658f448ec680022c
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505815"
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
