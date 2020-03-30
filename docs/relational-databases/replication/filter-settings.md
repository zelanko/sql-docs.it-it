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
monikerRange: =azuresqldb-mi-current||>=sql-server-2016||=sqlallproducts-allversions
ms.openlocfilehash: e5fa57172b7d6ec49b58bf965d81a23d4916cb2e
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/30/2020
ms.locfileid: "76286411"
---
# <a name="filter-settings"></a>Impostazioni filtro
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
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
  
  
