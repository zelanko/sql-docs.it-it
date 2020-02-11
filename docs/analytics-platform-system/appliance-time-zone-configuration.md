---
title: Configurare il fuso orario
description: La pagina fuso orario consente di impostare il fuso orario per tutti i nodi nell'appliance del sistema di piattaforma di analisi (APS).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 1da16790d011a628bc2536de051eb1181f06b8cf
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401389"
---
# <a name="appliance-time-zone-configuration---analytics-platform-system"></a>Configurazione del fuso orario dell'appliance-sistema della piattaforma Analytics
La pagina **fuso orario** consente di impostare il fuso orario per tutti i nodi nell'appliance del sistema di piattaforma di analisi (APS).  
  
## <a name="to-set-the-time-zone"></a>Per impostare il fuso orario  
  
1.  Avviare il Configuration Manager. Per ulteriori informazioni, vedere [la pagina relativa all'avvio del&#41;di sistema della piattaforma Configuration Manager &#40;Analytics ](launch-the-configuration-manager.md).  
  
2.  Arrestare i servizi Appliance usando la pagina **stato Servizi** nella Configuration Manager. Per istruzioni, vedere [lo stato dei servizi PDW &#40;&#41;di sistema della piattaforma di analisi](pdw-services-status.md) .  
  
3.  Nel riquadro sinistro del Configuration Manager fare clic su **fuso orario**. Selezionare il fuso orario desiderato dal menu a discesa **fuso orario** . A seconda della posizione, è anche possibile scegliere di selezionare la casella accanto a **regola automaticamente orologio per l'ora legale**.  
  
4.  Fare clic su **applica** per salvare le modifiche.  
  
5.  Riavviare i servizi Appliance utilizzando la pagina **stato Servizi** nella Configuration Manager. Se si prevede anche di modificare i privilegi, è possibile eseguire questa operazione prima di riavviare l'appliance.  
  
![Ora dello strumento DWConfig](./media/appliance-time-zone-configuration/SQL_Server_PDW_DWConfig_ApplTopTime.png "SQL_Server_PDW_DWConfig_ApplTopTime")  
  
## <a name="see-also"></a>Vedere anche  
[Avviare la piattaforma Configuration Manager &#40;Analytics System&#41;](launch-the-configuration-manager.md)  
  
