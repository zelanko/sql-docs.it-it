---
title: Monitoraggio attività processi | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- SQL12.SWB.ACTIVITYMON.F1
- sql12.ag.jobactivitymonitor.alljobs.f1
ms.assetid: 11f2182c-5f71-46f8-8d2b-74f0fc48f2d6
author: stevestein
ms.author: sstein
ms.openlocfilehash: 58f04e83541f218a4cdcfbd99d6b3de12bf38b2f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 06/18/2020
ms.locfileid: "85064979"
---
# <a name="job-activity-monitor"></a>Monitoraggio attività processi
  Utilizzare questa pagina per visualizzare l'attività corrente dei processi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Fare clic su **Filtro** per limitare i processi visualizzati. La griglia **Attività processi agente** è di sola lettura. Per ordinare la griglia fare clic sulle intestazioni di colonna. Per modificare un processo, selezionarlo facendo doppio clic per aprire la finestra di dialogo **Proprietà processo** . Fare clic con il pulsante destro del mouse su un processo nella griglia per avviare l'esecuzione di tutti i passaggi di processo, per avviare un particolare passaggio di processo, per disabilitare o abilitare il processo, per aggiornare il processo, per eliminare il processo, per visualizzare la cronologia del processo o per visualizzare le proprietà del processo. Fare clic su **Aggiorna** per aggiornare la griglia con le informazioni correnti.  
  
## <a name="options"></a>Opzioni  
 **Nome**  
 Nome del processo.  
  
 **Enabled**  
 Indica se il processo è abilitato (**sì**) o non abilitato (**no**).  
  
 **Stato** <sup>1</sup>  
 Stato corrente del processo.  
  
 **Risultati ultima esecuzione**  
 Stato del processo all'ultima esecuzione.  
  
 **Ultima esecuzione**  
 Data e ora dell'ultima esecuzione del processo utilizzando la data e l'ora locali del server.  
  
 **Prossima esecuzione** <sup>1</sup>  
 Data e ora pianificate per la successiva esecuzione del processo utilizzando la data e l'ora locali del server.  
  
 **Categoria**  
 Categoria assegnata al processo.  
  
 **Eseguibile**  
 **Sì** se il processo può essere eseguito, **No** se il processo non può essere eseguito. Un processo non può essere eseguito se non è associato a passaggi o a un server di destinazione.  
  
 **Scheduled**  
 **Sì** se il processo è assegnato a una programmazione processi, **No** se il processo non ha alcuna programmazione.  
  
 <sup>1</sup> Solo i membri del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ruolo predefinito del server sysadmin e del gruppo Administrators del server possono visualizzare i valori in questa colonna. Membri del ruolo SQLAgentOperatorRole non possono vedere i valori in questa colonna.  
  
#### <a name="to-open-the-job-activity-monitor"></a>Per aprire Monitoraggio attività processi  
  
-   In **Esplora oggetti**espandere il server, espandere **SQL Server Agent**, fare clic con il pulsante destro del mouse su **Monitoraggio attività processi**e scegliere **Visualizza attività processi**.  
  
## <a name="see-also"></a>Vedere anche  
 [Monitoraggio delle attività del processo](monitor-job-activity.md)  
  
  
