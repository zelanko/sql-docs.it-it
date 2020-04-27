---
title: MSSQL_ENG024070 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- MSSQL_ENG024070 error
ms.assetid: 23ac7e00-fab6-429b-9f85-2736a322aa65
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 2f5fc8fdc9b522ad79e67a7769ba2571b7a80af9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 04/26/2020
ms.locfileid: "63023908"
---
# <a name="mssql_eng024070"></a>MSSQL_ENG024070
    
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
  
 "Executed as user \<: AccountUtente>. Replica-sottosistema snapshot repliche: \<Agent agentname> non riuscito. Eseguita come utente: \<AccountUtente>. Il client non dispone di un privilegio necessario. Passaggio non riuscito. `[SQLSTATE 42000] (Error 14151)`. Passaggio non riuscito."  
  
 Questo problema si verifica perché Gestione controllo servizi di Windows non concede le autorizzazioni necessarie al nuovo account di servizio di [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
## <a name="user-action"></a>Azione dell'utente  
 Per evitare questo problema in futuro, utilizzare sempre Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anziché Gestione controllo servizi di Windows per modificare gli account di servizio e le password.  
  
 Per risolvere il problema, utilizzare Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per ripristinare l'account di servizio originale. Utilizzare quindi Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] per modificare il nuovo account. Durante questa operazione, Gestione configurazione [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aggiunge il nuovo account al gruppo di sicurezza seguente:  
  
 SQLServer2008SQLAgentUser$ComputerName$InstanceName  
  
 L'appartenenza a questo gruppo di sicurezza consente al nuovo account di ottenere le autorizzazioni necessarie per eseguire il processo dell'agente di replica.  
  
## <a name="see-also"></a>Vedi anche  
 [Guida di riferimento a errori ed eventi &#40;&#41;di replica](errors-and-events-reference-replication.md)   
 [Gestire gli account di accesso e le password nella replica](security/identity-and-access-control-replication.md#manage-logins-and-passwords-in-replication)   
 [Gestione configurazione SQL Server](../sql-server-configuration-manager.md)  
  
  
