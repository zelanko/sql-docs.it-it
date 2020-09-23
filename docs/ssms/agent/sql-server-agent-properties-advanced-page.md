---
description: Proprietà SQL Server Agent (pagina Avanzate)
title: Proprietà SQL Server Agent (pagina Avanzate)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.agent.advanced.f1
ms.assetid: a4d798ee-4c18-40d4-b6af-63d17503738c
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 96dcf5690bac961e08c222023e14d92b833cfff2
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 08/17/2020
ms.locfileid: "88318179"
---
# <a name="sql-server-agent-properties-advanced-page"></a>Proprietà SQL Server Agent (pagina Avanzate)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> In [Istanza gestita di SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita di SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Usare questa pagina per visualizzare e modificare le proprietà avanzate del servizio [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="options"></a>Opzioni  
**Inoltro eventi SQL Server**  
Le opzioni di questa categoria consentono di attivare e configurare l'inoltro di eventi.  
  
**Inoltra eventi a un altro server**  
Gli eventi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent vengono inoltrati a un server diverso.  
  
**Server**  
Consente di selezionare il nome del server al quale inoltrare gli eventi.  
  
**Eventi non gestiti**  
Solo gli eventi non gestiti vengono inoltrati al server specificato. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent inoltra solo gli eventi ai quali non risponde alcun avviso.  
  
**Tutti gli eventi**  
Vengono inoltrati tutti gli eventi. Quando un avviso nell'istanza locale risponde a un evento, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent inoltra l'evento ed elabora l'avviso.  
  
**Eventi con gravità maggiore o uguale a**  
Vengono inoltrati solo gli eventi il cui livello di gravità e maggiore o uguale al livello specificato.  
  
**Condizione di inattività CPU**  
Le opzioni di questa categoria consentono di definire le condizioni in base alle quali [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent esegue i processi pianificati per l'esecuzione in base alla pianificazione di inattività della CPU.  
  
**Imposta condizione di inattività CPU**  
Consente di definire le condizioni in base alle quali [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent considera la CPU come inattiva.  
  
**L'utilizzo medio della CPU è inferiore al**  
La percentuale di utilizzo della CPU al di sotto della quale la CPU viene considerata inattiva.  
  
**per almeno**  
Periodo di tempo durante il quale l'utilizzo medio della CPU deve essere al di sotto del livello specificato prima che [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent esegua i processi in base alla pianificazione di inattività della CPU.  
  
## <a name="see-also"></a>Vedere anche  
[Creazione e collegamento di pianificazioni ai processi](../../ssms/agent/create-and-attach-schedules-to-jobs.md)  
[Gestione di eventi](../../ssms/agent/manage-events.md)  
  
