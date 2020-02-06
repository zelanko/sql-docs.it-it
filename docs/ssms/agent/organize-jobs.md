---
title: organizzare processi
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- job category
- organize jobs
ms.assetid: 629c3e06-f933-483b-8621-280dbb7a7bd1
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: a02f50ed88a2883d0149dbbd37df63b27e87dfa4
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 01/31/2020
ms.locfileid: "75247608"
---
# <a name="organize-jobs"></a>organizzare processi
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Le categorie consentono di organizzare i processi per semplificare le operazioni di raggruppamento e filtro. È ad esempio possibile organizzare tutti i processi di backup dei database raggruppandoli nella categoria Manutenzione database. È inoltre possibile creare categorie di processi personalizzate.  
  
> [!WARNING]  
> Le categorie multiserver sono disponibili solo in un server master. In un server master è disponibile una sola categoria di processi predefinita: [**Senza categoria (multiserver)** ]. Quando viene scaricato un processo multiserver, la categoria viene modificata in **Processi dal server MSX** nel server di destinazione.  
  
## <a name="related-tasks"></a>Attività correlate  
  
|||  
|-|-|  
|**Descrizione**|**Argomento**|  
|Descrive come creare una categoria di processi.|[Creare una categoria di processi](../../ssms/agent/create-a-job-category.md)|  
|Descrive come eliminare una categoria di processi.|[Eliminare una categoria di processi](../../ssms/agent/delete-a-job-category.md)|  
|Descrive come assegnare un processo a una categoria di processi.|[Assegnare un processo a una categoria di processi](../../ssms/agent/assign-a-job-to-a-job-category.md)|  
|Descrive come modificare l'appartenenza a una categoria di processi.|[Modificare l'appartenenza a una categoria di processi](../../ssms/agent/change-the-membership-of-a-job-category.md)|  
|Descrive come visualizzare un elenco di informazioni sulla categoria.|[Elencare le informazioni sulle categorie di processi](../../ssms/agent/list-job-category-information.md)|  
  
