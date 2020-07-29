---
title: Configurare i log degli errori (pagina Generale)
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
f1_keywords:
- sql13.ag.errorlog.configure.f1
ms.assetid: e08de622-6f87-470c-aee0-b2d6cb6cca88
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 6e23a0c27675a9d873387dc2face6924d7541fdc
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/01/2020
ms.locfileid: "85749119"
---
# <a name="configure-sql-server-agent-error-logs-general-page"></a>Configura log degli errori di SQL Server Agent (pagina Generale)

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Utilizzare questa schermata per visualizzare e aggiornare le impostazioni relative alla registrazione degli errori di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="options"></a>Opzioni  
**File di log degli errori**  
Consente di specificare il file in cui [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent dovrà scrivere i log degli errori.  
  
**...**  
Consente di individuare i file di log degli errori.  
  
**Scrivi log degli errori OEM**  
Consente di scrivere il file di log degli errori come file non Unicode. In questo modo, è possibile ridurre la quantità di spazio su disco utilizzata dal file di log. Quando questa opzione è selezionata, è tuttavia possibile che i messaggi contenenti dati Unicode siano più difficili da leggere.  
  
**Errori**  
Nel file di log vengono scritti soltanto gli errori e i messaggi informativi.  
  
**Avvisi**  
Nel file di log vengono scritti gli avvisi e i messaggi informativi.  
  
**Informazioni**  
Nel file di log vengono scritti soltanto i messaggi informativi.  
  
## <a name="see-also"></a>Vedere anche  
[Log degli errori di SQL Server Agent](../../ssms/agent/sql-server-agent-error-log.md)  
  
