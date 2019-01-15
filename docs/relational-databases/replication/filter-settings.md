---
title: Impostazioni filtro | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
f1_keywords:
- sql13.rep.monitor.filtersettings.f1
ms.assetid: 1b401d7d-db8a-4ba1-acb1-b8dec14e3311
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a626e79a33c134a3bdde5880b68f2545c6dea78e
ms.sourcegitcommit: 7aa6beaaf64daf01b0e98e6c63cc22906a77ed04
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/09/2019
ms.locfileid: "54129641"
---
# <a name="filter-settings"></a>Impostazioni filtro
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La finestra di dialogo **Impostazioni filtro** consente di definire filtri per le griglie in Monitoraggio replica. Per visualizzare, ad esempio, solo le sottoscrizioni attive nella scheda **Tutte le sottoscrizioni** , selezionare **Stato** nella colonna **Nome colonna** , **Uguale a** nella colonna **Operatore** e **Attivo** nella colonna **Valore1** . Dopo avere definito un filtro basato su una o più colonne, il filtro viene applicato in modo che nella griglia venga visualizzato solo il subset di righe che corrispondono ai criteri di filtro.  
  
## <a name="options"></a>Opzioni  
 **Nome colonna**  
 Consente di selezionare il nome della colonna su cui si desidera basare il filtro. È possibile basare un filtro su una o più colonne.  
  
 **Operatore**  
 Consente di selezionare un operatore per il filtro, ad esempio **Minore o uguale a**.  
  
 **Valore1** e **Valore2**  
 Consentono di immettere o selezionare un valore per il filtro. Per la maggior parte degli operatori è sufficiente specificare un valore nella colonna **Valore1** , tuttavia, gli operatori **Compreso tra** e **Non compreso tra** richiedono anche un valore nella colonna **Valore2** .  
  
 **Cancella filtro**  
 Fare clic su questo pulsante per cancellare tutti i filtri definiti. Per rimuovere un solo filtro, selezionare la riga del filtro e premere Canc.  
  
## <a name="see-also"></a>Vedere anche  
 [Monitoraggio della replica](../../relational-databases/replication/monitor/monitoring-replication.md)  
  
  
