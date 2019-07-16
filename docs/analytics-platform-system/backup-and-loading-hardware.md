---
title: Backup e il caricamento di hardware - Parallel Data Warehouse
description: Per distribuire i end-to-end soluzione di data warehousing su Analitica piattaforma di strumenti analitici con Parallel Data Warehouse (PDW), è necessario creare un piano di backup nel data warehouse e il caricamento dei dati. Usare queste linee guida per acquisire e configurare i server di backup e il caricamento in grado di soddisfare i requisiti aziendali.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 90f142a8bb86f99ed5cf5d9ff926bdf849060324
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961411"
---
# <a name="backup-and-loading-hardware-overview---parallel-data-warehouse"></a>Backup e il caricamento Cenni preliminari sull'hardware - Parallel Data Warehouse
Per distribuire i end-to-end soluzione di data warehousing su Analitica piattaforma di strumenti analitici con Parallel Data Warehouse (PDW), è necessario creare un piano di backup nel data warehouse e il caricamento dei dati. Usare queste linee guida per acquisire e configurare i server di backup e il caricamento in grado di soddisfare i requisiti aziendali.  
  
## <a name="acquire-and-configure-backup-servers"></a>Acquisire e configurare i server di backup  
![Processo di backup](media/backup-process.png "processo di Backup")  
  
Per eseguire il backup di un database PDW, sono necessari uno o più server di backup. È possibile usare il proprio hardware esistente o acquistare nuovo hardware. Per altre informazioni, vedere [acquisire e configurare un Server di Backup](acquire-and-configure-backup-server.md). Queste istruzioni includono una [Backup server capacità pianificazione foglio di lavoro](backup-capacity-planning-worksheet.md) per pianificare la soluzione ideale per il backup.  
  
## <a name="acquire-and-configure-loading-servers"></a>Acquisire e configurare il caricamento dei server  
![Processo di caricamento](media/loading-process.png "processo di caricamento")  
  
Per caricare i dati, è necessario uno o più server di caricamento. È possibile usare il proprio ETL esistenti o ad altri server o è possibile acquistare nuovi server. Per altre informazioni, vedere [Acquire e configurare un server di caricamento](acquire-and-configure-loading-server.md). Queste istruzioni includono una [caricamento di foglio di lavoro di pianificazione della capacità server](loading-server-capacity-planning-worksheet.md) per pianificare la soluzione ideale per il caricamento.  
  
## <a name="see-also"></a>Vedere anche  
[Panoramica su backup e ripristino](backup-and-restore-overview.md)  
[Panoramica di carico](load-overview.md)  
  
