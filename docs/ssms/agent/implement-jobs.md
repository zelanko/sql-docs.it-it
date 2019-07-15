---
title: Implementare processi | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent]
- SQL Server Agent jobs
- SQL Server Agent jobs, about jobs
- jobs [SQL Server Agent], about jobs
ms.assetid: 69e06724-25c7-4fb3-8a5b-3d4596f21756
author: markingmyname
ms.author: maghan
manager: jroth
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 804fd7c15a639df1b59059ddba11f2a341efa061
ms.sourcegitcommit: 5d839dc63a5abb65508dc498d0a95027d530afb6
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/09/2019
ms.locfileid: "67687006"
---
# <a name="implement-jobs"></a>Implementazione di processi
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

I processi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent consentono di automatizzare le attività amministrative di routine, in modo da rendere più efficiente l'amministrazione.  
  
Un processo include una serie di operazioni specificate eseguite in sequenza da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Un processo può eseguire un'ampia gamma di attività, inclusa l'esecuzione di script [!INCLUDE[tsql](../../includes/tsql-md.md)] , applicazioni della riga di comando, script Microsoft ActiveX, pacchetti di Integration Services, comandi e query di Analysis Services o attività di replica. I processi possono eseguire attività ripetitive o pianificabili e possono inviare automaticamente agli utenti notifiche sullo stato dei processi tramite la generazione di avvisi, semplificando notevolmente l'amministrazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
È possibile eseguire un processo manualmente oppure configurarlo per l'esecuzione in base a una pianificazione o in risposta ad avvisi.  
  
## <a name="related-tasks"></a>Attività correlate  
  
|||  
|-|-|  
|**Descrizione**|**Argomento**|  
|Contiene informazioni sulla creazione dei processi e sull'assegnazione della proprietà.|[Crea processi](../../ssms/agent/create-jobs.md)|  
|Contiene informazioni sull'organizzazione dei processi in categorie.|[Organizzare processi](../../ssms/agent/organize-jobs.md)|  
|Contiene informazioni sui diversi tipi di passaggi di processo che è possibile creare e sulla rispettiva modalità di gestione.|[Gestire passaggi di processo](../../ssms/agent/manage-job-steps.md)|  
|Contiene informazioni sulla definizione del momento di avvio dei processi e sulla relativa frequenza di esecuzione.|[Creazione e collegamento di pianificazioni ai processi](../../ssms/agent/create-and-attach-schedules-to-jobs.md)|  
|Sono incluse informazioni sull'esecuzione manuale dei processi (senza pianificazione).|[Esecuzione di processi](../../ssms/agent/run-jobs.md)|  
|Sono incluse informazioni sulla configurazione di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per rispondere ai processi. È possibile configurare [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent, ad esempio, in modo da notificare agli amministratori il completamento dei processi.|[Specifica delle risposte ai processi](../../ssms/agent/specify-job-responses.md)|  
|Contiene informazioni sulla visualizzazione dei processi esistenti e sulla cronologia processo eseguiti, nonché sulle modalità di modifica dei processi.|[Visualizzare o modificare processi](../../ssms/agent/view-or-modify-jobs.md)|  
|Contiene informazioni sulla modalità di eliminazione dei processi.|[Eliminare processi](../../ssms/agent/delete-jobs.md)|  
  
## <a name="see-also"></a>Vedere anche  
[Implementazione della sicurezza di SQL Server Agent](../../ssms/agent/implement-sql-server-agent-security.md)  
  
