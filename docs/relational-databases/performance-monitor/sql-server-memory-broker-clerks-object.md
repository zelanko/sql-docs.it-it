---
title: Oggetto Memory Broker Clerks di SQL Server | Microsoft Docs
description: Informazioni sull'oggetto prestazione SQLServer:Memory Broker Clerks, che fornisce contatori per statistiche correlate ai clerk broker di memoria.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Memory Broker Clerks
ms.assetid: 47b9c236-66a3-4c42-97ee-da5555bdc046
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 6e3a569e65d02af75e4b0195ed0795e097b96838
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505645"
---
# <a name="sql-server-memory-broker-clerks-object"></a>SQL Server, oggetto Memory Broker Clerks
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
L'oggetto prestazione **SQLServer:Memory Broker Clerks** fornisce contatori per statistiche correlate ai clerk broker di memoria.

La tabella seguente descrive gli oggetti prestazioni **Memory Broker Clerks** di SQL Server.

|**Contatori dell'oggetto Memory Broker Clerks di SQL Server**|Descrizione|  
|-------------|-----------------|  
|**Vantaggio interno**|Valore interno di memoria per il numero di richieste di pagine, in ms per pagina per ms, moltiplicato per 10 miliardi e troncato a un intero.|
|**Dimensioni clerk broker di memoria**|Dimensioni in pagine del clerk.|
|**Eliminazioni periodiche (pagine)**|Numero di pagine eliminate dal clerk broker durante l'ultima eliminazione periodica.|
|**Eliminazioni richieste di pagine (pagine/sec)**|Numero di pagine al secondo eliminate dal clerk broker dal numero di richieste di memoria.|
|**Vantaggio simulazione**|Valore di memoria per il clerk, in ms per pagina per ms, moltiplicato per 10 miliardi e troncato a un intero.|
|**Dimensioni simulazione**|Dimensioni correnti in pagine della simulazione del clerk.|

C'è un'istanza del contatore per il pool di buffer e il pool di oggetti dell'archivio colonne.

## <a name="see-also"></a>Vedere anche  
[Monitoraggio dell'utilizzo delle risorse (Monitor di sistema)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)
