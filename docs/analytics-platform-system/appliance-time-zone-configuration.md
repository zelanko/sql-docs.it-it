---
title: Configurare il fuso orario - sistema di piattaforma Analitica | Microsoft Docs
description: Pagina fuso orario consente di impostare il fuso orario per tutti i nodi per l'appliance del sistema di piattaforma Analitica (AP).
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 6a17ef4e77f9703a285f1e232077582e4441f293
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/15/2019
ms.locfileid: "63275989"
---
# <a name="appliance-time-zone-configuration---analytics-platform-system"></a>Configurazione del fuso orario Appliance - sistema di piattaforma Analitica
Il **fuso orario** pagina consente di impostare il fuso orario per tutti i nodi per l'appliance del sistema di piattaforma Analitica (AP).  
  
## <a name="to-set-the-time-zone"></a>Per impostare il fuso orario  
  
1.  Avviare Gestione configurazione. Per altre informazioni, vedere [avviare Gestione configurazione &#40;sistema di piattaforma Analitica&#41;](launch-the-configuration-manager.md).  
  
2.  Arrestare i servizi di appliance usando il **stato dei servizi** pagina in Gestione configurazione. Visualizzare [stato dei servizi PDW &#40;sistema di piattaforma Analitica&#41; ](pdw-services-status.md) per istruzioni.  
  
3.  Nel riquadro a sinistra di Configuration Manager, fare clic su **fuso orario**. Selezionare il fuso orario desiderato dal **fuso orario** dal menu a discesa. A seconda del punto di accesso, si può anche scegliere di selezionare la casella accanto a **automaticamente le regolazioni dell'orologio dell'ora legale**.  
  
4.  Fare clic su **applica** per salvare le modifiche.  
  
5.  Riavviare i servizi di appliance usando il **stato dei servizi** pagina in Gestione configurazione. Se si prevede anche di modificare i privilegi, è possibile farlo prima di riavviare l'appliance.  
  
![DWConfig Appliance Time](./media/appliance-time-zone-configuration/SQL_Server_PDW_DWConfig_ApplTopTime.png "SQL_Server_PDW_DWConfig_ApplTopTime")  
  
## <a name="see-also"></a>Vedere anche  
[Avviare Gestione configurazione &#40;sistema di piattaforma Analitica&#41;](launch-the-configuration-manager.md)  
  
