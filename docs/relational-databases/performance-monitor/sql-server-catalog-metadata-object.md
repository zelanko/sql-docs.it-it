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
manager: craigg
ms.openlocfilehash: c7e3e4632141040f791b6b83640c5261017726c6
ms.sourcegitcommit: 0c1d552b3256e1bd995e3c49e0561589c52c21bf
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2018
ms.locfileid: "53380793"
---
# <a name="sql-server-catalog-metadata-object"></a>SQL Server, oggetto Catalog Metadata
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
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
