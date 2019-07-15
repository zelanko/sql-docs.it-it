---
title: Proprietà SQL Server Agent (pagina Sistema processi) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.agent.job.f1
ms.assetid: e171d13e-1302-4f0e-88be-67d656aec8d3
author: markingmyname
ms.author: maghan
manager: jroth
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 2da80fa6ba2e8b28c91b8750e4515acaa6b1cddc
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/09/2019
ms.locfileid: "67681790"
---
# <a name="sql-server-agent-properties-job-system-page"></a>Proprietà SQL Server Agent (pagina Sistema processi)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Usare questa pagina per visualizzare e modificare il modo in cui il servizio [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent gestisce i processi.  
  
## <a name="options"></a>Opzioni  
**Intervallo di timeout chiusura (secondi)**  
Consente di specificare il numero di secondi di attesa del completamento dei processi prima che questi vengano chiusi da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Se il processo è ancora in esecuzione dopo la scadenza dell'intervallo specificato, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent lo arresterà in modo forzato.  
  
**Usa account proxy non amministratore**  
Imposta un account proxy non amministratore per [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)] e versioni successive supportano più proxy, pertanto questa opzione è applicabile unicamente quando si gestiscono le versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent precedenti a [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)].  
  
**User name**  
Digitare il nome dell'utente per l'account proxy non amministratore. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta più proxy, pertanto questa opzione è applicabile unicamente quando si gestiscono versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent precedenti a [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)].  
  
**Password**  
Digitare la password dell'utente per l'account proxy non amministratore. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versioni successive supportano più proxy, pertanto questa opzione è applicabile unicamente quando si gestiscono le versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent precedenti a [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)].  
  
**Dominio**  
Digitare il dominio dell'utente per l'account proxy non amministratore. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] supporta più proxy, pertanto questa opzione è applicabile unicamente quando si gestiscono versioni di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent precedenti a [!INCLUDE[ssKatmai](../../includes/sskatmai_md.md)].  
  
## <a name="see-also"></a>Vedere anche  
[Implementazione di processi](../../ssms/agent/implement-jobs.md)  
  
