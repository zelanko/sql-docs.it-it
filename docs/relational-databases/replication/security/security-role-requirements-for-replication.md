---
title: Requisiti del ruolo di sicurezza per la replica | Microsoft Docs
description: Informazioni sul livello di autenticazione necessario per le attività comuni di configurazione e di manutenzione della replica in SQL Server.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- security [SQL Server replication], roles
- roles [SQL Server], replication
ms.assetid: b324a80f-4319-4cb2-847b-1910c49d90e0
author: MashaMSFT
ms.author: mathoma
monikerRange: =azuresqldb-mi-current||>=sql-server-2016
ms.openlocfilehash: 4c715601699b689a41765633a079b9d6a99da8b5
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: it-IT
ms.lasthandoff: 12/14/2020
ms.locfileid: "97475642"
---
# <a name="security-role-requirements-for-replication"></a>Requisiti del ruolo di sicurezza per la replica
[!INCLUDE[sql-asdbmi](../../../includes/applies-to-version/sql-asdbmi.md)]
  La replica limita le azioni specifiche che un utente può eseguire in base ai ruoli a cui viene eseguito il mapping dell'account di accesso dell'utente. La replica concede determinate autorizzazioni al ruolo predefinito del server **sysadmin** , al ruolo predefinito del database **db_owner** e agli account di accesso presenti nell'elenco di accesso alla pubblicazione.  
  
## <a name="security-role-requirements-for-replication-setup"></a>Requisiti del ruolo di sicurezza per la configurazione della replica  
 Nella tabella seguente vengono descritti i livelli di autenticazione necessari per le normali attività di configurazione della replica:  
  
|Attività di configurazione|Requisito di appartenenza|  
|----------------|----------------------------|  
|Attivazione di un server di distribuzione, un server di pubblicazione o un Sottoscrittore.|Ruolo del server **sysadmin** nel server di pubblicazione.|  
|Attivazione di un database per la replica.|Ruolo del server **sysadmin** nel server di pubblicazione.|  
|Creazione di una pubblicazione.|Ruolo del database **db_owner** nel database di pubblicazione nel server di pubblicazione o ruolo del server **sysadmin** nel server di pubblicazione.|  
|Visualizzazione delle proprietà della pubblicazione.|Membro dell'elenco di accesso alla pubblicazione nel server di pubblicazione, ruolo del database **db_owner** nel database di pubblicazione nel server di pubblicazione o ruolo del server **sysadmin** nel server di pubblicazione.|  
|Creazione di una sottoscrizione.|Ruolo del database **db_owner** nel database di pubblicazione nel server di pubblicazione o ruolo del server **sysadmin** nel server di pubblicazione.<br /><br /> Ruolo del database **db_owner** nel database di sottoscrizione nel Sottoscrittore o ruolo del server **sysadmin** nel Sottoscrittore.|  
|Configurazione dei profili agenti.|Ruolo del server **sysadmin** nel server di distribuzione.|  
  
## <a name="security-role-requirements-for-replication-maintenance"></a>Requisiti del ruolo di sicurezza per la manutenzione della replica  
 Nella tabella seguente vengono descritti i livelli di autenticazione necessari per le normali attività di manutenzione della replica:  
  
|Attività di manutenzione|Requisito di appartenenza|  
|----------------------|----------------------------|  
|Modifica o eliminazione di un server di distribuzione, un server di pubblicazione o un Sottoscrittore.|Ruolo del server **sysadmin** nel server appropriato.|  
|Modifica o eliminazione di una pubblicazione.|Ruolo del database **db_owner** nel database di pubblicazione nel server di pubblicazione o ruolo del server **sysadmin** nel server di pubblicazione.|  
|Modifica o eliminazione di una sottoscrizione nel server di pubblicazione.|Ruolo del database **db_owner** nel database di pubblicazione nel server di pubblicazione o ruolo del server **sysadmin** nel server di pubblicazione.|  
|Modifica o eliminazione di una sottoscrizione nel Sottoscrittore.|Ruolo del database **db_owner** nel database di sottoscrizione nel Sottoscrittore o ruolo del server **sysadmin** nel Sottoscrittore.|  
|Contrassegno di una sottoscrizione per la reinizializzazione.|Sottoscrizione push: ruolo del database **db_owner** nel database di pubblicazione nel server di pubblicazione o ruolo del server **sysadmin** nel server di pubblicazione.<br /><br /> Sottoscrizione pull: ruolo del database **db_owner** nel database di sottoscrizione nel Sottoscrittore o ruolo del server **sysadmin** nel Sottoscrittore.|  
|Visualizzazione dell'attività, degli errori e della cronologia della replica tramite Monitoraggio replica. Un utente può modificare i profili, le pianificazioni o altri elementi degli agenti solo se è membro del ruolo del server **sysadmin** .|Ruolo del database **replmonitor** nel database di distribuzione nel server di distribuzione o ruolo del server **sysadmin** nel server di distribuzione.|  
|Gestione degli agenti di replica.|Ruolo del database **db_owner** nel database appropriato o ruolo del server **sysadmin** nel server appropriato.<br /><br /> Se l'agente è stato creato da un utente nel ruolo **sysadmin** e per l'agente non è stato specificato alcun account proxy, l'agente verrà eseguito nel contesto dell'account di [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Agent. In questo caso, un utente nel ruolo **db_owner** non può modificare il processo associato all'agente.|  
|Avvio o arresto di un agente di replica.|Proprietario del processo dell'agente o ruolo del server **sysadmin** nel server appropriato.|  
  
## <a name="see-also"></a>Vedere anche  
 [Replication Security Best Practices](../../../relational-databases/replication/security/replication-security-best-practices.md)   
 [Visualizzare e modificare le impostazioni di sicurezza della replica](../../../relational-databases/replication/security/view-and-modify-replication-security-settings.md)  
  
  
