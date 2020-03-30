---
title: Seleziona pianificazione per il processo
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.pickscheduleforjob.f1
helpviewer_keywords:
- Pick Schedule for Job dialog box
ms.assetid: 6de2025d-c25c-47b9-9a25-18c294935c15
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 8b7da81bd6c0a54c96367fc24cc742fce6700974
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 03/29/2020
ms.locfileid: "75247622"
---
# <a name="pick-schedule-for-job"></a>Seleziona pianificazione per il processo
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Usare questa finestra di dialogo per selezionare una pianificazione esistente per il processo di [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="options"></a>Opzioni  
**Pianificazioni disponibili**  
Consente di elencare le pianificazioni disponibili per il processo. Poiché un processo e una pianificazione devono avere lo stesso proprietario, in questo elenco sono incluse solo le pianificazioni di proprietà del proprietario del processo.  
  
**Nome**  
Consente di visualizzare il nome della pianificazione.  
  
**Enabled**  
Questa opzione è selezionata se la pianificazione è abilitata.  
  
**Descrizione**  
Descrive le condizioni nelle quali la pianificazione esegue il processo.  
  
**Processi nella pianificazione**  
Consente di visualizzare l'elenco dei numeri di processo collegati alla pianificazione. Fare clic su un numero per visualizzare le proprietà del processo.  
  
**Proprietà**  
Apre la finestra di dialogo **Proprietà pianificazione processo** tramite la quale è possibile visualizzare informazioni sulla pianificazione.  
  
## <a name="see-also"></a>Vedere anche  
[Creazione e collegamento di pianificazioni ai processi](../../ssms/agent/create-and-attach-schedules-to-jobs.md)  
  
