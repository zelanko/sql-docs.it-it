---
title: Stato dei servizi PDW
description: Stato dei servizi di Parallel data warehouse (PDW) per il sistema di piattaforma di analisi.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 2789c8b74420a56a32d08a0339d4ee6d3cc112d1
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400849"
---
# <a name="parallel-data-warehouse-services-status-for-analytics-platform-system"></a>Stato dei servizi di data warehouse paralleli per il sistema della piattaforma Analytics
La pagina stato Parallel data warehouse **Services** nel piattaforma di strumenti analitici Microsoft Configuration Manager Mostra lo stato corrente di tutti i servizi SQL Server PDW e consente di arrestare e avviare i servizi PDW. Questo è l'unico metodo supportato per l'avvio e l'arresto dei servizi PDW. Si noti che i singoli componenti o servizi non possono essere avviati in modo indipendente.  
  
#### <a name="to-start-or-stop-the-appliance-services"></a>Per avviare o arrestare i servizi Appliance  
  
1.  Per avviare i servizi Appliance, fare clic su **Avvia Appliance**.  
  
2.  Per arrestare i servizi Appliance, fare clic su **Interrompi Appliance**.  
  
Non è necessario fare clic su **applica** quando si avviano e si arrestano i servizi Appliance usando **Avvia Appliance** e **Arresta Appliance**.  
  
![Servizi PDW strumento DWConfig](./media/pdw-services-status/SQL_Server_PDW_DWConfig_ApplPDWServices.png "SQL_Server_PDW_DWConfig_ApplPDWServices")  
  
> [!NOTE]  
> L'arresto dell'area PDW interrompe anche l'agente PDW (sqldwagent) nei nodi. L'agente PDW richiede il nodo di controllo PDW per segnalare il monitoraggio dell'integrità.  
  
## <a name="see-also"></a>Vedere anche  
[Accendere o disabilitare l'appliance APS &#40;sistema della piattaforma di analisi&#41;](power-the-aps-appliance-on-or-off.md)  
  
