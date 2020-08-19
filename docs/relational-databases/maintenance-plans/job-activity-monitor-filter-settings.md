---
description: Monitoraggio attività processi (Impostazioni filtro)
title: Monitoraggio attività processi (Impostazioni filtro) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.jobactivitymon.filter.f1
ms.assetid: 89cb0055-5262-447f-8464-7203d4caba78
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: f7533366a28517fcc2fdb8ca5c2e4ad0c0dd01c5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424053"
---
# <a name="job-activity-monitor-filter-settings"></a>Monitoraggio attività processi (Impostazioni filtro)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Utilizzare questa pagina per ridurre il numero di righe visualizzate in Monitoraggio attività processi. Immettere i criteri in una o più caselle disponibili per visualizzare solo le righe che soddisfano i valori specificati. Alcune caselle, ad esempio **Stato** o **Tipo blocco** , consentono di immettere un numero finito di valori possibili, disponibili in un elenco a discesa. In altre caselle, ad esempio **Applicazione** , è invece possibile immettere qualsiasi tipo e numero di valori sotto forma di elenco delimitato da virgole. Le icone sulla barra degli strumenti possono essere utilizzate per ordinare le caselle disponibili alfabeticamente o in base alla categoria. Fare clic sui criteri per visualizzarne una breve descrizione.  
  
 Per filtrare il Monitoraggio attività processi, specificare un numero qualsiasi di criteri di filtro, fare clic su **Applica filtro**e quindi su **OK**.  
  
## <a name="all-jobs"></a>Tutti i processi  
 Questo gruppo di criteri di filtro è disponibile per il filtraggio di Monitoraggio attività processi.  
  
 **Nome**  
 Consente di filtrare i processi in base al nome.  
  
 **Prossima esecuzione**  
 Consente di filtrare in base alla data pianificata per la prossima esecuzione.  
  
 **Eseguibile**  
 Consente di visualizzare i processi che possono essere eseguiti oppure quelli che non possono essere eseguiti. Selezionare **Sì** per visualizzare solo i processi che possono essere eseguiti, selezionare **No** per visualizzare solo i processi che non possono essere eseguiti oppure selezionare **Tutti** per visualizzare entrambi.  
  
 **Ultima esecuzione**  
 Consente di filtrare in base alla data dell'ultima esecuzione.  
  
 **Risultati ultima esecuzione**  
 Consente di filtrare in base allo stato dell'ultima esecuzione dei processi.  
  
 **Enabled**  
 Consente di visualizzare solo i processi abilitati o non abilitati.  
  
 **Categoria**  
 Consente di filtrare in base alla categoria del processo.  
  
 **Pianificate**  
 Consente di visualizzare tutti i processi che dispongono o non dispongono di pianificazioni.  
  
 **Status**  
 Consente di filtrare i processi in base allo stato.  
  
## <a name="description-area"></a>Area descrizione  
 **Casella descrizione**  
 In questa casella senza nome viene visualizzata una breve descrizione dei criteri nel momento in cui vengono selezionati.  
  
 **Applica filtro**  
 Per applicare il filtro, fare clic su **Applica filtro** e quindi su **OK**. Per conservare le impostazioni di filtro nella finestra di dialogo **Impostazioni filtro** senza applicarle, deselezionare **Applica filtro** e quindi fare clic su **OK** in modo da visualizzare tutte le righe.  
  
 **Cancella**  
 Consente di ripristinare le impostazioni di filtro predefinite.  
  
## <a name="see-also"></a>Vedere anche  
 [Monitoraggio delle attività del processo](../../ssms/agent/monitor-job-activity.md)  
  
  
