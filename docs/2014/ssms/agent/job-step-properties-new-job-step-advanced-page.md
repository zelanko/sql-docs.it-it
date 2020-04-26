---
title: 'Proprietà passaggio processo: nuovo passaggio di processo (pagina Avanzate) | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql12.ag.job.stepadvanced.f1
ms.assetid: bdecfd4f-bcd8-4ba2-8ada-fbb636314f40
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f0bc24411ebceb0601f00ca659452b55596d869c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "62937197"
---
# <a name="job-step-properties-new-job-step-advanced-page"></a>Proprietà passaggio processo: Nuovo passaggio di processo (pagina Avanzate)
  Utilizzare questa pagina per visualizzare e modificare le proprietà di un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] passaggio di processo di Agent.  
  
## <a name="options"></a>Opzioni  
 **Azione in caso di esito positivo**  
 Consente di impostare l'azione che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve eseguire in caso di esito positivo del passaggio di processo.  
  
 **Tentativi**  
 Consente di impostare il numero di tentativi eseguiti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per ripetere un passaggio di processo non riuscito.  
  
 **Intervallo tra i tentativi (minuti)**  
 Consente di impostare l'intervallo di attesa di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent tra l'esecuzione di un tentativo e l'altro.  
  
 **Azione in caso di esito negativo**  
 Consente di impostare l'azione che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent deve eseguire in caso di esito negativo del passaggio di processo.  
  
## <a name="options-for-transact-sql-job-steps"></a>Opzioni per i passaggi del processo Transact-SQL  
 **File di output**  
 Consente di impostare il file da utilizzare per l'output del passaggio di processo. Questa opzione è disponibile solo per i membri del ruolo predefinito del server **sysadmin** .  
  
 **...**  
 Selezionare il file da utilizzare per l'output del passaggio di processo.  
  
 **Visualizza**  
 In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], questo pulsante è disabilitato per la visualizzazione dei file di output. In alternativa, utilizzare Notepad per visualizzare i file di output del passaggio di processo.  
  
 **Accoda output a file esistente**  
 Consente di accodare l'output al contenuto già esistente nel file. Diversamente, il precedente contenuto del file viene sovrascritto ogni volta che il passaggio di processo viene eseguito.  
  
 **Registra nella tabella**  
 Consente di registrare l'output del passaggio di processo nella tabella **sysjobstepslogs** del database **msdb** .  
  
 **Visualizza**  
 Dopo avere eseguito almeno una volta il passaggio di processo, fare clic su **Visualizza** per visualizzare l'output corrispondente nella tabella.  
  
 **Accoda output a voce esistente nella tabella**  
 Consente di accodare l'output al contenuto già esistente nella tabella. Diversamente, il precedente contenuto della tabella viene sovrascritto ogni volta che il passaggio di processo viene eseguito.  
  
 **Includi output passaggio nella cronologia**  
 Selezionare questa opzione per includere l'output del passaggio di processo nella cronologia processo.  
  
 **Esegui come utente**  
 Se si è membri del ruolo predefinito del server **sysadmin** , è possibile selezionare un altro account di accesso SQL per eseguire questo passaggio di processo.  
  
## <a name="options-for-operating-system-cmdexec-job-steps"></a>Opzioni per i passaggi del processo Sistema operativo (CmdExec)  
 **File di output**  
 Consente di impostare il file da utilizzare per l'output del passaggio di processo.  
  
 **...**  
 Selezionare il file da utilizzare per l'output del passaggio di processo.  
  
 **Visualizza**  
 In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], questo pulsante è disabilitato per la visualizzazione dei file di output. In alternativa, utilizzare Notepad per visualizzare i file di output del passaggio di processo.  
  
 **Accoda output a file esistente**  
 Consente di accordare l'output del passaggio di processo al precedente contenuto del file ogni volta che il passaggio di processo viene eseguito.  
  
 **Registra nella tabella**  
 Consente di registrare l'output del passaggio di processo nella tabella **sysjobstepslogs** del database **msdb** .  
  
 **Visualizza**  
 Dopo avere eseguito almeno una volta il passaggio di processo, fare clic su **Visualizza** per visualizzare l'output corrispondente nella tabella.  
  
 **Accoda output a voce esistente nella tabella**  
 Consente di accodare l'output al contenuto già esistente nella tabella. Diversamente, il precedente contenuto della tabella viene sovrascritto ogni volta che il passaggio di processo viene eseguito.  
  
 **Includi output passaggio nella cronologia**  
 Selezionare questa opzione per includere l'output del passaggio di processo nella cronologia processo.  
  
