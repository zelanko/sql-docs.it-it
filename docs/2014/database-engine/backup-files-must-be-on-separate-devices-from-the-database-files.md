---
title: I file di backup devono trovarsi in dispositivi separati dai file di database | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- Best Practices [Database Engine]
ms.assetid: 7039bebb-1f25-4cf3-81f1-393dfb78da12
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: d5eff9cb3139e1e1043f99ba63d11160b1010c27
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/17/2020
ms.locfileid: "84936146"
---
# <a name="backup-files-must-be-on-separate-devices-from-the-database-files"></a>Posizionamento dei file di backup in dispositivi separati rispetto ai file di database
  Questa regola consente di controllare se i file di database si trovano in dispositivi separati rispetto ai file di backup. Se file di database e i file di backup sono archiviati nello stesso dispositivo e si verifica un errore nel dispositivo, il database e i backup non saranno disponibili. L'archiviazione dei file di database e di backup in dispositivi distinti, inoltre, consente di ottimizzare le prestazioni di I/O per l'utilizzo del database in un ambiente di produzione e per la scrittura dei backup.  
  
## <a name="best-practices-recommendations"></a>Procedure consigliate  
 È consigliabile archiviare il database e i backup in dispositivi di backup distinti.  
  
> [!NOTE]  
>  Questi criteri non sono in grado di rilevare dispositivi fisici separati mediante punti di montaggio.  
  
## <a name="for-more-information"></a>Ulteriori informazioni  
 [Dispositivi di backup &#40;SQL Server&#41;](../relational-databases/backup-restore/backup-devices-sql-server.md)  
  
 [Backup e ripristino di database SQL Server](../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)  
  
## <a name="see-also"></a>Vedere anche  
 [Monitorare e applicare le procedure consigliate tramite la gestione basata su criteri](../relational-databases/policy-based-management/monitor-and-enforce-best-practices-by-using-policy-based-management.md)  
  
  
