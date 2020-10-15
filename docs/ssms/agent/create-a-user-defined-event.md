---
description: Creazione di un evento definito dall'utente
title: Creazione di un evento definito dall'utente
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent alerts, user-defined events
- user-defined events [SQL Server]
- multiple language support [SQL Server], alerts
- languages [SQL Server], alerts
- severity levels [SQL Server]
- global considerations [SQL Server], alerts
- events [SQL Server], user-defined
- SQL Server Agent alerts, multiple-language environments
- alerts [SQL Server], user-defined events
- alerts [SQL Server], multiple-language environments
- custom events [SQL Server Agent]
- international considerations [SQL Server], alerts
ms.assetid: 03d71a35-97fa-4bba-aa9a-23ac9c9cf879
author: markingmyname
ms.author: maghan
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: bf18385b89ac7af32bfde26d704880eb4e9bb300
ms.sourcegitcommit: 22dacedeb6e8721e7cdb6279a946d4002cfb5da3
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 10/14/2020
ms.locfileid: "92036667"
---
# <a name="create-a-user-defined-event"></a>Creazione di un evento definito dall'utente
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> In [Istanza gestita di SQL di Azure](/azure/sql-database/sql-database-managed-instance) sono attualmente supportate la maggior parte delle funzionalità di SQL Server Agent, ma non tutte. Per informazioni dettagliate, vedere [Differenze T-SQL tra Istanza gestita di SQL di Azure e SQL Server](/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent).

Per monitorare eventi diversi da quelli predefiniti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile creare eventi definiti dall'utente. È inoltre possibile assegnare un livello di gravità a ogni evento definito dall'utente.  
  
> [!NOTE]  
> Quando si usa [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], selezionare l'opzione **Scrivi nel registro eventi delle applicazioni di Windows** per ogni messaggio di evento definito dall'utente, in modo da assicurarsi che i messaggi vengano registrati. Per impostazione predefinita, i messaggi definiti dall'utente con livello di gravità minore di 19 non vengono inviati al registro delle applicazioni di [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows quando si verificano. Tali messaggi non generano quindi avvisi di SQL Server Agent.  
  
È necessario che agli eventi definiti dall'utente sia associato un numero di messaggio univoco. Tali numeri devono essere maggiori di 50.000. È possibile definire messaggi per l'evento in più lingue. Prima di potere aggiungere messaggi in altre lingue, è tuttavia necessario che sia disponibile un messaggio **En-US** .  
  
Se si amministra un ambiente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] multilingue, creare messaggi definiti dall'utente in ciascuna lingua supportata. Ad esempio se si crea un nuovo messaggio dell'evento che verrà utilizzato sia in un server con sistema operativo in inglese che in un server con sistema operativo in tedesco, utilizzare lo stesso numero di messaggio e lo stesso livello di gravità per entrambi, ma assegnare una lingua diversa a ognuno di essi.  
  
Nelle attività riportate di seguito sono disponibili informazioni su come creare eventi definiti dall'utente e avvisi in risposta a tali eventi.  
  
**Per creare un avviso in base a un numero di messaggio**  
  
-   [SQL Server Management Studio](../../ssms/agent/create-an-alert-using-an-error-number.md)  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)  
  
**Per creare un avviso in base ai livelli di gravità**  
  
-   [SQL Server Management Studio](../../ssms/agent/create-an-alert-using-severity-level.md)  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-alert-transact-sql.md)  
  
**Per definire la risposta a un avviso**  
  
-   [SQL Server Management Studio](../../ssms/agent/define-the-response-to-an-alert-sql-server-management-studio.md)  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-notification-transact-sql.md)  
  
**Per creare un messaggio di errore relativo a un evento definito dall'utente**  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-addmessage-transact-sql.md)  
  
**Per modificare un messaggio di errore relativo a un evento definito dall'utente**  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-altermessage-transact-sql.md)  
  
**Per eliminare un messaggio di errore relativo a un evento definito dall'utente**  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-dropmessage-transact-sql.md)  
  
**Per disabilitare o riattivare un avviso**  
  
-   [SQL Server Management Studio](../../ssms/agent/disable-or-reactivate-an-alert.md)  
  
-   [Transact-SQL](../../relational-databases/system-stored-procedures/sp-update-alert-transact-sql.md)  
  
## <a name="see-also"></a>Vedere anche  
[sp_update_alert (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-update-alert-transact-sql.md)  
