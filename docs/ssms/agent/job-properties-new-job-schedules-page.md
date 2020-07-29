---
title: Proprietà processo - Nuovo processo (pagina Pianificazioni)
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.schedules.f1
ms.assetid: 0b03585b-a510-484d-8a63-9b32459def9c
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: cd9d5a33ff433204cd066eef3d17f9ec7dfd10ff
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85782994"
---
# <a name="job-properties---new-job-schedules-page"></a>Proprietà processo - Nuovo processo (pagina Pianificazioni)
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Usare questa pagina per visualizzare e organizzare le pianificazioni relative a un processo di [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="options"></a>Opzioni  
**Elenco pianificazioni**  
Elenca le pianificazioni relative al processo corrente.  
  
**Nuovo**  
Consente di creare una nuova pianificazione. Dopo la creazione, la pianificazione verrà aggiunta al processo.  
  
**Seleziona**  
Consente di selezionare una pianificazione tra quelle esistenti. Poiché un processo e una pianificazione devono avere lo stesso proprietario, questa opzione consente soltanto di selezionare una pianificazione dall'elenco di quelle di cui si è proprietari.  
  
**Modifica**  
Consente di modificare la pianificazione selezionata per cambiare le proprietà di pianificazione di un processo.  
  
**Rimuovi**  
Consente di rimuovere dal processo la pianificazione selezionata. Se la pianificazione non è utilizzata da altri processi, viene eliminata dal database.  
  
## <a name="see-also"></a>Vedere anche  
[Implementazione di processi](../../ssms/agent/implement-jobs.md)  
  