## <a name="options-for-powershell-job-steps"></a>Opzioni per i passaggi di processo di PowerShell  
 **File di output**  
 Consente di impostare il file da utilizzare per l'output del passaggio di processo.  
  
 **...**  
 Selezionare il file da utilizzare per l'output del passaggio di processo.  
  
 **Visualizza**  
 In [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], questo pulsante è disabilitato per la visualizzazione dei file di output. In alternativa, utilizzare Notepad per visualizzare i file di output del passaggio di processo.  
  
 **Accoda output a file esistente**  
 Consente di accordare l'output del passaggio di processo al precedente contenuto del file ogni volta che il passaggio di processo viene eseguito.  
  
 **Registra nella tabella**  
 Consente di registrare l'output del passaggio di processo nella tabella **sysjobstepslogs** del database **msdb** .  
  
 **Visualizza**  
 Dopo avere eseguito almeno una volta il passaggio di processo, fare clic su **Visualizza** per visualizzare l'output corrispondente nella tabella.  
  
 **Accoda output a voce esistente nella tabella**  
 Consente di accodare l'output al contenuto già esistente nella tabella. Diversamente, il precedente contenuto della tabella viene sovrascritto ogni volta che il passaggio di processo viene eseguito.  
  
 **Includi output passaggio nella cronologia**  
 Selezionare questa opzione per includere l'output del passaggio di processo nella cronologia processo.  
  
## <a name="options-for-replication-queue-reader-job-steps"></a>Opzioni per i passaggi del processo Lettura coda repliche  
 **Server**  
 Consente di impostare il server da utilizzare per un passaggio di processo Lettura coda repliche.  
  
 **Database**  
 Consente di impostare il database da utilizzare per un passaggio di processo Lettura coda repliche.  
  
## <a name="options-for-sql-server-analysis-services-job-steps"></a>Opzioni per i passaggi del processo SQL Server Analysis Services  
 **File di output**  
 Consente di impostare il file da utilizzare per l'output del passaggio di processo. Questa opzione è disponibile solo per i membri del ruolo predefinito del server **sysadmin** .  
  
 **...**  
 Selezionare il file da utilizzare per l'output del passaggio di processo.  
  
 **Visualizza**  
 In [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], questo pulsante è disabilitato per la visualizzazione di file di output. In alternativa, utilizzare Notepad per visualizzare i file di output del passaggio di processo.  
  
 **Accoda output a file esistente**  
 Consente di accodare l'output al contenuto già esistente nel file. Diversamente, il precedente contenuto del file viene sovrascritto ogni volta che il passaggio di processo viene eseguito.  
  
 **Registra nella tabella**  
 Consente di registrare l'output del passaggio di processo nella tabella **sysjobstepslogs** del database **msdb** .  
  
 **Visualizza**  
 Dopo avere eseguito almeno una volta il passaggio di processo, fare clic su **Visualizza** per visualizzare l'output corrispondente nella tabella.  
  
 **Accoda output a voce esistente nella tabella**  
 Consente di accodare l'output al contenuto già esistente nella tabella. Diversamente, il precedente contenuto della tabella viene sovrascritto ogni volta che il passaggio di processo viene eseguito.  
  
 **Includi output passaggio nella cronologia**  
 Selezionare questa opzione per includere l'output del passaggio di processo nella cronologia processo.  
  
## <a name="see-also"></a>Vedi anche  
 [Gestire passaggi di processo](manage-job-steps.md)  
  
  
