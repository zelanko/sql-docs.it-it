---
title: -Stato di servizi PDW sistema di piattaforma Analitica | Microsoft Docs
description: Parallel Data Warehouse (PDW) dello stato dei servizi di sistema di piattaforma Analitica.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 6892bfcca05e0f85039dddee65a54b485a7ed433
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/23/2019
ms.locfileid: "63027555"
---
# <a name="parallel-data-warehouse-services-status-for-analytics-platform-system"></a>Parallel Data Warehouse lo stato dei servizi per il sistema di piattaforma Analitica
Parallel Data Warehouse **stato dei servizi** pagina in Gestione configurazione di Microsoft Analitica Platform System Mostra lo stato corrente di tutti i servizi di SQL Server PDW e offre la possibilità di arrestare e avviare i servizi PDW. Questo è l'unico metodo supportato per l'avvio e arresto dei servizi PDW. Si noti che i singoli componenti o servizi non possono essere avviati in modo indipendente.  
  
#### <a name="to-start-or-stop-the-appliance-services"></a>Per avviare o arrestare i servizi di appliance  
  
1.  Per avviare i servizi di appliance, fare clic su **Appliance avviare**.  
  
2.  Per arrestare i servizi di appliance, fare clic su **arrestare Appliance**.  
  
Non è necessario fare clic su **Apply** durante l'avvio e arresto dei servizi appliance usando **avviare Appliance** e **arrestare Appliance**.  
  
![DWConfig Appliance PDW Services](./media/pdw-services-status/SQL_Server_PDW_DWConfig_ApplPDWServices.png "SQL_Server_PDW_DWConfig_ApplPDWServices")  
  
> [!NOTE]  
> L'arresto dell'area PDW interrompe anche l'agente PDW (sqldwagent) nei nodi. L'agente PDW richiede il nodo di controllo PDW per segnalare il monitoraggio dell'integrità.  
  
## <a name="see-also"></a>Vedere anche  
[Accendere l'Appliance APS o spegnere &#40;sistema di piattaforma Analitica&#41;](power-the-aps-appliance-on-or-off.md)  
  
