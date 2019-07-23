---
title: MSSQL_ENG024070 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG024070 error
ms.assetid: 23ac7e00-fab6-429b-9f85-2736a322aa65
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 51dcb95500af71615b646bb8e9785374c2f26425
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 07/15/2019
ms.locfileid: "68022815"
---
# <a name="mssqleng024070"></a>MSSQL_ENG024070
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="message-details"></a>Dettagli messaggio  
  
|||  
|-|-|  
|Nome prodotto|SQL Server|  
|ID evento|24070|  
|Origine evento|MSSQLSERVER|  
|Componente|[!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]|  
|Nome simbolico||  
|Testo del messaggio|Il client non dispone di un privilegio necessario.|  
  
## <a name="explanation"></a>Spiegazione  
 Questo errore generale può essere generato indipendentemente dal fatto che la replica venga utilizzata o meno. Per un server di una topologia di replica, l'errore viene normalmente generato in seguito alla modifica dell'account del servizio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent tramite Gestione controllo servizi di [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows, anziché tramite Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Quando si tenta di eseguire un processo di agente dopo aver modificato l'account di servizio, il processo potrebbe avere esito negativo e restituire un messaggio di errore simile al seguente:  
  
 `Executed as user: \<UserAccount>. Replication-Replication Snapshot Subsystem: agent \<AgentName> failed. Executed as user: \<UserAccount>. A required privilege is not held by the client. The step failed. [SQLSTATE 42000] (Error 14151). The step failed.`  
  
 Questo problema si verifica perché Gestione controllo servizi di Windows non concede le autorizzazioni necessarie al nuovo account di servizio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="user-action"></a>Azione dell'utente  
 Per evitare questo problema in futuro, utilizzare sempre Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anziché Gestione controllo servizi di Windows per modificare gli account di servizio e le password.  
  
 Per risolvere il problema, utilizzare Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per ripristinare l'account di servizio originale. Utilizzare quindi Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per modificare il nuovo account. Durante questa operazione, Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aggiunge il nuovo account al gruppo di sicurezza seguente:  
  
 SQLServer2008SQLAgentUser$ComputerName$InstanceName  
  
 L'appartenenza a questo gruppo di sicurezza consente al nuovo account di ottenere le autorizzazioni necessarie per eseguire il processo dell'agente di replica.  
  
## <a name="see-also"></a>Vedere anche  
 [Guida di riferimento a errori ed eventi &#40;replica&#41;](../../relational-databases/replication/errors-and-events-reference-replication.md)   
 [Gestire gli account di accesso e le password nella replica](../../relational-databases/replication/security/identity-and-access-control-replication.md)   
 [Gestione configurazione SQL Server](../../relational-databases/sql-server-configuration-manager.md)  
  
  
