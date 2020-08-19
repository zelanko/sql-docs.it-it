---
description: Aggiornamento dei dati in Monitoraggio replica
title: Aggiornare i dati in Monitoraggio replica | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- refreshing data
ms.assetid: e9582244-7d00-45f4-be16-020a65c76a5e
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: c3a493417a4c45b43e6b4b6c4c95f20fb4e4fac2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88380207"
---
# <a name="refresh-data-in-replication-monitor"></a>Aggiornamento dei dati in Monitoraggio replica
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  In Monitoraggio replica è possibile aggiornare automaticamente o manualmente la finestra principale e le finestre dei dettagli, ovvero le finestre avviate dalla finestra principale. Per aggiornare manualmente una finestra, premere F5. Per impostazione predefinita, la finestra principale viene aggiornata automaticamente ogni cinque secondi. È possibile personalizzare la frequenza di ogni server di pubblicazione.  
  
 I dati visualizzati in Monitoraggio replica provengono da query eseguite nella cache. Per informazioni sul rapporto tra la cache e l'aggiornamento di Monitoraggio replica, vedere [Memorizzazione nella cache, aggiornamento e prestazioni di Monitoraggio replica](../../../relational-databases/replication/monitor/caching-refresh-and-replication-monitor-performance.md). Per informazioni sull'avvio di Monitoraggio replica, vedere [Avviare Monitoraggio replica](../../../relational-databases/replication/monitor/start-the-replication-monitor.md).  
  
### <a name="to-set-refresh-options-for-replication-monitor"></a>Per impostare le opzioni di aggiornamento di Monitoraggio replica
  
1.  Fare clic con il pulsante destro del mouse su un server di pubblicazione nel riquadro sinistro di Monitoraggio replica e quindi scegliere **Impostazioni server di pubblicazione**.  
  
2.  Nella finestra di dialogo **Impostazioni server di pubblicazione** , impostare le opzioni **Aggiornamento automatico** e **Frequenza di aggiornamento** . L'impostazione **Aggiornamento automatico** è valida per la finestra principale di Monitoraggio replica. L'impostazione **Frequenza di aggiornamento** è valida anche per le finestre dei dettagli sulle quali è stato impostato l'aggiornamento automatico. Le modifiche apportate all'impostazione avranno effetto sulle finestre dei dettagli solo alla loro successiva apertura.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  

### <a name="to-specify-that-a-detail-window-should-automatically-refresh"></a>Per impostare l'aggiornamento automatico di una finestra dei dettagli  
  
1.  Aprire una finestra dei dettagli in Monitoraggio replica. Ad esempio:  
  
    1.  Espandere un gruppo di server di pubblicazione nel riquadro sinistro, espandere un server di pubblicazione e quindi fare clic su una pubblicazione.  
  
    2.  Fare clic sulla scheda **Tutte le sottoscrizioni** .  
  
    3.  Fare clic con il pulsante destro del mouse su una sottoscrizione e quindi scegliere **Visualizza dettagli**.  
  
2.  Nella finestra dei dettagli **Sottoscrizione \<SubscriptionName>** fare clic su **Azione** e quindi fare clic su **Aggiornamento automatico**. La frequenza di aggiornamento viene determinata dall'impostazione **Frequenza di aggiornamento** nella finestra di dialogo **Impostazioni server di pubblicazione** .  
  
## <a name="see-also"></a>Vedere anche  
 [Monitoraggio della replica](../../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
