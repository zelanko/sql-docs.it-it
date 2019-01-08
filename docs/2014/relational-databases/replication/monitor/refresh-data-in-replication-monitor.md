---
title: Aggiornare i dati in Monitoraggio replica | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- refreshing data
ms.assetid: e9582244-7d00-45f4-be16-020a65c76a5e
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 03dae95f44b4166947da4ef7bd88b532db00dd03
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 12/03/2018
ms.locfileid: "52757903"
---
# <a name="refresh-data-in-replication-monitor"></a>Aggiornamento dei dati in Monitoraggio replica
  In Monitoraggio replica è possibile aggiornare automaticamente o manualmente la finestra principale e le finestre dei dettagli, ovvero le finestre avviate dalla finestra principale. Per aggiornare manualmente una finestra, premere F5. Per impostazione predefinita, la finestra principale viene aggiornata automaticamente ogni cinque secondi. È possibile personalizzare la frequenza di ogni server di pubblicazione.  
  
 I dati visualizzati in Monitoraggio replica provengono da query eseguite nella cache. Per informazioni sul rapporto tra la cache e l'aggiornamento di Monitoraggio replica, vedere [Memorizzazione nella cache, aggiornamento e prestazioni di Monitoraggio replica](caching-refresh-and-replication-monitor-performance.md). Per informazioni sull'avvio di Monitoraggio replica, vedere [Avviare Monitoraggio replica](start-the-replication-monitor.md).  
  
### <a name="to-set-refresh-options-for-replication-monitor"></a>Per impostare le opzioni di aggiornamento di Monitoraggio replica  
  
1.  Fare clic con il pulsante destro del mouse su un server di pubblicazione nel riquadro sinistro di Monitoraggio replica e quindi scegliere **Impostazioni server di pubblicazione**.  
  
2.  Nella finestra di dialogo **Impostazioni server di pubblicazione** , impostare le opzioni **Aggiornamento automatico** e **Frequenza di aggiornamento** . L'impostazione **Aggiornamento automatico** è valida per la finestra principale di Monitoraggio replica. L'impostazione **Frequenza di aggiornamento** è valida anche per le finestre dei dettagli sulle quali è stato impostato l'aggiornamento automatico. Le modifiche apportate all'impostazione avranno effetto sulle finestre dei dettagli solo alla loro successiva apertura.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
### <a name="to-specify-that-a-detail-window-should-automatically-refresh"></a>Per impostare l'aggiornamento automatico di una finestra dei dettagli  
  
1.  Aprire una finestra dei dettagli in Monitoraggio replica. Ad esempio:  
  
    1.  Espandere un gruppo di server di pubblicazione nel riquadro sinistro, espandere un server di pubblicazione e quindi fare clic su una pubblicazione.  
  
    2.  Fare clic sulla scheda **Tutte le sottoscrizioni** .  
  
    3.  Fare clic con il pulsante destro del mouse su una sottoscrizione e quindi scegliere **Visualizza dettagli**.  
  
2.  Nella finestra dei dettagli **Sottoscrizione \<NomeSottoscrizione>** fare clic su **Azione** e quindi scegliere **Aggiornamento automatico**. La frequenza di aggiornamento viene determinata dall'impostazione **Frequenza di aggiornamento** nella finestra di dialogo **Impostazioni server di pubblicazione** .  
  
## <a name="see-also"></a>Vedere anche  
 [Monitoraggio della replica](../monitoring-replication.md)  
  
  
