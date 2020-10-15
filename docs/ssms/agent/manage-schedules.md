---
description: Gestione pianificazioni
title: Gestione pianificazioni
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.job.manageschedules.f1
ms.assetid: f56c0736-dccc-41d2-afcf-71344aff143a
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: af21aa75f777d2745901736dce695cf226f3cbcf
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/14/2020
ms.locfileid: "92037854"
---
# <a name="manage-schedules"></a>Gestione pianificazioni
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> In [Istanza gestita di SQL di Azure](/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte ma non tutte le funzionalità di SQL Server Agent. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita di SQL di Azure e SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Consente di visualizzare e modificare le proprietà per le pianificazioni dei processi di [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="options"></a>Opzioni  
**Pianificazioni disponibili**  
Consente di visualizzare l'elenco delle pianificazioni disponibili per questo utente. Si noti che un processo e una pianificazione devono appartenere allo stesso proprietario. Nell'elenco sono pertanto incluse solo le pianificazioni appartenenti al proprietario del processo.  
  
**Nome**  
Consente di visualizzare il nome della pianificazione.  
  
**Enabled**  
Selezionare questa opzione per abilitare la pianificazione.  
  
**Descrizione**  
Descrive le condizioni nelle quali la pianificazione esegue il processo.  
  
**Processi nella pianificazione**  
Consente di visualizzare l'elenco dei numeri di processo collegati alla pianificazione. Fare clic su un numero per visualizzare le proprietà del processo.  
  
**Nuovo**  
Fare clic su questo pulsante per creare una nuova pianificazione.  
  
**Elimina**  
Fare clic su questo pulsante per eliminare la pianificazione selezionata.  
  
**Proprietà**  
Fare clic su questo pulsante per modificare le proprietà della pianificazione selezionata.  
  
## <a name="see-also"></a>Vedere anche  
[Creazione e collegamento di pianificazioni ai processi](../../ssms/agent/create-and-attach-schedules-to-jobs.md)  
