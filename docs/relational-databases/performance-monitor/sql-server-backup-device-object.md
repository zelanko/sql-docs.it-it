---
title: Oggetto Backup Device di SQL Server | Microsoft Docs
description: Informazioni sull'oggetto Backup Device, che include contatori per il monitoraggio dei dispositivi di backup di Microsoft SQL Server usati per le operazioni di backup e ripristino.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:Backup Device
- Backup Device object
ms.assetid: 52e7febf-d5e0-4674-945b-aacc40a9ad6e
author: WilliamDAssafMSFT
ms.author: wiassaf
ms.openlocfilehash: 383e1cd4ccca7a466817ac5ca226785fa56560ce
ms.sourcegitcommit: 0e0cd9347c029e0c7c9f3fe6d39985a6d3af967d
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/02/2020
ms.locfileid: "96505902"
---
# <a name="sql-server-backup-device-object"></a>Oggetto Backup Device di SQL Server
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  L'oggetto **Backup Device** include contatori per il monitoraggio dei dispositivi di backup di Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usati per le operazioni di backup e ripristino. Monitorare i dispositivi di backup se si desidera determinare la velocità effettiva oppure lo stato di avanzamento e le prestazioni delle operazioni di backup e ripristino per ogni dispositivo. Per monitorare la velocità effettiva di un'operazione di backup o ripristino dell'intero database, usare il contatore **Velocità effettiva backup o ripristino/sec** dell'oggetto **Databases** di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Per altre informazioni, vedere [SQL Server, Databases Object](../../relational-databases/performance-monitor/sql-server-databases-object.md).  
  
 Nella tabella seguente viene descritto il contatore **Backup Device** di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Contatore dell'oggetto Backup Device di SQL Server|Descrizione|  
|---------------------------------------|-----------------|  
|**Byte/sec velocità effettiva dispositivo**|Velocità effettiva delle operazioni di lettura e scrittura (in byte al secondo) di un dispositivo di backup utilizzato durante il backup o il ripristino dei database. Il contatore è disponibile solo durante l'esecuzione dell'operazione di backup o ripristino.|  
  
## <a name="see-also"></a>Vedere anche  
 [Dispositivi di backup &#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)   
 [Monitorare l'utilizzo delle risorse &#40;Monitor di sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
