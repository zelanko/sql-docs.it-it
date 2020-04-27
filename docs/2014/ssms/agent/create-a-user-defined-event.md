---
title: Creare un evento definito dall'utente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
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
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 5625e65b1da45e05002b540774f441f2deabd3f4
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63260952"
---
# <a name="create-a-user-defined-event"></a>Creazione di un evento definito dall'utente
  Per monitorare eventi diversi da quelli predefiniti da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], è possibile creare eventi definiti dall'utente. È inoltre possibile assegnare un livello di gravità a ogni evento definito dall'utente.  
  
> [!NOTE]  
>  Quando si usa [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], selezionare l'opzione **Scrivi nel registro eventi delle applicazioni di Windows** per ogni messaggio di evento definito dall'utente, in modo da assicurarsi che i messaggi vengano registrati. Per impostazione predefinita, i messaggi definiti dall'utente con livello di gravità minore di 19 non vengono inviati al registro delle applicazioni di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows quando si verificano. Tali messaggi non generano quindi avvisi di SQL Server Agent.  
  
 È necessario che agli eventi definiti dall'utente sia associato un numero di messaggio univoco. Tali numeri devono essere maggiori di 50.000. È possibile definire messaggi per l'evento in più lingue. Prima di potere aggiungere messaggi in altre lingue, è tuttavia necessario che sia disponibile un messaggio **En-US** .  
  
 Se si amministra un ambiente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] multilingue, creare messaggi definiti dall'utente in ciascuna lingua supportata. Ad esempio se si crea un nuovo messaggio dell'evento che verrà utilizzato sia in un server con sistema operativo in inglese che in un server con sistema operativo in tedesco, utilizzare lo stesso numero di messaggio e lo stesso livello di gravità per entrambi, ma assegnare una lingua diversa a ognuno di essi.  
  
 Nelle attività riportate di seguito sono disponibili informazioni su come creare eventi definiti dall'utente e avvisi in risposta a tali eventi.  
  
 **Per creare un avviso in base a un numero di messaggio**  
  
-   [SQL Server Management Studio](create-an-alert-using-an-error-number.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-alert-transact-sql)  
  
 **Per creare un avviso in base ai livelli di gravità**  
  
-   [SQL Server Management Studio](create-an-alert-using-severity-level.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-alert-transact-sql)  
  
 **Per definire la risposta a un avviso**  
  
-   [SQL Server Management Studio](../sql-server-management-studio-ssms.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-add-notification-transact-sql)  
  
 **Per creare un messaggio di errore relativo a un evento definito dall'utente**  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addmessage-transact-sql)  
  
 **Per modificare un messaggio di errore relativo a un evento definito dall'utente**  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-altermessage-transact-sql)  
  
 **Per eliminare un messaggio di errore relativo a un evento definito dall'utente**  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-dropmessage-transact-sql)  
  
 **Per disabilitare o riattivare un avviso**  
  
-   [SQL Server Management Studio](disable-or-reactivate-an-alert.md)  
  
-   [Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-update-alert-transact-sql)  
  
## <a name="see-also"></a>Vedi anche  
 [sp_update_alert &#40;&#41;Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-update-alert-transact-sql)  
  
  
