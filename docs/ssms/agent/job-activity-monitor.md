---
title: Monitoraggio attività processi | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.jobactivitymonitor.alljobs.f1
- SQL13.SWB.ACTIVITYMON.F1
ms.assetid: 11f2182c-5f71-46f8-8d2b-74f0fc48f2d6
author: markingmyname
ms.author: maghan
manager: jroth
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: e855db862f917306bd8217b16b6bfee9f92c7c21
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/09/2019
ms.locfileid: "67686987"
---
# <a name="job-activity-monitor"></a>Monitoraggio attività processi
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Utilizzare questa pagina per visualizzare l'attività corrente dei processi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Fare clic su **Filtro** per limitare i processi visualizzati. La griglia **Attività processi agente** è di sola lettura. Per ordinare la griglia fare clic sulle intestazioni di colonna. Per modificare un processo, selezionarlo facendo doppio clic per aprire la finestra di dialogo **Proprietà processo** . Fare clic con il pulsante destro del mouse su un processo nella griglia per avviare l'esecuzione di tutti i passaggi di processo, per avviare un particolare passaggio di processo, per disabilitare o abilitare il processo, per aggiornare il processo, per eliminare il processo, per visualizzare la cronologia del processo o per visualizzare le proprietà del processo. Fare clic su **Aggiorna** per aggiornare la griglia con le informazioni correnti.  
  
## <a name="options"></a>Opzioni  
**Nome**  
Nome del processo  
  
**Abilitata**  
Indica se il processo è abilitato (**sì**) o non abilitato (**no**).  
  
**Stato***  
Stato corrente del processo.  
  
**Risultati ultima esecuzione**  
Stato del processo all'ultima esecuzione.  
  
**Ultima esecuzione**  
Data e ora dell'ultima esecuzione del processo utilizzando la data e l'ora locali del server.  
  
**Prossima esecuzione***  
Data e ora pianificate per la successiva esecuzione del processo utilizzando la data e l'ora locali del server.  
  
**Category**  
Categoria assegnata al processo.  
  
**Eseguibile**  
**Sì** se il processo può essere eseguito, **No** se il processo non può essere eseguito. Un processo non può essere eseguito se non è associato a passaggi o a un server di destinazione.  
  
**Pianificato**  
**Sì** se il processo è assegnato a una programmazione processi, **No** se il processo non ha alcuna programmazione.  
  
*Solo i membri del ruolo predefinito del server sysadmin di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e il gruppo degli amministratori del server possono visualizzare i valori in questa colonna. Membri del ruolo SQLAgentOperatorRole non possono vedere i valori in questa colonna.  
  
#### <a name="to-open-the-job-activity-monitor"></a>Per aprire Monitoraggio attività processi  
  
-   In **Esplora oggetti**espandere il server, espandere **SQL Server Agent**, fare clic con il pulsante destro del mouse su **Monitoraggio attività processi**e scegliere **Visualizza attività processi**.  
  
## <a name="see-also"></a>Vedere anche  
[Monitoraggio delle attività del processo](../../ssms/agent/monitor-job-activity.md)  
  
