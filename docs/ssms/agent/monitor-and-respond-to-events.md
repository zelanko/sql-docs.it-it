---
title: Monitorare e rispondere agli eventi | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- notifications [SQL Server], alert
- events [SQL Server], alerts
- alerts [SQL Server]
- notifications [SQL Server]
- events [SQL Server], automatically responding to
- administrator notifications [SQL Server Agent]
- automatic event responses
- SQL Server Agent alerts
- monitoring [SQL Server], events
- responding to events automatically
ms.assetid: f7fbe155-5b68-4777-bc71-a47637471f32
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: fae6e419838ef4de06e778665c98df023e7eb707
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/16/2019
ms.locfileid: "68267513"
---
# <a name="monitor-and-respond-to-events"></a>Monitoraggio e risposta agli eventi
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> In [Istanza gestita di database SQL di Azure](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita del database SQL di Azure e SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent può monitorare e rispondere automaticamente agli *eventi*, ad esempio messaggi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], a condizioni specifiche delle prestazioni e agli eventi del servizio Strumentazione gestione Windows (WMI).  
  
## <a name="in-this-section"></a>Contenuto della sezione  
[Avvisi](../../ssms/agent/alerts.md)  
Sono incluse informazioni sulla denominazione di un avviso e sulla selezione di eventi o condizioni delle prestazioni a cui rispondono gli avvisi.  
  
[Creazione di un evento definito dall'utente](../../ssms/agent/create-a-user-defined-event.md)  
Sono incluse informazioni sulla creazione di eventi diversi da quelli predefiniti di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
[Operatori](../../ssms/agent/operators.md)  
Sono incluse informazioni sulla creazione di alias per gli amministratori che possono essere utilizzati da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per inviare notifiche in caso di esito positivo o negativo dei processi.  
  
## <a name="about-monitoring-and-responding-to-events"></a>Informazioni sul monitoraggio e sulla risposta agli eventi  
Le risposte automatiche agli eventi sono denominate *Avvisi*. È possibile definire un avviso relativo a uno o più eventi per specificare la risposta di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent quando vengono generati tali eventi. Un avviso può rispondere a un evento informando un amministratore o eseguendo un processo oppure in entrambi i modi. Un avviso può inoltre inviare un evento al registro applicazioni di Microsoft Windows in un computer diverso. È possibile specificare che un operatore deve ricevere immediatamente una notifica se viene generato un evento con livello di gravità 19. La definizione di avvisi consente agli amministratori di database di monitorare e gestire [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]con maggiore efficienza.  
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent risponde solo agli eventi per cui è stato definito un avviso. Il metodo utilizzato in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per il monitoraggio degli eventi varia in base al tipo di evento.  
  
Se è stato definito un avviso di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent per un contatore delle prestazioni, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent esegue direttamente il monitoraggio di tale contatore. Per un evento WMI, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent registra la query di eventi.  
  
Per rispondere ai messaggi di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent esegue il monitoraggio del registro applicazioni di Windows. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent può rispondere solo ai messaggi contenuti in tale registro. Per impostazione predefinita, SQL Server inserisce nel registro applicazioni di Windows i messaggi seguenti:  
  
-   Errori sysmessages con livello di gravità 19 o superiore.  
  
    Se si desidera registrare anche gli errori sysmessages con livello di gravità inferiore a 19, utilizzare la stored procedure sp_altermessage per designarli come errori da registrare sempre.  
  
-   Qualsiasi istruzione RAISERROR richiamata tramite la sintassi WITH LOG.  
  
    RAISERROR WITH LOG è il metodo consigliato per la scrittura nel registro applicazioni di Windows da un'istanza di SQL Server.  
  
-   Qualsiasi evento dell'applicazione registrato tramite xp_logevent.  
  
    > [!NOTE]  
    > La registrazione di eventi delle applicazioni occupa spazio nel registro applicazioni di Windows causando il superamento delle dimensioni massime. Per evitare la perdita di informazioni sugli eventi di SQL Server, verificare che le dimensioni massime del registro applicazioni di Windows siano sufficienti.  
  
Quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registra un messaggio, il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent lo confronta con gli avvisi definiti dall'amministratore di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
Indipendentemente dall'origine dell'evento, il servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent risponde all'evento eseguendo le attività specificate nell'avviso corrispondente.  
  
## <a name="see-also"></a>Vedere anche  
[sp_altermessage](../../relational-databases/system-stored-procedures/sp-altermessage-transact-sql.md)  
  
