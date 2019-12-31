---
title: Backup & caricamento hardware
description: Per distribuire una soluzione di data warehousing end-to-end in un sistema di piattaforma di analisi (APS) con data warehouse paralleli (PDW), è necessario creare un piano per il backup del data warehouse e il caricamento dei dati. Usare queste linee guida per acquisire e configurare i server di backup e di caricamento che soddisferanno i requisiti aziendali.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 4dd4fba91b1507f711a66a88f40b2fa2ea35e1ae
ms.sourcegitcommit: d587a141351e59782c31229bccaa0bff2e869580
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 11/22/2019
ms.locfileid: "74401366"
---
# <a name="backup-and-loading-hardware-overview---parallel-data-warehouse"></a>Panoramica dell'hardware di backup e caricamento-data warehouse parallele
Per distribuire una soluzione di data warehousing end-to-end in un sistema di piattaforma di analisi (APS) con data warehouse paralleli (PDW), è necessario creare un piano per il backup del data warehouse e il caricamento dei dati. Usare queste linee guida per acquisire e configurare i server di backup e di caricamento che soddisferanno i requisiti aziendali.  
  
## <a name="acquire-and-configure-backup-servers"></a>Acquisire e configurare i server di backup  
![Processo di backup](media/backup-process.png "Processo di backup")  
  
Per eseguire il backup di un database PDW, sono necessari uno o più server di backup. È possibile utilizzare l'hardware esistente o acquistare nuovo hardware. Per altre informazioni, vedere [acquisire e configurare un server di backup](acquire-and-configure-backup-server.md). Queste istruzioni includono un [foglio](backup-capacity-planning-worksheet.md) di disegno per la pianificazione della capacità del server di backup che consente di pianificare la soluzione corretta per il backup.  
  
## <a name="acquire-and-configure-loading-servers"></a>Acquisire e configurare i server di caricamento  
![Processo di caricamento](media/loading-process.png "Processo di caricamento")  
  
Per caricare i dati, sono necessari uno o più server di caricamento. È possibile utilizzare il proprio ETL o altri server esistenti oppure è possibile acquistare nuovi server. Per altre informazioni, vedere [acquisire e configurare un server di caricamento](acquire-and-configure-loading-server.md). Queste istruzioni includono un [foglio](loading-server-capacity-planning-worksheet.md) di disegno per la pianificazione della capacità del server per facilitare la pianificazione della soluzione corretta per il caricamento.  
  
## <a name="see-also"></a>Vedere anche  
[Panoramica di backup e ripristino](backup-and-restore-overview.md)  
[Panoramica sul carico](load-overview.md)  
  
